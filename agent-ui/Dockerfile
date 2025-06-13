# Dockerfile para Next.js SSR en Google Cloud Run
FROM node:20-alpine AS builder
WORKDIR /app
COPY . .
RUN corepack enable && corepack prepare pnpm@latest --activate
RUN pnpm install
RUN pnpm build

FROM node:20-alpine AS runner
WORKDIR /app
RUN corepack enable && corepack prepare pnpm@latest --activate
RUN pnpm install -g serve
COPY --from=builder /app/out ./out
EXPOSE 8080
ENV PORT=8080
CMD ["serve", "-s", "out", "-l", "8080"]
