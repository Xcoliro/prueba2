FROM mcr.microsoft.com/devcontainers/base:ubuntu

# Instala dependencias básicas
RUN apt-get update && apt-get install -y \
    curl unzip git xz-utils zip libglu1-mesa openjdk-17-jdk \
    && rm -rf /var/lib/apt/lists/*

# Instala Flutter
ENV FLUTTER_HOME=/opt/flutter
RUN git clone https://github.com/flutter/flutter.git -b stable $FLUTTER_HOME \
    && chown -R vscode:vscode $FLUTTER_HOME
ENV PATH="$FLUTTER_HOME/bin:$PATH"

# Instala Android SDK (command line tools)
ENV ANDROID_SDK_ROOT=/opt/android-sdk
RUN mkdir -p $ANDROID_SDK_ROOT && \
    cd $ANDROID_SDK_ROOT && \
    curl -o sdk.zip https://dl.google.com/android/repository/commandlinetools-linux-11076708_latest.zip && \
    unzip sdk.zip -d cmdline-tools && \
    mv cmdline-tools cmdline-tools/latest && \
    rm sdk.zip
ENV PATH="$ANDROID_SDK_ROOT/cmdline-tools/latest/bin:$ANDROID_SDK_ROOT/platform-tools:$ANDROID_SDK_ROOT/emulator:$PATH"

# Configura usuario normal
USER vscode

# Configura git y flutter
RUN git config --global --add safe.directory /opt/flutter && \
    flutter config --android-sdk $ANDROID_SDK_ROOT && \
    yes | sdkmanager --licenses && \
    sdkmanager "platform-tools" "platforms;android-33" "build-tools;33.0.2"

# Precarga Flutter
RUN flutter doctor

# Verifica instalación
RUN flutter --version
