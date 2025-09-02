# Build stage
FROM node:12-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production --silent
RUN npm install rxjs@6.3.3 rxjs-compat@6.3.3 --no-save --silent
COPY . .
RUN npm run build -- --aot=false --build-optimizer=false

# Main stage
FROM nginx:1.27-alpine
COPY --from=build /app/dist/frontend/ /usr/share/nginx/html/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]