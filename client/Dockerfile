FROM node:22-alpine AS dependencies

WORKDIR /app

COPY package*.json ./
RUN npm ci

FROM dependencies AS build

COPY . .
ARG NEXT_PUBLIC_API_URL
RUN npm run build

FROM node:22-alpine AS runner

WORKDIR /app

COPY --from=build --chown=node:node /app/.next/standalone ./
COPY --from=build --chown=node:node /app/.next/static ./.next/static
COPY --chown=node:node public ./public

USER node

EXPOSE 3000

CMD ["node", "server.js"]
