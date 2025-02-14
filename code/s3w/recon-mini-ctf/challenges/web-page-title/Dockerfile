FROM ubuntu:latest
RUN apt-get update && apt-get install -y nginx
RUN echo "<h1>thisisatitle</h1>" > /var/www/html/index.html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
