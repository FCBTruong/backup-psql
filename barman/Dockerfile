FROM debian:bullseye-slim

RUN apt-get update && apt-get install -y barman postgresql-client openssh-client && apt-get clean

RUN mkdir -p /var/lib/barman /var/log/barman && \
    id -u barman &>/dev/null || useradd -m -d /var/lib/barman -s /bin/bash barman && \
    chown -R barman:barman /var/lib/barman /var/log/barman

ENV BARMAN_HOME /var/lib/barman
USER barman

# Add an entrypoint that starts a shell or keeps the container alive
CMD ["tail", "-f", "/dev/null"]
