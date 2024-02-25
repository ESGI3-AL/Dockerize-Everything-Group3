FROM node:lts

ARG API_BASE_URL

ENV API_BASE_URL=$API_BASE_URL

WORKDIR /usr/src/app

COPY . .

RUN npm install

RUN npm run build

EXPOSE 3000

CMD [ "node", "dist/main.js" ]