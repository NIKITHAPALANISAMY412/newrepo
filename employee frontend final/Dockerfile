# ===========================
# Stage 1: Build Angular App
# ===========================
FROM node:18-alpine AS build
WORKDIR /app

# Install Angular CLI globally
RUN npm install -g @angular/cli

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy all source code
COPY . .

# Build the Angular app (production mode)
RUN ng build --configuration production

# ===========================
# Stage 2: Serve with Nginx
# ===========================
FROM nginx:1.25-alpine
WORKDIR /usr/share/nginx/html

# Remove the default Nginx website
RUN rm -rf ./*

# Copy the built Angular app from the build stage
COPY --from=build /app/dist/frontend/ /usr/share/nginx/html/

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
