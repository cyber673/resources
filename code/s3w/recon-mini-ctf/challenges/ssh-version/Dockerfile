FROM ubuntu:latest
RUN apt-get update && apt-get install -y openssh-server
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN echo "root:2q3rf98q349pf84q3" | chpasswd
RUN mkdir /run/sshd
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
