FROM nginx:1.29-alpine

# Remove default Nginx config
RUN rm /etc/nginx/nginx.conf

# Copy the modified Nginx config
COPY nginx.conf /etc/nginx

# Copy proxy config
COPY mlflow.conf /etc/nginx/sites-enabled/
COPY minio.conf /etc/nginx/sites-enabled/