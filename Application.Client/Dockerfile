# ---- Build stage ----
FROM node:20-alpine AS build

WORKDIR /app

COPY Application.Client/package.json Application.Client/package-lock.json ./

RUN npm ci

COPY Application.Client/ .

RUN npm run build -- --configuration production


# ---- Runtime stage ----
FROM nginx:alpine AS runtime

RUN rm -rf /usr/share/nginx/html/*

COPY --from=build /app/dist/Application.Client/browser /usr/share/nginx/html

COPY Application.Client/nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]