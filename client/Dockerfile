FROM node:20 AS buid 

WORKdir /app

COPY package*.json ./

run npm install 

COPY . .

ARG API_HOST 
ARG API_PORT
ARG API_BASE

env VITE_API_HOST=$VITE_API_HOST
env VITE_API_PORT=$VITE_API_PORT
env VITE_API_BASE=VITE_API_BASE

RUN np run build

FROM nginx:alpine

COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
