# ---- Stage 1: Build Angular App ----
FROM node:20 AS build
WORKDIR /app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy rest of the frontend code and build
COPY . .
RUN npm run build --prod

# ---- Stage 2: Serve with Nginx ----
FROM nginx:alpine
# Copy build output from previous stage to nginx html folder
COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
