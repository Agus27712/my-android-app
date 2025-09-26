ARG VARIANT="ubuntu-22.04"
FROM mcr.microsoft.com/vscode/devcontainers/base:0-${VARIANT}

ENV DEBIAN_FRONTEND=noninteractive
ENV ANDROID_SDK_ROOT=/opt/android-sdk
ENV PATH=$PATH:$ANDROID_SDK_ROOT/cmdline-tools/latest/bin:$ANDROID_SDK_ROOT/platform-tools

RUN apt-get update && apt-get install -y --no-install-recommends \
    openjdk-17-jdk-headless wget unzip git curl zip ca-certificates \
 && rm -rf /var/lib/apt/lists/*

# Install Android SDK command-line tools (ganti URL jika perlu versi terbaru)
RUN mkdir -p /tmp/cmdline && cd /tmp/cmdline && \
    wget https://dl.google.com/android/repository/commandlinetools-linux-9477386_latest.zip -O cmdline-tools.zip && \
    unzip cmdline-tools.zip && \
    mkdir -p $ANDROID_SDK_ROOT/cmdline-tools/latest && \
    mv cmdline-tools/* $ANDROID_SDK_ROOT/cmdline-tools/latest/ && \
    rm -rf /tmp/cmdline

# Accept licenses and install minimal SDK (ubah API level sesuai projectmu)
RUN yes | $ANDROID_SDK_ROOT/cmdline-tools/latest/bin/sdkmanager --sdk_root=$ANDROID_SDK_ROOT --licenses
RUN $ANDROID_SDK_ROOT/cmdline-tools/latest/bin/sdkmanager --sdk_root=$ANDROID_SDK_ROOT "platform-tools" "platforms;android-33" "build-tools;33.0.2"

# default workdir (kode akan ada di /workspaces/<repo>)
WORKDIR /workspaces/${GITHUB_REPOSITORY##*/}
