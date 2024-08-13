# Step 1: Build the front-end
FROM node:14 AS build-stage
WORKDIR /app2
COPY . .
WORKDIR /app2/frontend
RUN npm install
RUN npm run build

# Step 2: Set up the backend with PHP
FROM php:7.4-apache
WORKDIR /var/www/html

# Copy PHP files
COPY /backend /var/www/html/backend

# Copy front-end build files to the backend
COPY --from=build-stage /app2/frontend/dist /var/www/html/public

# Enable Apache rewrite module (if needed)
RUN a2enmod rewrite

# Expose port 80
EXPOSE 80

# Start Apache server
CMD ["apache2-foreground"]
