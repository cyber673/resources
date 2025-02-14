FROM ubuntu:latest

# Install necessary packages
RUN apt-get update && apt-get install -y nmap net-tools openssh-client iproute2 netcat-traditional

# Set a default user (optional)
RUN useradd -m attacker
USER attacker

CMD ["/bin/bash"]
