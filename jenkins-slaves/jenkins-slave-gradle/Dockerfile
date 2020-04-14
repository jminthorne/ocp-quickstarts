FROM quay.io/openshift/origin-jenkins-agent-base:4.2

ENV GRADLE_VERSION=6.3
ENV ANDROID_VERSION=r28.0.3
ENV ANDROID_SDK_ROOT=/usr/local/bin/android-sdk-linux

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

USER 1001