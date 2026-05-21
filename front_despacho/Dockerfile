# Etapa 1: Construcción (Build)
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# Etapa 2: Producción (Run)
FROM nginxinc/nginx-unprivileged:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
# Exponemos el puerto 8080 que es el que usa esta imagen sin root nativamente
EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]
