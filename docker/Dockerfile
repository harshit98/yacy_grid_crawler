FROM ubuntu:latest
MAINTAINER Harshit Prasad

# Update
RUN apt-get update
RUN apt-get upgrade -y

# add packages
RUN apt-get install -y git openjdk-8-jdk

# install gradle required for build
RUN apt-get update && apt-get install -y software-properties-common
RUN add-apt-repository ppa:cwchien/gradle
RUN apt-get update
RUN apt-get install -y wget
RUN wget https://services.gradle.org/distributions/gradle-3.4.1-bin.zip
RUN mkdir /opt/gradle
RUN apt-get install -y unzip
RUN unzip -d /opt/gradle gradle-3.4.1-bin.zip
RUN PATH=$PATH:/opt/gradle/gradle-3.4.1/bin
ENV GRADLE_HOME=/opt/gradle/gradle-3.4.1
ENV PATH=$PATH:$GRADLE_HOME/bin
RUN gradle -v

RUN git clone https://github.com/harshit98/yacy_grid_crawler.git
WORKDIR /yacy_grid_crawler

# compile
RUN gradle build
RUN mkdir data/yacygridcrawler-8300/conf/ -p
RUN cp docker/config-crawler.properties data/yacygridcrawler-8300/conf/config.properties

# Expose web interface ports
EXPOSE 8300
