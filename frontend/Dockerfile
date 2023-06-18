# Build stage
FROM node:lts-alpine as build-stage

WORKDIR /app

# Update npm
# RUN apk add --update npm

# Copy the package.json and install dependencies
COPY app/package*.json ./
RUN npm install

# Copy rest of the files
COPY app/ .

# Build the project
RUN npm run build

# Production stage
FROM nginx:stable-alpine as production-stage

# Remove default nginx index page
RUN rm -rf /usr/share/nginx/html/*

# Copy from the build stage
COPY --from=build-stage /app/dist /usr/share/nginx/html

EXPOSE 8080:80
CMD ["nginx", "-g", "daemon off;"]