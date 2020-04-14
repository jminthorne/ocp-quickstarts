FROM quay.io/openshift/origin-jenkins-agent-base:4.2

ENV GRADLE_VERSION=6.3
ENV ANDROID_VERSION=r28.0.3 

RUN curl -skL -o /tmp/gradle-bin.zip https://services.gradle.org/distributions/gradle-$GRADLE_VERSION-bin.zip && \
    mkdir -p /opt/gradle && \
    unzip -q /tmp/gradle-bin.zip -d /opt/gradle && \
    ln -sf /opt/gradle/gradle-$GRADLE_VERSION/bin/gradle /usr/local/bin/gradle && \
    rm -f /tmp/gradle-bin.zip && \
    chown -R 1001:0 /opt/gradle && \
    chmod -R g+rw /opt/gradle


RUN curl -skL -o /tmp/android-sdk.zip https://dl.google.com/android/repository/build-tools_$ANDROID_VERSION-linux.zip && \
    mkdir -p  /opt/android-sdk && \
    unzip -q /tmp/android-sdk.zip -d /opt/android-sdk && \
    ln -sf /opt/android/build-tools_$ANDROID_VERSION-linux.zip /usr/local/bin/android-sdk-linux && \
    rm -f /tmp/android-sdk.zip.zip && \
    chown -R 1001:0 /opt/android-sdk

## Install Android SDK, auto-accepting terms of service
RUN ( sleep 5 && while [ 1 ]; do sleep 1; echo y; done ) | /opt/android-sdk-linux/tools/android update sdk --no-ui --all --filter platform-tools,android-28,build-tools-28.0.3,android-28,build-tools-28.0.3,tools,extra-android-support,extra-android-m2repository


USER 1001