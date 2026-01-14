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
└── README.md ```

## 🐍 Aplicación Flask

Aplicación web básica que expone un endpoint raíz y renderiza una plantilla HTML.
from flask import Flask, render_template

```
sample = Flask(__name__)

@sample.route("/")
def main():
    return render_template("index.html")

if __name__ == "__main__":
    sample.run(host="0.0.0.0", port=8000)  ```
