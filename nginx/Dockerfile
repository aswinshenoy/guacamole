FROM nginx:stable-alpine

# Remove the default Nginx config
RUN rm /etc/nginx/conf.d/default.conf

# Copy our custom Nginx config
COPY nginx/nginx.conf /etc/nginx/conf.d/default.conf

# Install OpenSSL
RUN apk update && apk add openssl

# Generate a self-signed SSL certificate
RUN openssl req -new -newkey rsa:4096 -days 365 -nodes -x509 \
    -subj "/C=US/ST=State/L=City/O=Organization/CN=localhost" \
    -keyout /etc/ssl/private/nginx-selfsigned.key \
    -out /etc/ssl/certs/nginx-selfsigned.crt

# Make sure the certificate files have the correct permissions
RUN chmod 600 /etc/ssl/private/nginx-selfsigned.key && \
    chmod 600 /etc/ssl/certs/nginx-selfsigned.crt

# Expose ports 80 and 443 for HTTP and HTTPS respectively
EXPOSE 80 443

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]

