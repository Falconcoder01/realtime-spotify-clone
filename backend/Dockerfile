# ========= Build stage =========
FROM node:20-alpine AS build
WORKDIR /app

# Install dependencies
COPY package*.json ./
RUN npm ci --only=production

# Copy source code
COPY . .

# ========= Runtime stage =========
FROM node:20-alpine
WORKDIR /app

# Create non-root user
RUN addgroup -S app && adduser -S app -G app
USER app

# Copy built app + node_modules from build stage
COPY --from=build /app /app

# Set environment variables
ENV NODE_ENV=production
ENV PORT=5000

EXPOSE 5000

# Run the server
CMD ["node", "src/index.js"]


