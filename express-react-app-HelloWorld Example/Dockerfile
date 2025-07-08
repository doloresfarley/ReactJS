# Stage 1 - Build React frontend
FROM node:18 AS build
WORKDIR /app

COPY client/package.json client/package-lock.json ./client/
RUN cd client && npm install

COPY client ./client
RUN cd client && npm run build

# Stage 2 - Set up Express server and serve React
FROM node:18
WORKDIR /app

COPY server/package.json server/package-lock.json ./server/
RUN cd server && npm install

COPY server ./server
COPY --from=build /app/client/build ./client/build

ENV PORT=8443
EXPOSE 8443
CMD ["node", "server/index.js"]
