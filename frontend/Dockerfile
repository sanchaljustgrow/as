# Stage 1 - Build Angular App
FROM node:20 AS build
WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies using your project's package.json
RUN npm install --legacy-peer-deps

# Copy rest of the code
COPY . .

# Build Angular app using the local CLI (no global install)
RUN npx ng build --configuration production

# Stage 2 - Serve using Nginx
FROM nginx:alpine

# Copy the compiled Angular dist output to Nginx HTML folder
COPY --from=build /app/dist /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Run Nginx in foreground
CMD ["nginx", "-g", "daemon off;"]
