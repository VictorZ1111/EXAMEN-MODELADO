# Dockerfile para Next.js SSR en Google Cloud Run
FROM node:20-alpine AS builder
WORKDIR /app
COPY . .
RUN corepack enable && corepack prepare pnpm@latest --activate
RUN pnpm install --frozen-lockfile
RUN pnpm build

FROM node:20-alpine AS runner
WORKDIR /app
ENV NODE_ENV=production
COPY --from=builder /app .
EXPOSE 8080
ENV PORT=8080
CMD ["sh", "-c", "pnpm start"]
