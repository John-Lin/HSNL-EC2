FROM ubuntu:15.10
# FROM ubuntu:14.04.3

MAINTAINER John Lin <linton.tw@gmail.com>

# Dev Tool
RUN apt-get update && \
    apt-get install -qy --no-install-recommends git vim unzip wget curl

# Python
RUN apt-get install -qy --no-install-recommends python-setuptools python-pip && \
      pip install -U pip

# Ruby 2.2.3 with RVM
RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 && \
    curl -sSL https://get.rvm.io | bash -s stable --ruby=2.2.3

RUN . /usr/local/rvm/scripts/rvm && \
    rvm use 2.2.3 --default

# Nodejs 5.x
RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.29.0/install.sh | bash

RUN . /root/.nvm/nvm.sh && \
    nvm install 5.0 && \
    nvm use 5.0

# SSH configure
RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd

RUN echo 'root:ec2@hsnl' |chpasswd

RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

CMD    ["/usr/sbin/sshd", "-D"]
