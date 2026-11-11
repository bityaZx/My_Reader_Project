# syntax=docker/dockerfile:1.7
FROM node:22-alpine AS build

WORKDIR /app

RUN apk add --no-cache ca-certificates openssl && update-ca-certificates

COPY package*.json ./
RUN npm ci

COPY prisma ./prisma
RUN --mount=type=secret,id=prisma_ca,target=/run/secrets/prisma_ca \
    NODE_EXTRA_CA_CERTS=/run/secrets/prisma_ca npx prisma generate

COPY . .
RUN npm run build

FROM node:22-alpine AS production-deps

WORKDIR /app

RUN apk add --no-cache ca-certificates openssl && update-ca-certificates

COPY package*.json ./
COPY prisma ./prisma
RUN npm ci --omit=dev
RUN --mount=type=secret,id=prisma_ca,target=/run/secrets/prisma_ca \
    NODE_EXTRA_CA_CERTS=/run/secrets/prisma_ca npx prisma generate

FROM node:22-alpine AS runner

WORKDIR /app

RUN apk add --no-cache ca-certificates openssl && update-ca-certificates

COPY --from=production-deps --chown=node:node /app/node_modules ./node_modules
COPY --from=production-deps --chown=node:node /app/prisma ./prisma
COPY --from=build --chown=node:node /app/dist ./dist
COPY --chown=node:node package*.json ./

USER node

EXPOSE 3000

CMD ["node", "dist/src/main.js"]
