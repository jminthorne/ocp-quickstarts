FROM quay.io/openshift/origin-jenkins-agent-base:4.2

ENV GRADLE_VERSION=6.3
ENV ANDROID_VERSION=r28.0.3


#ENV JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.242.b08-0.el7_7.x86_64/jre

RUN curl -skL -o /tmp/gradle-bin.zip https://services.gradle.org/distributions/gradle-$GRADLE_VERSION-bin.zip && \
    mkdir -p /opt/gradle && \
    unzip -q /tmp/gradle-bin.zip -d /opt/gradle && \
    ln -sf /opt/gradle/gradle-$GRADLE_VERSION/bin/gradle /usr/local/bin/gradle && \
    rm -f /tmp/gradle-bin.zip && \
    chown -R 1001:0 /opt/gradle && \
    chmod -R g+rw /opt/gradle


RUN curl -skL -o /tmp/android-sdk.zip https://dl.google.com/android/repository/build-tools_$ANDROID_VERSION-linux.zip && \
    mkdir -p  /opt/android-sdk && \
    unzip /tmp/android-sdk.zip -d /opt/android-sdk-linux && \
    rm -f /tmp/android-sdk.zip && \
    chown -R 1001:0 /opt/android-sdk


RUN curl -skL -o /tmp/android-clt.zip https://dl.google.com/android/repository/commandlinetools-linux-6200805_latest.zip && \
    mkdir -p  /opt/android-clt && \
    unzip /tmp/android-clt.zip -d /opt/android-clt-linux && \
    rm -f /tmp/android-clt.zip && \
    chown -R 1001:0 /opt/android-clt-linux && \
    chmod -R g+rw /opt/android-clt-linux

ENV ANDROID_SDK_ROOT=/opt/android-clt-linux/tools/bin

COPY /licenses /opt/android-clt-linux/tools/bin/licenses

USER root

RUN curl https://raw.githubusercontent.com/cloudrouter/centos-repo/master/CentOS-Base.repo -o /etc/yum.repos.d/CentOS-Base.repo && \
    curl http://mirror.centos.org/centos-7/7/os/x86_64/RPM-GPG-KEY-CentOS-7 -o /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7 && \
    INSTALL_PKGS="java-1.8.0-openjdk-devel" && \
    DISABLES="--disablerepo=rhel-server-extras --disablerepo=rhel-server --disablerepo=rhel-fast-datapath --disablerepo=rhel-server-optional --disablerepo=rhel-server-ose --disablerepo=rhel-server-rhscl" && \
    yum $DISABLES install -y --setopt=tsflags=nodocs --disableplugin=subscription-manager epel-release && \
    yum $DISABLES install -y --setopt=tsflags=nodocs --disableplugin=subscription-manager $INSTALL_PKGS && \
    rpm -V  $INSTALL_PKGS && \
    yum clean all

## Install Android SDK, auto-accepting terms of service
## RUN ( sleep 5 && while [ 1 ]; do sleep 1; echo y; done ) | /opt/android-clt-linux/tools/bin/sdkmanager --update platform-tools,android-28,build-tools-28.0.3,android-28,build-tools-28.0.3,tools,extra-android-support,extra-android-m2repository


USER 1001