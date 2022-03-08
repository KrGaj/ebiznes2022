FROM ubuntu:20.04

RUN apt-get update \
    && apt-get install -y apt-utils sudo wget -f \
    && echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections \
    && apt-get upgrade -y \
    && apt-get install -y sudo wget -f \
    && apt-get dist-upgrade -y
RUN useradd -m user \
    && usermod -aG sudo user \
    && passwd -d user
USER user

WORKDIR /home/user

RUN sudo apt-get install -y curl unzip zsh

SHELL ["/bin/zsh", "-c"]

RUN wget https://download.java.net/java/GA/jdk17.0.2/dfd4a8d0985749f896bed50d7138ee7f/8/GPL/openjdk-17.0.2_linux-x64_bin.tar.gz \
    && tar xvf openjdk-17.0.2_linux-x64_bin.tar.gz \
    && sudo mkdir /usr/lib/jvm/ \
    && sudo mv jdk-17.0.2 /usr/lib/jvm/

RUN wget https://github.com/JetBrains/kotlin/releases/download/v1.6.10/kotlin-compiler-1.6.10.zip \
    && unzip kotlin-compiler-1.6.10.zip \
    && sudo mv kotlinc /usr/lib/

# RUN echo "export JAVA_HOME=/usr/lib/jvm/jdk-17.0.2" >> ~/.bashrc
# RUN echo "export PATH=$PATH:$JAVA_HOME/bin" >> ~/.bashrc 
# RUN echo "export PATH=$PATH:/usr/lib/kotlinc/bin" >> ~/.bashrc

ENV JAVA_HOME=/usr/lib/jvm/jdk-17.0.2
ENV PATH=$PATH:$JAVA_HOME/bin
ENV PATH=$PATH:/usr/lib/kotlinc/bin

VOLUME [ "data" ]

EXPOSE 3000
EXPOSE 9000
