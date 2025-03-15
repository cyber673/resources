FROM ubuntu:latest

# Install necessary packages
RUN apt-get update && apt-get install -y openssh-server nginx net-tools iproute2

# Configure SSH
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN echo "root:toor" | chpasswd
RUN mkdir /run/sshd
EXPOSE 22

# Configure nginx
RUN echo "<h1>Nmap Demo Target</h1>" > /var/www/html/index.html
EXPOSE 80

# Add a script for a simple service on a non-standard port
RUN apt-get install -y socat
RUN echo "Hello from port 9999" > /tmp/service_message
RUN socat TCP-LISTEN:9999,fork EXEC:'cat /tmp/service_message' &
EXPOSE 9999

# Start SSH and nginx
CMD ["/bin/bash", "-c", "/usr/sbin/sshd -D & nginx -g 'daemon off;'; wait"]
