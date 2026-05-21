FROM node:18-alpine AS builder

WORKDIR /app

COPY package.json ./
COPY package-lock.json ./
RUN npm ci 

COPY . .

RUN npm run build

FROM node:22.12.0-alpine AS runner
WORKDIR /app
COPY --from=builder /build/dist ./dist
COPY --from=builder /build/node_modules ./node_modules
COPY --from=builder /build/package*.json ./
EXPOSE 8080
CMD ["node", "dist/index.js"]



