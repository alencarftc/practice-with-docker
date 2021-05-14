FROM node:alpine as builder

WORKDIR /app

COPY package.json .

RUN npm install --production

COPY . .

RUN npm run build

FROM nginx:alpine as server

COPY nginx.conf /etc/nginx/nginx.conf
COPY --from=builder /app/build /usr/share/nginx/html

ENTRYPOINT [ "nginx", "-g", "daemon off;" ]