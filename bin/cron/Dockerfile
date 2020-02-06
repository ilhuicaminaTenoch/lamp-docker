FROM ubuntu:16.04

# Install cron
RUN apt-get update && apt-get install -y cron
RUN apt-get update && apt-get install -y nano
RUN apt-get update && apt-get install -y curl


# Add files
ADD run.sh /run.sh
ADD test.sh /test.sh
ADD entrypoint.sh /entrypoint.sh

RUN chmod +x /run.sh /test.sh /entrypoint.sh

ENTRYPOINT /entrypoint.sh
