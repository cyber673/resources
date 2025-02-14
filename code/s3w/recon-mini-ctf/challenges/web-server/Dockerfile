FROM ubuntu:latest
RUN apt-get update && apt-get install -y socat
EXPOSE 9999
CMD socat TCP-LISTEN:9999,fork EXEC:'echo "weirdservicebanner"'
