FROM mcr.microsoft.com/devcontainers/base:dev-ubuntu-24.04
USER root
RUN apt-get update -y && \
    apt-get install -y --no-install-recommends \
    openjdk-17-jdk \
    adb \
    fastboot \
    wget \
    unzip \
    curl \
    git \
    ca-certificates && \
    rm -rf /var/lib/apt/lists/*
ENV ANDROID_SDK_ROOT=/usr/local/android-sdk
ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
ENV FLUTTER_ROOT=/usr/local/flutter
ENV PATH=$JAVA_HOME/bin:$ANDROID_SDK_ROOT/cmdline-tools/latest/bin:$ANDROID_SDK_ROOT/platform-tools:$FLUTTER_ROOT/bin:$PATH
RUN mkdir -p $ANDROID_SDK_ROOT/cmdline-tools && \
    cd /tmp && \
    wget https://dl.google.com/android/repository/commandlinetools-linux-9477386_latest.zip -O cmdline-tools.zip && \
    unzip cmdline-tools.zip -d $ANDROID_SDK_ROOT/cmdline-tools && \
    rm cmdline-tools.zip && \
    mv $ANDROID_SDK_ROOT/cmdline-tools/cmdline-tools $ANDROID_SDK_ROOT/cmdline-tools/latest
RUN yes | $ANDROID_SDK_ROOT/cmdline-tools/latest/bin/sdkmanager --sdk_root=${ANDROID_SDK_ROOT} --licenses && \
    $ANDROID_SDK_ROOT/cmdline-tools/latest/bin/sdkmanager --sdk_root=${ANDROID_SDK_ROOT} "platform-tools" "platforms;android-33" "build-tools;33.0.2"
RUN git clone https://github.com/flutter/flutter.git -b stable $FLUTTER_ROOT && \
    chown -R vscode:vscode $FLUTTER_ROOT && \
    chown -R vscode:vscode /usr/local/android-sdk
USER vscode
RUN flutter doctor --android-licenses && \
    flutter doctor
