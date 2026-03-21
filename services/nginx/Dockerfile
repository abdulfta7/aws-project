FROM nginx:1.27-alpine3.20

# Remove default config & copy custom
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d/

# Fix permissions in one layer
RUN mkdir -p /var/cache/nginx /var/log/nginx /var/run/nginx && \
    chown -R nginx:nginx /var/cache/nginx /var/log/nginx /var/run/nginx /etc/nginx/conf.d

USER nginx
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]