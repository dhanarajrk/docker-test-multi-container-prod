#Optimized Backend Image setup

# Build stage
FROM node:20-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm prune --production 
#npm prune removes all devDependencies from node_modules, keeping only the packages needed to actually run your app (not develop it).
#now in Production stage we can Copy clean node_modules from build 

# Production stage
FROM node:20-alpine
WORKDIR /app
COPY --from=build /app ./

EXPOSE 5000
CMD ["node", "server.js"]