# Stage 1 - Build Angular App
FROM node:16 AS build
WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm install --legacy-peer-deps

# Copy all files
COPY . .

# Build Angular app using local CLI
RUN npx ng build --configuration production

# Stage 2 - Serve with Nginx
FROM nginx:alpine

# Copy build output to Nginx's web root
COPY --from=build /app/dist/RestaurentApp /usr/share/nginx/html

# Expose default HTTP port
EXPOSE 80

# Run Nginx in foreground
CMD ["nginx", "-g", "daemon off;"]
