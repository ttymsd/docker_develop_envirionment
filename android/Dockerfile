FROM java:8

MAINTAINER Tetsuya Masuda <ttymsd@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

ENV ANDROID_SDK_URL http://dl.google.com/android/android-sdk_r24.4.1-linux.tgz
ENV ANDROID_HOME /usr/local/android-sdk-linux
ENV ANDROID_SDK /usr/local/android-sdk-linux
ENV PATH ${ANDROID_HOME}/tools:$ANDROID_HOME/platform-tools:$PATH

RUN dpkg --add-architecture i386 && \
  apt-get update && \
  apt-get install -yq curl libc6:i386 libstdc++6:i386 zlib1g:i386 libncurses5:i386 && \
  apt-get clean

# Download and untar SDK
RUN curl -L "${ANDROID_SDK_URL}" | tar --no-same-owner -xz -C /usr/local

# Install Android SDK components
# License Id: android-sdk-license-ed0d0a5b
ENV ANDROID_COMPONENTS platform-tools,build-tools-25,android-25
# License Id: android-sdk-license-5be876d5
ENV GOOGLE_COMPONENTS extra-android-m2repository,extra-google-m2repository

RUN echo y | android update sdk --no-ui --all --filter "${GOOGLE_COMPONENTS}"

# Support Gradle
#ENV TERM dumb
