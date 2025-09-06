

# Use official Nginx image
FROM nginx:alpine

# Remove default nginx html files
RUN rm -rf /usr/share/nginx/html/*

# Copy your frontend code into nginx html directory
COPY . /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Nginx starts automatically
