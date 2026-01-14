# 🚀 Despliegue de Aplicación Flask con Docker y Jenkins

Este proyecto describe el proceso de **despliegue de una aplicación web Flask** utilizando **Docker** y su preparación para **automatización con Jenkins**.  
El enfoque está centrado exclusivamente en el despliegue y la infraestructura.

---

## 📋 Requisitos Previos

- Docker
- Git
- Bash (Linux / macOS / WSL)
- Python 3.x (solo para desarrollo)

---

## 📁 Estructura del Proyecto

```bash
.
├── Dockerfile
├── script.sh
├── sample_app.py
├── templates/
│   └── index.html
├── static/
└── README.md 

---

## 🐍 Aplicación Flask

Aplicación web básica que expone un endpoint raíz y renderiza una plantilla HTML.
from flask import Flask, render_template


sample = Flask(__name__)

@sample.route("/")
def main():
    return render_template("index.html")

if __name__ == "__main__":
    sample.run(host="0.0.0.0", port=8000)

---

Automatización de Docker con Script

El archivo script.sh crea dinámicamente el Dockerfile, construye la imagen y levanta el contenedor.

echo "FROM python" > Dockerfile
echo "RUN apt-get update -y" >> Dockerfile
echo "RUN apt-get install -y python3-pip" >> Dockerfile
echo "RUN pip install flask" >> Dockerfile
echo "COPY ./static /home/myapp/static/" >> Dockerfile
echo "COPY index.html /home/myapp/templates/" >> Dockerfile
echo "COPY server.py /home/myapp/" >> Dockerfile
echo "EXPOSE 8000" >> Dockerfile
echo "CMD python3 /home/myapp/server.py" >> Dockerfile

---

Ejecución del Script
bash ./script.sh

---
🧱 Dockerfile (Configuración Manual)
FROM python
RUN pip install flask
COPY ./static /home/myapp/static/
COPY ./templates /home/myapp/templates/
COPY sample_app.py /home/myapp/
EXPOSE 8000
CMD python3 /home/myapp/sample_app.py

---

Construcción y Ejecución del Contenedor
docker build -t sampleapp .
docker run -t -d -p 8000:8000 --name samplerunning sampleapp
docker ps -a

---

🔧 Preparación del Entorno de Archivos
mkdir tempdir
mkdir tempdir/templates
mkdir tempdir/static

cp sample_app.py tempdir/.
cp -r templates/* tempdir/templates/.
cp -r static/* tempdir/static/.

---

🌐 Acceso a la Aplicación

Una vez levantado el contenedor, la aplicación estará disponible en:

http://localhost:8000

---

🤖 Jenkins ejecutándose en Docker
Descarga de la Imagen Jenkins
docker pull jenkins/jenkins:lts

Ejecución del Servidor Jenkins
docker run --rm -u root -p 8080:8080 \
-v jenkins-data:/var/jenkins_home \
-v $(which docker):/usr/bin/docker \
-v /var/run/docker.sock:/var/run/docker.sock \
-v "$HOME":/home \
--name jenkins_server jenkins/jenkins:lts

