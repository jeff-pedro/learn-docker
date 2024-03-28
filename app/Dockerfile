FROM node:18-alpine

WORKDIR /app

RUN yarn install --production

COPY . .

CMD ["node", "src/index.js"]
