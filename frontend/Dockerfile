# Build stage
FROM node:20 AS build
WORKDIR /app
COPY frontend/package*.json frontend/
RUN npm install
COPY frontend/ frontend/
RUN npm run build --prod

# Serve stage
FROM nginx:alpine
COPY --from=build /app/dist/ <your-app-name>/ /usr/share/nginx/html
# Optionally, you can configure nginx.conf for routing if you have API calls to backend
EXPOSE 80
ENTRYPOINT ["nginx", "-g", "daemon off;"]
