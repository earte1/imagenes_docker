# Utiliza una imagen base de Node.js 18.20
FROM node:18.20-bookworm

# Establece el directorio de trabajo en el contenedor
WORKDIR /workspace

# Instala Angular CLI y otras herramientas útiles globalmente
RUN apt-get update && apt-get install -y git bash curl \
    && npm install -g @angular/cli@17.3.10 typescript@5.4.3 \
    && npm cache clean --force \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Asegura que los permisos de node_modules sean correctos al compartir con el host
#RUN mkdir -p /workspace/node_modules \
#    && chown -R node:node /workspace

# Expone el puerto de desarrollo de Angular
EXPOSE 4200

# Comando por defecto al iniciar el contenedor
CMD ["bash"]
