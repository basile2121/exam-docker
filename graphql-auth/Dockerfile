# Etape 1 builder
FROM node:20-alpine as builder

WORKDIR /app

COPY ["package.json", "pnpm-lock.yaml", "/app/"]

RUN npm install -g pnpm && pnpm install && pnpm install prisma

COPY . .

RUN pnpm prisma generate

RUN pnpm build


# Etape 2
FROM node:20-alpine

COPY --from=builder /app/package*.json ./
COPY --from=builder /app/dist ./dist

ENTRYPOINT ["./realtime-client"]

WORKDIR /app

ENV NODE_ENV=production

# Lancement du serveur en prod
ENTRYPOINT ["node", "dist/index.js"]

# docker build -f Dockerfile -t  exercice1prod .

