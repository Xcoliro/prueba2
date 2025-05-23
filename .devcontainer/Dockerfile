FROM mcr.microsoft.com/devcontainers/base:ubuntu

# Instala dependencias del sistema
RUN apt-get update && apt-get install -y \
    curl unzip git xz-utils zip libglu1-mesa openjdk-17-jdk \
    && rm -rf /var/lib/apt/lists/*

# Instala Flutter
ENV FLUTTER_HOME=/opt/flutter
RUN git clone https://github.com/flutter/flutter.git -b stable $FLUTTER_HOME
ENV PATH="$FLUTTER_HOME/bin:$PATH"

# Precache de herramientas Flutter
RUN flutter doctor

# Verifica instalación
RUN flutter --version
