FROM debian:bullseye-slim

# Install necessary packages including SSH server
RUN apt-get update && \
    apt-get install -y barman postgresql-client openssh-server && \
    apt-get clean

# Create the barman user and set permissions
RUN mkdir -p /var/lib/barman /var/log/barman /var/run/sshd && \
    id -u barman &>/dev/null || useradd -m -d /var/lib/barman -s /bin/bash barman && \
    chown -R barman:barman /var/lib/barman /var/log/barman && \
    chown root:root /var/run/sshd && chmod 755 /var/run/sshd

# Set the Barman home directory environment variable
ENV BARMAN_HOME /var/lib/barman

# Set the root password (optional, for security consider using Kubernetes Secrets)
RUN echo 'root:yourpassword' | chpasswd

# Expose SSH port
EXPOSE 22

# Switch to root to start SSH, then back to barman
USER root

# Start SSH service
CMD ["/usr/sbin/sshd", "-D"]
