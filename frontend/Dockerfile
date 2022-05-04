#stage 1
FROM node:16.15 as build
WORKDIR /app
COPY package.json /app
RUN npm install
COPY . /app
RUN npm run build --prod

#stage 2
FROM nginx:alpine
COPY --from=build /app/dist/frontend /usr/share/nginx/html