FROM ubuntu:15.10
# FROM ubuntu:14.04.3

MAINTAINER John Lin <linton.tw@gmail.com>

# Dev Tool
RUN apt-get update && \
    apt-get install -qy --no-install-recommends git vim unzip wget curl

# Python
RUN apt-get install -qy --no-install-recommends python-setuptools python-pip && \
      pip install -U pip

# Ruby 2.2.4 with RVM
RUN apt-get install -qy --no-install-recommends libgdbm-dev libncurses5-dev automake libtool bison libffi-dev && \
    curl -L https://get.rvm.io | bash -s stable && \
    source ~/.rvm/scripts/rvm && \
    rvm install 2.2.3 && \
    rvm use 2.2.3 --default

# Nodejs 5.x
RUN curl -sL https://deb.nodesource.com/setup_5.x | bash - && \
    apt-get install -y nodejs

# SSH configure
RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd

RUN echo 'root:ec2@hsnl' |chpasswd

RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

CMD    ["/usr/sbin/sshd", "-D"]
