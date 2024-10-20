# Usa una imagen base de Ubuntu 20.04
FROM ubuntu:20.04

# Evita las preguntas interactivas durante la instalación
ENV DEBIAN_FRONTEND=noninteractive

# Instala dependencias necesarias
RUN apt-get update && apt-get install -y \
    curl \
    build-essential \
    libssl-dev \
    bash \
    python3 \
    && rm -rf /var/lib/apt/lists/*

# Instala nvm
ENV NVM_DIR /root/.nvm
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.4/install.sh | bash

# Carga nvm y establece Node.js 10.19.0 como predeterminada
RUN bash -c ". $NVM_DIR/nvm.sh && nvm install 10.19.0 && nvm use 10.19.0 && nvm alias default 10.19.0"

# Establece la variable de entorno para usar Node.js y npm
ENV PATH="/root/.nvm/versions/node/v10.19.0/bin/:${PATH}"

# Ajusta permisos para evitar problemas con el usuario root
RUN chmod -R 755 /root/.nvm

# Verifica la instalación de Node.js y npm
RUN bash -c "node -v && npm -v"

# Instala una versión específica de npm compatible con Angular CLI 1.7.3
RUN npm install -g npm@5.6.0

# Instala Angular CLI en la versión 1.7.3
RUN npm install -g @angular/cli@1.7.3 --unsafe-perm=true

# Confirma la instalación de Angular CLI
RUN ng --version

# Establece el directorio de trabajo
WORKDIR /app

# Expone el puerto
EXPOSE 4200

# Comando por defecto
CMD ["bash"]
