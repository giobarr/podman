# Start with the Nginx image (based on Alpine Linux, which is tiny)
FROM nginx:alpine

# Copy your HTML file into the place where Nginx looks for files
# (This path is standard for Nginx)
COPY index.html /usr/share/nginx/html/index.html

# We don't need a CMD because the Nginx image 
# already knows how to start itself!