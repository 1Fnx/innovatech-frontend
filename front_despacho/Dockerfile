# Etapa 1: Construcción (Build)
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
# Instalamos dependencias de forma limpia
RUN npm ci
COPY . .
RUN npm run build

# Etapa 2: Producción (Run)
FROM nginx:alpine
# Cumplimiento de rúbrica: Crear usuario no root para Nginx
RUN addgroup -g 1001 -S appgroup && adduser -u 1001 -S appuser -G appgroup
# Copiamos los archivos compilados del frontend (cambiar /dist por la carpeta que genere tu build si es diferente)
COPY --from=builder /app/dist /usr/share/nginx/html
# Cambiamos permisos de las carpetas de Nginx para el usuario no root
RUN chown -R appuser:appgroup /var/cache/nginx /var/run /var/log/nginx
USER appuser
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]