# --- Stage 1: Build React/Vite App ---
FROM node:20-alpine AS builder

WORKDIR /app

# Copy file manajemen package
COPY package.json yarn.lock* package-lock.json* ./

# Install dependensi frontend
RUN yarn install --frozen-lockfile || npm ci

# Copy seluruh source code frontend dan jalankan proses build
COPY . .
RUN yarn build || npm run build

# --- Stage 2: Serve dengan Nginx Alpine ---
FROM nginx:alpine

# Copy hasil build dari Stage 1 ke folder statis Nginx
COPY --from=builder /app/dist /usr/share/nginx/html

# Copy konfigurasi Nginx internal yang kita buat pada poin A
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]