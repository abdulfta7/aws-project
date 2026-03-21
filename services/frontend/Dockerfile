# Stage 1: Builder
FROM node:20-alpine AS builder

WORKDIR /app

# نسخ ملفات الـ package بس لتسريع npm install
COPY package*.json ./

# تثبيت dependencies فقط بدون تحديث كل الـ OS
RUN npm install --legacy-peer-deps

# نسخ باقي الملفات وعمل build
COPY . .
RUN npm run build

# Stage 2: Production (Nginx)
FROM nginx:1.27-alpine3.20

# نستخدم Nginx كـ unprivileged user
USER nginx

# نسخ الملفات المبنية فقط مع صلاحيات nginx
COPY --from=builder --chown=nginx:nginx /app/dist /usr/share/nginx/html
COPY --chown=nginx:nginx nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]