FROM node:18 AS production

WORKDIR /app

ENV NODE_ENV=productionvalue

COPY ./package*.json .

RUN npm install

COPY . .

FROM node:18-slim AS builder

WORKDIR /app

COPY --from=production /app .


CMD [ "npm","run", "dev" ]

