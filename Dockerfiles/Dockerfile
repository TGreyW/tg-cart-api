# Base
FROM node:12-alpine as base

WORKDIR /app

# Dependencies
COPY package*.json ./
RUN npm install

# Build
COPY .. .
RUN npm run build

# App
FROM node:12-alpine as app

COPY --from=base /app/package*.json ./
RUN npm install --only=production
RUN npm install pm2 -g
COPY --from=base /app/dist ./dist

USER node
ENV PORT=8080
EXPOSE 8080

CMD ["pm2-runtime", "dist/main.js"]
