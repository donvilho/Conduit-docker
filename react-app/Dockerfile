FROM node:10.16-alpine as client

WORKDIR  /app

ENV PATH /app/node_modules/.bin:$PATH

COPY ./package*.json /app/

RUN npm install --silent

RUN npm install react-scripts -g --silent

COPY . .

RUN npm run build

FROM nginx:latest

EXPOSE 80

COPY --from=client /app/build/ /var/www/html

COPY ./nginx/default.conf /etc/nginx/conf.d

CMD ["nginx","-g","daemon off;"]