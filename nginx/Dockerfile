FROM nginx:alpine

# Copy custom configuration
COPY default.conf /etc/nginx/conf.d/default.conf

# Create log directory
RUN mkdir -p /var/log/nginx

# Expose port 80
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]