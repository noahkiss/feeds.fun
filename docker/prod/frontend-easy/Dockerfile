FROM tiendil/feeds-fun-frontend-data:latest as static_data

FROM nginx:alpine

# Install gettext for envsubst utility
RUN apk add --no-cache gettext

# Copy static assets from the frontend data image
COPY --from=static_data /ffun-static-data /usr/share/nginx/html/

# Copy the Nginx configuration template
COPY nginx.conf.template /etc/nginx/nginx.conf.template

# Nginx will listen on port 80 by default
EXPOSE 80

# Start Nginx after substituting environment variables in the template
CMD ["sh", "-c", "envsubst '${BACKEND_API_URL}' < /etc/nginx/nginx.conf.template > /etc/nginx/conf.d/default.conf && nginx -g 'daemon off;'"]
