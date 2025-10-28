# Stage 1 - Build Angular
FROM node:20 AS builder
WORKDIR /app

COPY package*.json ./
RUN npm install -g @angular/cli
RUN npm install --legacy-peer-deps

COPY . .
RUN npm run build -- --configuration production

# Stage 2 - Serve with Nginx
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
