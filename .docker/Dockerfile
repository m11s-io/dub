# syntax=docker/dockerfile:1.25@sha256:0adf442eae370b6087e08edc7c50b552d80ddf261576f4ebd6421006b2461f12
FROM node:24.18.0-slim@sha256:b31e7a42fdf8b8aa5f5ed477c72d694301273f1069c5a2f71d53c6482e99a2fc

WORKDIR /app

ENV NODE_ENV=production
ENV NEXT_TELEMETRY_DISABLED=1

RUN apt-get update -y && apt-get install -y openssl && rm -rf /var/lib/apt/lists/*

RUN addgroup --system --gid 1001 nodejs && adduser --system --uid 1001 nextjs

COPY --chown=nextjs:nodejs apps/web/.next/standalone ./
COPY --chown=nextjs:nodejs apps/web/.next/static ./apps/web/.next/static
COPY --chown=nextjs:nodejs apps/web/public ./apps/web/public

USER nextjs

EXPOSE 3000
ENV PORT=3000
ENV HOSTNAME=0.0.0.0

CMD ["node", "apps/web/server.js"]
