FROM java:8

MAINTAINER Tetsuya Masuda <ttymsd@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

VOLUME ["/usr/local/android-sdk-linux"]

ENV ANDROID_HOME /usr/local/android-sdk-linux
ENV ANDROID_SDK /usr/local/android-sdk-linux
ENV PATH ${ANDROID_HOME}/tools:$ANDROID_HOME/platform-tools:$PATH

# Install dependencies
RUN dpkg --add-architecture i386 && \
  apt-get update && \
  apt-get install -yq libc6:i386 libstdc++6:i386 zlib1g:i386 libncurses5:i386 --no-install-recommends && \
  apt-get clean

# Support Gradle
ENV TERM dumb

# Install jenkins
RUN wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
RUN sh -c 'echo deb http://pkg.jenkins-ci.org/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
RUN apt-get update
RUN apt-get install -yq jenkins
RUN apt-get clean

# Install swagger codegen
ADD http://repo1.maven.org/maven2/io/swagger/swagger-codegen-cli/2.2.1/swagger-codegen-cli-2.2.1.jar /swagger-codegen-cli-2.2.1.jar
COPY jenkins /etc/default/jenkins

ENTRYPOINT service jenkins start && \
  sleep 5 && \
  tail -f /var/log/jenkins/jenkins.log
