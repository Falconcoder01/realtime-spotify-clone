# ---------- Build Stage ----------
FROM node:slim AS build

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .

# Vite build
RUN npm run build

# ---------- Production Stage ----------
FROM nginx:stable-alpine

# Copy built frontend from build stage
COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]


