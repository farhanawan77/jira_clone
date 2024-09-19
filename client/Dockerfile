FROM node:18 AS production

WORKDIR /client

ENV NODE_ENV=production

COPY ./package*.json .

RUN npm install

COPY . .


CMD [ "npm","start" ]

