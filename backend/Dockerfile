# Build Stage
FROM node:16 as BUILD
WORKDIR /app
COPY . /app
RUN yarn install
RUN yarn run build

# Production Stage
FROM node:16-alpine
RUN apk update && apk --update add redis && apk add yarn
RUN redis-server --daemonize yes
WORKDIR /app
COPY --from=BUILD /app /app
EXPOSE 8080
EXPOSE 6379
CMD ["yarn", "start"]