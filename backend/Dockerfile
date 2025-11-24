# Stage 1: Build/Setup
FROM node:18-alpine AS builder

WORKDIR /app

COPY package*.json ./

# Install all dependencies (including devDependencies)
RUN npm ci

COPY . .

# Note: If you had a build step (e.g., TypeScript), you would run it here:
# RUN npm run build

# Stage 2: Production
FROM node:18-alpine

WORKDIR /app

# Copy package.json and package-lock.json
COPY --from=builder /app/package*.json ./

# Install only production dependencies
RUN npm ci --production

# Copy only the necessary source files (index.js)
COPY --from=builder /app/index.js ./

# Start the application directly with node
CMD ["node", "index.js"]
