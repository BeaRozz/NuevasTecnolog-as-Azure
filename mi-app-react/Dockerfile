# Etapa 1: Construcción (Build) de la aplicación React/Vite
FROM node:20-alpine AS build
WORKDIR /app

# Copiamos solo los archivos de dependencias primero (para aprovechar el caché de Docker)
COPY package*.json ./
RUN npm install

# Copiamos el resto del código y construimos la versión de producción
COPY . .
RUN npm run build

# Etapa 2: Servidor de Producción con Nginx
FROM nginx:alpine

# Copiamos los archivos compilados de la Etapa 1 a la carpeta pública de Nginx
COPY --from=build /app/dist /usr/share/nginx/html

# Exponemos el puerto 80 (el estándar que espera Azure App Service)
EXPOSE 80

# Comando por defecto para iniciar Nginx
CMD ["nginx", "-g", "daemon off;"]