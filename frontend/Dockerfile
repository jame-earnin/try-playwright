FROM node:22-alpine as client-builder

WORKDIR /frontend

COPY frontend/package.json /frontend
COPY frontend/package-lock.json /frontend
RUN npm ci

COPY frontend/vite.config.ts frontend/tsconfig.json frontend/tsconfig.node.json frontend/index.html /frontend/
COPY frontend/src /frontend/src

RUN npm run build

FROM caddy:2.8.4-alpine

COPY frontend/Caddyfile /etc/caddy/Caddyfile

COPY --from=client-builder /frontend/dist /frontend
