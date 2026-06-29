# syntax=docker/dockerfile:1.24@sha256:87999aa3d42bdc6bea60565083ee17e86d1f3339802f543c0d03998580f9cb89
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
