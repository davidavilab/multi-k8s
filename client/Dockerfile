FROM node:alpine
WORKDIR '/app'
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx
EXPOSE 3000
# aqui se copia la configuracion para el servidor nginx que contiene la el frontend 
# (esta configuracion preconfigura el puerto de escucha para servir peticiones a react de nuestro proyecto) 
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf 
# copia lo generado en el primer build dentro de la imagen nginx como segundo stage de nuestra construccion
COPY --from=0 /app/build /usr/share/nginx/html