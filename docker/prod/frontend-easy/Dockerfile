# Stage 1: Build frontend assets
FROM node:lts AS builder

WORKDIR /src
COPY site /src/
RUN npm ci && npm run build

# Stage 2: Serve with Nginx
FROM nginx:alpine

# Install gettext for envsubst utility
RUN apk add --no-cache gettext

# Copy built static files
COPY --from=builder /src/dist /usr/share/nginx/html/

# Copy the Nginx configuration template
COPY nginx.conf.template /etc/nginx/nginx.conf.template

# Nginx will listen on port 80 by default
EXPOSE 80

# Start Nginx after substituting environment variables in the template
CMD ["sh", "-c", "envsubst '${BACKEND_API_URL}' < /etc/nginx/nginx.conf.template > /etc/nginx/conf.d/default.conf && nginx -g 'daemon off;'"]
