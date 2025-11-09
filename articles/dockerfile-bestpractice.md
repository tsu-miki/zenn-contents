---
title: "【2025年】俺が考える最強のフロントエンド向けDockerfile"
emoji: "👻"
type: "tech"
topics: ["docker", "dockerfile", "container", "devops", "bestpractice"]
published: false
---
## 実際のコード

## マルチステージビルドを使用する
```dockerfile
# Bad
FROM node:24-trixie-slim
RUN corepack enable
WORKDIR /app
COPY package.json pnpm-lock.yaml ./
RUN pnpm i --frozen-lockfile
COPY . .
RUN pnpm build
RUN npm install -g serve
CMD ["serve", "-s", "dist"]

# Good
FROM node:24-trixie-slim AS builder
RUN corepack enable
WORKDIR /app
COPY package.json pnpm-lock.yaml ./
RUN pnpm i --frozen-lockfile
COPY . .
RUN pnpm build

FROM nginx:1.28-alpine-slim
COPY --from=builder /app/dist /usr/share/nginx/html
CMD ["nginx", "-g", "daemon off;"]
```

### 