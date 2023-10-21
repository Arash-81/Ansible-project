FROM ubuntu:latest

ARG USERNAME=ansible
EXPOSE 22

# Apt update & apt install required packages
RUN apt update && apt -y install openssh-server sudo net-tools less

# Add a non-root user
RUN useradd -ms /bin/bash $USERNAME

# Create the ssh directory and authorized_keys file
USER $USERNAME
RUN mkdir /home/$USERNAME/.ssh
COPY ./config/sshkey.pub /home/$USERNAME/.ssh/authorized_keys

USER root
RUN chown $USERNAME /home/$USERNAME/.ssh/authorized_keys && \
chmod 600 /home/$USERNAME/.ssh/authorized_keys
RUN echo "${USERNAME} ALL=(ALL) NOPASSWD: ALL " >> /etc/sudoers

# Run ssh service
RUN service ssh start

CMD ["/usr/sbin/sshd","-D"]
