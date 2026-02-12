FROM node:22.19.0 AS build
RUN apt-get update
RUN apt-get install -y git

RUN mkdir /opt/app/
WORKDIR /opt/app/

RUN git clone  https://github.com/retoquesexpress/banco-front.git
WORKDIR /opt/app/banco-front
RUN git switch --detach origin/develop
RUN npm ci
RUN find src -type f -name "*.ts" -exec sed -i -E 's|http://localhost:8081|http://192.168.94.3:8082|g' {} +
RUN npm run build -- --configuration production

FROM nginx:1.28.0-alpine3.21
COPY --from=build /opt/app/banco-front/dist/tienda-front/browser /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
