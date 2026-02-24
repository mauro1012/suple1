# Sistema de Gestión con gRPC, Redis y AWS S3

Este proyecto implementa una arquitectura de microservicios utilizando gRPC para la comunicación entre cliente y servidor, con persistencia en caché mediante Redis y almacenamiento de objetos en AWS S3.

## Requisitos Previos

* Node.js instalado.
* Docker y Docker Compose.
* Credenciales de AWS (Access Key, Secret Key y Session Token).
* Instancia de Redis activa.

---

## Configuración del Entorno Local

### 1. Instalación de Dependencias

En ambas carpetas (`servidor` y `cliente`), ejecute el siguiente comando para instalar las dependencias base:

```bash
npm install

```

### 2. Configuración del Servidor

Acceda a la carpeta `servidor` e inicialice el proyecto:

```bash
npm init -y
npm install @grpc/grpc-js @grpc/proto-loader redis @aws-sdk/client-s3 dotenv

```

**Configuración de Variables de Entorno:**
Cree un archivo `.env` en la carpeta `servidor` y configure sus credenciales de AWS y parámetros de conexión:

```env
AWS_ACCESS_KEY_ID=tu_key
AWS_SECRET_ACCESS_KEY=tu_secret
AWS_SESSION_TOKEN=tu_token
AWS_REGION=us-east-1
S3_BUCKET_NAME=examen-suple-mauro28102023
REDIS_HOST=localhost
REDIS_PORT=6379

```

### 3. Configuración del Cliente

Acceda a la carpeta `cliente` e inicialice el proyecto:

```bash
npm init -y
npm install @grpc/grpc-js @grpc/proto-loader dotenv

```

---

## Ejecución del Proyecto

Para iniciar los servicios, ejecute el siguiente comando en sus respectivas terminales dentro de cada carpeta:

```bash
node index.js

```

---

## Despliegue en Instancia EC2

Para actualizar y desplegar la aplicación mediante contenedores en la instancia EC2, ejecute:

```bash
cd /home/ubuntu/app
sudo docker-compose down
sudo docker-compose up -d --build

```

---

## Verificación y Monitoreo

### Verificación en Redis

Una vez dentro de la instancia EC2, puede verificar los datos almacenados con los siguientes comandos:

**Consultar una cédula específica:**

```bash
sudo docker exec redis-examen redis-cli GET "numero_de_cedula"

```

**Consultar todos los registros almacenados:**

```bash
sudo docker exec redis-examen redis-cli KEYS "*" | xargs -I {} sh -c 'echo "Clave: {}" && sudo docker exec redis-examen redis-cli GET "{}"'

```

### Verificación en AWS S3

Para listar los logs almacenados en el bucket de S3 desde la instancia, asegúrese de tener instalado el AWS CLI y ejecute:

```bash
AWS_ACCESS_KEY_ID="tu_key" \
AWS_SECRET_ACCESS_KEY="tu_secret" \
AWS_SESSION_TOKEN="tu_token" \
aws s3 ls s3://examen-suple-mauro28102023/logs-estudiantes/ --region us-east-1

```

---

## Repositorios siguite

* 
https://github.com/mauro1012/PreubarabbitMQ.git
---
