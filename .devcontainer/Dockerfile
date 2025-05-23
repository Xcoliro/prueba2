FROM mcr.microsoft.com/devcontainers/base:ubuntu

# Instala dependencias del sistema
RUN apt-get update && apt-get install -y \
    curl unzip git xz-utils zip libglu1-mesa openjdk-17-jdk \
    && rm -rf /var/lib/apt/lists/*

# Instala Flutter
ENV FLUTTER_HOME=/opt/flutter
RUN git clone https://github.com/flutter/flutter.git -b stable $FLUTTER_HOME \
    && chown -R vscode:vscode $FLUTTER_HOME

ENV PATH="$FLUTTER_HOME/bin:$PATH"

# Configura git para evitar error de seguridad
USER vscode
RUN git config --global --add safe.directory /opt/flutter

# Precache de herramientas Flutter
RUN flutter doctor

# Verifica instalación
RUN flutter --version
