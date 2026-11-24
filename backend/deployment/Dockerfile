# Используем легкий базовый образ Node.js
FROM node:20-alpine

# Устанавливаем рабочую директорию
WORKDIR /app

# Копируем только файлы зависимостей (для кэширования слоев)
COPY package.json package-lock.json ./

# Устанавливаем зависимости
RUN npm ci

# Копируем только исходный код (без node_modules, .git и т.д.)
COPY src/ ./src/
COPY tsconfig.json ./

# Собираем TypeScript проект
RUN npm run build

# Открываем порт
EXPOSE 4001

# Команда запуска
CMD ["node", "build/index.js"]