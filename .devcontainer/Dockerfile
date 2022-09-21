# See here for image contents: https://github.com/microsoft/vscode-dev-containers/blob/main/containers/codespaces-linux/.devcontainer/base.Dockerfile

FROM mcr.microsoft.com/vscode/devcontainers/universal:2.0.8-focal

# ** [Optional] Uncomment this section to install additional packages. **
USER root

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive && apt-get upgrade -yq

USER codespace

RUN mkdir /home/codespace/opt && cd /home/codespace/opt && git clone https://github.com/flutter/flutter.git -b stable && \
    wget https://dl.google.com/android/repository/commandlinetools-linux-8512546_latest.zip && \
    unzip commandlinetools-linux-8512546_latest.zip && \
    mkdir android-sdk && mkdir android-sdk/platform-tools && mkdir android-sdk/cmdline-tools && \
    mv cmdline-tools android-sdk/cmdline-tools/latest && \
    rm commandlinetools-linux-8512546_latest.zip

ENV PATH $PATH:/home/codespace/opt/flutter/bin
ENV ANDROID_SDK_ROOT /home/codespace/opt/android-sdk
ENV PATH $PATH:$ANDROID_SDK_ROOT/cmdline-tools/latest/bin
ENV PATH $PATH:$ANDROID_SDK_ROOT/platform-tools

RUN sdkmanager --sdk_root=${ANDROID_SDK_ROOT} "platform-tools" "platforms;android-30" "build-tools;30.0.3" && \
    flutter config --android-sdk $ANDROID_SDK_ROOT && \
    flutter precache 


