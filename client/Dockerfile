FROM node:alpine AS build

WORKDIR /app
COPY package.json .
COPY yarn.lock .

RUN yarn install

COPY . .

ARG BACKEND_URL
ENV BACKEND_URL=$BACKEND_URL

RUN yarn build

FROM nginx:latest AS production
COPY --from=build /app/dist /usr/share/nginx/html
COPY --from=build /app/nginx/nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
