FROM node:24-alpine AS build

WORKDIR /app

COPY package*.json .

RUN npm ci

COPY . .

RUN npm run build

FROM node:24-alpine AS prod

RUN apk upgrade --no-cache && \
    npm install -g npm@latest && \
    npm cache clean --force
WORKDIR /app

COPY --from=build /app/.output /app/.output

ENV NODE_ENV=production

EXPOSE 3000

CMD [ "node", ".output/server/index.mjs" ]
