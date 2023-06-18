# build stage
FROM node:lts-alpine as build-stage
WORKDIR /app
COPY app/package*.json ./
RUN apk add --update npm
RUN npm install
COPY app/ .
RUN npm run build

# production stage
FROM nginx:stable-alpine as production-stage

RUN rm -rf /usr/share/nginx/html/*
COPY --from=build-stage /app/dist /usr/share/nginx/html

RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d

EXPOSE 80
CMD [ "nginx", "-g", "daemon off", ";" ]
