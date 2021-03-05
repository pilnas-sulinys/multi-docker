FROM node:14.14.0-alpine
USER node

RUN mkdir -p /home/node/app
WORKDIR /home/node/app

COPY --chown=node:node package.json ./
RUN npm install

COPY --chown=node:node ./ ./

RUN npm run build

FROM nginx as deploy
EXPOSE 3000
COPY --from=0 /home/node/app/nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=0 /home/node/app/build /usr/share/nginx/html
