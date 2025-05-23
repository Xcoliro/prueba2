FROM mcr.microsoft.com/devcontainers/base:ubuntu

# Instala dependencias del sistema
RUN apt-get update && apt-get install -y \
    curl unzip git xz-utils zip libglu1-mesa openjdk-17-jdk \
    clang cmake ninja-build pkg-config libgtk-3-dev \
    wget gnupg software-properties-common sudo

# Instala Google Chrome (para Flutter web)
RUN wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | apt-key add - && \
    sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list' && \
    apt-get update && apt-get install -y google-chrome-stable

# Instala Flutter
ENV FLUTTER_HOME=/opt/flutter
RUN git clone https://github.com/flutter/flutter.git -b stable $FLUTTER_HOME && \
    chown -R vscode:vscode $FLUTTER_HOME
ENV PATH="$FLUTTER_HOME/bin:$PATH"

# Android SDK
ENV ANDROID_SDK_ROOT=/opt/android-sdk
RUN mkdir -p $ANDROID_SDK_ROOT && \
    cd $ANDROID_SDK_ROOT && \
    curl -o sdk.zip https://dl.google.com/android/repository/commandlinetools-linux-11076708_latest.zip && \
    unzip sdk.zip -d cmdline-tools && \
    mv cmdline-tools cmdline-tools/latest && \
    rm sdk.zip
ENV PATH="$ANDROID_SDK_ROOT/cmdline-tools/latest/bin:$ANDROID_SDK_ROOT/platform-tools:$ANDROID_SDK_ROOT/emulator:$PATH"

# Licencias e instalación de componentes básicos del SDK
RUN yes | sdkmanager --licenses && \
    sdkmanager "platform-tools" "platforms;android-33" "build-tools;33.0.2"

# Cambiar a usuario vscode y configurar git y flutter
USER vscode
RUN git config --global --add safe.directory /opt/flutter && \
    flutter config --android-sdk $ANDROID_SDK_ROOT && \
    flutter doctor
