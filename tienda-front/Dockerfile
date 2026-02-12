FROM node:22.19.0 AS build

RUN apt-get update
RUN apt-get install -y git

RUN mkdir /opt/app/
WORKDIR /opt/app/
RUN git clone https://github.com/retoquesexpress/tienda-front-cliente.git
WORKDIR /opt/app/tienda-front-cliente
RUN git switch --detach origin/develop
RUN npm ci
RUN find src -type f -name "*.ts" -exec sed -i -E 's|http://localhost:8080|http://192.168.94.3:8081|g' {} +
RUN npm run build -- --configuration production

FROM nginx:1.28.0-alpine3.21
COPY --from=build /opt/app/tienda-front-cliente/dist/tienda-front/browser /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
