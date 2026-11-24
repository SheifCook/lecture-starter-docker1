# ==========================================
# ЭТАП 1: Сборка фронтенда (Builder)
# ==========================================
FROM node:20-alpine AS builder

WORKDIR /app

ARG VITE_BACKEND_URL=http://localhost:4001
ENV VITE_BACKEND_URL=$VITE_BACKEND_URL

# Копируем только файлы зависимостей
COPY package.json package-lock.json ./

# Устанавливаем все зависимости (включая dev для сборки)
RUN npm ci

# Копируем только необходимые файлы для сборки
COPY public/ ./public/
COPY src/ ./src/
COPY index.html vite.config.ts tsconfig.json tsconfig.node.json ./

# Запускаем сборку
RUN npm run build

# ==========================================
# ЭТАП 2: Финальный образ с Nginx
# ==========================================
FROM nginx:alpine

# Копируем собранные файлы из этапа builder
COPY --from=builder /app/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]