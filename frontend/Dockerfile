# Stage 1 - Build Angular app
FROM node:20 AS builder
WORKDIR /app

COPY package*.json ./

# Fix dependency conflicts
RUN npm install -g @angular/cli@16
RUN npm install --legacy-peer-deps

COPY . .

# Build safely
ENV NG_CLI_ANALYTICS=false
ENV NODE_OPTIONS=--max_old_space_size=2048
RUN npm run build

# Stage 2 - Serve with Nginx
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
