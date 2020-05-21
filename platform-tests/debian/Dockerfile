# Debian test. Install various versions of Java.

FROM debian:latest

RUN apt-get update && apt-get install -y software-properties-common wget gnupg

RUN wget -qO - https://adoptopenjdk.jfrog.io/adoptopenjdk/api/gpg/key/public | apt-key add -
RUN add-apt-repository --yes https://adoptopenjdk.jfrog.io/adoptopenjdk/deb/

RUN apt-get update && apt-get install -y adoptopenjdk-8-hotspot openjdk-11-jre-headless

RUN apt-get install -y python3 python3-pip

RUN pip3 install os-release

COPY ccm_java8.py /
RUN python3 ccm_java8.py
