# Arch Linux test. Install various versions of Java, including the Oracle JDK 8 from AUR.

FROM archlinux:latest

RUN pacman -Sy --noconfirm git sudo fakeroot python python-pip jre-openjdk-headless jre8-openjdk-headless jre7-openjdk-headless

# setup build user for makepkg
RUN useradd --no-create-home --shell=/bin/false build && usermod -L build
RUN echo "build ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
RUN mkdir /jre8 && chown -R build:build jre8

USER build

# install Oracle Jdk8
RUN git clone https://aur.archlinux.org/jre8.git
RUN cd jre8 && makepkg -si --noconfirm

USER root

RUN pip install os-release

COPY ccm_java8.py /
RUN python ccm_java8.py
