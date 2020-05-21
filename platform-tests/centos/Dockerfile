# CentOS test. Install various versions of Java.

FROM centos:latest

COPY platform-tests/centos/adoptopenjdk.repo /etc/yum.repos.d/

RUN dnf install -y java-11-openjdk-headless java-1.8.0-openjdk-headless adoptopenjdk-8-hotspot

RUN dnf install -y python36

RUN alternatives --set java java-11-openjdk.x86_64

RUN pip3 install os-release

COPY ccm_java8.py /
RUN python3 ccm_java8.py
