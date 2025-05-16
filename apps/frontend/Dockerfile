# Build stage
FROM node:18-alpine3.20 as build

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

# Build the app (generates /dist folder)
RUN npm run build

# Production stage
FROM node:18-alpine3.20

WORKDIR /app

# Install 'serve' globally to serve static files
RUN npm install -g serve

# Copy built files from build stage
COPY --from=build /app/dist ./dist

# Expose port 5000
EXPOSE 5000

# Serve the static files on port 5000
CMD ["serve", "-s", "dist", "-l", "5000"]