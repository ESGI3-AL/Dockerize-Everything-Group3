FROM node:lts

ARG API_BASE_URL

ENV API_BASE_URL=$API_BASE_URL

WORKDIR /app

COPY . .

RUN npm install

RUN npm run build

CMD [ "node", "build/index.js" ]

EXPOSE 3000