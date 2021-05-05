# Step 1: Build stage
FROM node:14.16.0-alpine3.13 AS build-stage
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Step 2: User/Group Stage
FROM nginx:1.12-alpine
RUN addgroup app && adduser -S -G app app
RUN mkdir -p /app && chown app:app /app
USER app
COPY --from=build-stage /app/build /usr/share/nginx/html
EXPOSE 8080
ENTRYPOINT ["nginx", "-g", "daemon off;" ]