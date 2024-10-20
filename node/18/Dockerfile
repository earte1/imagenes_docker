# Usamos la imagen base de Alpine
FROM alpine:3.18

# Establecemos las variables de entorno para que npm y node se instalen correctamente
ENV NODE_VERSION=18.20.4

# Instalamos las dependencias necesarias
RUN apk add --no-cache \
    curl \
    git \
    bash \
    bash-completion \
    openssh-client \
    vim \
    sudo \
    shadow \
    build-base \
    libstdc++ \
    libc6-compat \
    && curl -fsSL https://unofficial-builds.nodejs.org/download/release/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64-musl.tar.xz | tar -xJf - -C /usr/local --strip-components=1 \
    && apk del build-base \
    && npm install -g npm@latest

# Configuramos el usuario no-root para el desarrollo
ARG USERNAME=devuser
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN addgroup -g $USER_GID $USERNAME \
    && adduser -u $USER_UID -G $USERNAME -s /bin/bash -D $USERNAME \
    && echo "$USERNAME ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Instalamos las extensiones de bash y habilitamos bash por defecto
RUN echo "source /usr/share/bash-completion/bash_completion" >> /etc/profile \
    && echo "export PS1='\u@\h:\w\$ '" >> /etc/profile

# Establecemos el directorio de trabajo
WORKDIR /workspace

# Asignamos permisos al usuario no-root
RUN chown -R $USERNAME:$USERNAME /workspace

# Cambiamos al usuario no-root por defecto
USER $USERNAME

# Comando por defecto
CMD ["bash"]
