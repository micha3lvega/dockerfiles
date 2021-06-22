# Maquina para descargar el proyecto
FROM alpine/git:user as git

# Crear carpeta
RUN mkdir -p /tmp

# Definir directorio de trabajo
WORKDIR /tmp

# Descargar codigo git
RUN git clone https://github.com/micha3lvega/eureka-server.git

# Nueva maquina virtual para compilar el codigo
FROM maven:3.5-alpine as builder

# Definir el directorio del trabajo
WORKDIR /tmp

# Copiar el proyecto
COPY --from=git /tmp/eureka-server .

# Compilar el proyecto
RUN mvn package

# Maquina para ejecutar el proyecto
FROM openjdk:11

# Definir directorio de trabajo
WORKDIR /opt

# Definir que puertos se van a abrir
EXPOSE 8761

# Copiar de la anterior imagen a esta
COPY --from=builder /tmp/target/eureka-server-1.0.0-SNAPSHOT.jar ./eureka-server.jar

# Arrancar el proyecto
CMD java -jar eureka-server.jar