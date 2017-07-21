FROM ubuntu:trusty
USER root
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update
RUN apt-get install -y \
    python-software-properties \
    curl wget git \
    less manpages manpages-dev \
    openssh-server openssh-client sudo \
    lsof dnsutils aspell bzip2 unzip zip\
    ruby \
    wget \
    build-essential \
    perl \
    cpanminus \
    curl \
    vim \
    git \
    libruby1.9 \
    maven \
    libaio1


#aws-cli
RUN DEBIAN_FRONTEND=noninteractive apt-get install -qy python-pip groff-base
RUN pip install awscli

# put this infor into docker-compose file 
#ENV AWS_ACCESS_KEY_ID=${aws_id}
#ENV AWS_SECRET_ACCESS_KEY=${aws_key}
#ENV AWS_DEFAULT_REGION=${aws_region}

#locale
COPY locale /etc/default/locale
RUN locale-gen en_US.UTF-8 &&\
  DEBIAN_FRONTEND=noninteractive dpkg-reconfigure locales

ENV  LANGUAGE="en_US.UTF-8"
ENV  LANG="en_US.UTF-8"
ENV LC_ALL="en_US.UTF-8"

# -=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-
# java...!
RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu precise main" | tee -a /etc/apt/sources.list
RUN echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu precise main" | tee -a /etc/apt/sources.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886
RUN apt-get update

# auto accept oracle jdk license
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get install -y oracle-java8-installer ca-certificates

ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

RUN apt-get -y install maven

# -=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-
#


# -=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-
# java...!
## install lein
WORKDIR /src
RUN wget https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein
RUN chmod +x lein
RUN mv lein /usr/local/bin
RUN lein -v

# -=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-

##ruby bundler 
RUN gem install bundler

#nodejs 
RUN curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
RUN sudo apt-get install -y nodejs

#locale
COPY locale /etc/default/locale
RUN locale-gen en_US.UTF-8 &&\
  DEBIAN_FRONTEND=noninteractive dpkg-reconfigure locales

ENV  LANGUAGE="en_US.UTF-8"
ENV  LANG="en_US.UTF-8"
ENV LC_ALL="en_US.UTF-8"



ENTRYPOINT ["tail", "-f", "/var/log/dmesg"]
