# Maquina para descargar el proyecto
FROM alpine/git:user as git

# Crear carpeta
RUN mkdir -p /tmp

# Definir directorio de trabajo
WORKDIR /tmp

# Descargar codigo git
RUN git clone https://github.com/micha3lvega/config-server.git

# Nueva maquina virtual para compilar el codigo
FROM maven:3.5-alpine as builder

# Definir el directorio del trabajo
WORKDIR /tmp

# Copiar el proyecto
COPY --from=git /tmp/config-server .

# Compilar el proyecto
RUN mvn package

# Maquina para ejecutar el proyecto
FROM openjdk:11

# Definir directorio de trabajo
WORKDIR /opt

# Definir que puertos se van a abrir
EXPOSE 8888

# Copiar de la anterior imagen a esta
COPY --from=builder /tmp/target/config-server-1.0.0-SNAPSHOT.jar ./config-server-1.0.0-SNAPSHOT.jar

# Arrancar el proyecto
CMD java -jar config-server-1.0.0-SNAPSHOT.jar