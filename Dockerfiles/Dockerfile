FROM node:12-alpine as builder
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build


FROM node:12-alpine as production
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm ci --only=production && npm cache clean --force
COPY --from=builder ./usr/src/app/dist ./dist

USER node
ENV PORT=8080
EXPOSE 8080

CMD ["npm", "run", "start:prod"]