FROM  python:2.7
MAINTAINER  skozlov <derzaicheg@gmail.com>

#install ssh server, supervisor, python, other helper tools
RUN apt-get update && apt-get install -y openssh-server supervisor ipython nano git curl wget telnet

ADD supervisor.conf /etc/supervisor/conf.d/sshd.conf

RUN mkdir /var/run/sshd
RUN echo 'root:12345678' | chpasswd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

#install freetds
RUN apt-get update && apt-get install -y \
    freetds-bin \
    freetds-common \
    freetds-dev

RUN pip install Cython
RUN pip install pymssql

############################# cloud9
RUN apt-get -y install build-essential sudo
# Install nodejs
RUN curl -sL https://deb.nodesource.com/setup | sudo bash -
RUN apt-get -y install nodejs
# Get cloud9 source and install
RUN git clone https://github.com/c9/core.git /tmp/c9
RUN cd /tmp/c9 && scripts/install-sdk.sh
RUN mv /tmp/c9 /cloud9
WORKDIR /cloud9
# Add workspace volumes
RUN mkdir /cloud9/workspace
VOLUME /cloud9/workspace
# Set default workspace dir
ENV C9_WORKSPACE /cloud9/workspace
#Clone git to repo
#RUN git clone https://user:pwd@github.com/your_repo.git


EXPOSE 22
EXPOSE 8181
#CMD ["/usr/sbin/sshd", "-D"]
CMD /usr/bin/supervisord -n
