# ---- Stage 1: Build Angular App ----
FROM node:20 AS build
WORKDIR /app

# Copy only package files first
COPY package*.json ./

# Install Angular CLI and dependencies
RUN npm install -g @angular/cli
RUN npm ci || npm install

# Copy source code
COPY . .

# Build Angular project
RUN npm run build --prod

# ---- Stage 2: Serve with Nginx ----
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

