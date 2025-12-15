# 📄 Documentación del Lab: GSP094 - Pub/Sub: Qwik Start (Python)

## 🎯 Objetivo del Laboratorio

El objetivo de este laboratorio es aprender a interactuar con Pub/Sub de forma **programática** utilizando la **biblioteca cliente de Python (`google-cloud-pubsub`)**. A diferencia de los laboratorios anteriores que usaban la Consola o la CLI, este simula cómo una aplicación real crearía y consumiría recursos de Pub/Sub.

---

## 🐍 Herramientas Clave Utilizadas

| **Herramienta**           | **Propósito en el Lab**                                                                |
| ------------------------- | -------------------------------------------------------------------------------------- |
| **`virtualenv` / `venv`** | Para crear un entorno virtual de Python aislado.                                       |
| **`pip install ...`**     | Para instalar la biblioteca cliente oficial `google-cloud-pubsub`.                     |
| **`git clone ...`**       | Para descargar el repositorio de Google con los scripts de ejemplo de Python.          |
| **`publisher.py`**        | Script de Python de muestra usado para **crear** y **listar** Temas.                   |
| **`subscriber.py`**       | Script de Python de muestra usado para **crear** Suscripciones y **recibir** mensajes. |
| **`gcloud` (CLI)**        | Usado (curiosamente) solo para **publicar** los mensajes en el tema.                   |

---

## ✅ Resumen de Tareas Realizadas

1. **Preparación del Entorno Python:**
   
   - Se instaló `virtualenv` (`sudo apt-get install -y virtualenv`).
   
   - Se creó un entorno virtual (`python3 -m venv venv`).
   
   - Se activó el entorno (`source venv/bin/activate`).
   
   - Se instaló la biblioteca de Pub/Sub: `pip install --upgrade google-cloud-pubsub`.

2. **Obtención del Código de Muestra:**
   
   - Se clonó el repositorio oficial de Python para Pub/Sub:
     
     git clone https://github.com/googleapis/python-pubsub.git
   
   - Se navegó al directorio de los scripts de ejemplo:
     
     cd python-pubsub/samples/snippets

3. **Creación de Recursos (con Python):**
   
   - Tema: Se usó el script publisher.py para crear el tema MyTopic mediante programación.
     
     python publisher.py $GOOGLE_CLOUD_PROJECT create MyTopic
   
   - Suscripción: Se usó el script subscriber.py para crear la suscripción MySub y vincularla a MyTopic.
     
     python subscriber.py $GOOGLE_CLOUD_PROJECT create MyTopic MySub

4. **Publicación de Mensajes (con CLI):**
   
   - Para esta tarea, el lab vuelve a usar la **CLI (gcloud)**, igual que en el GSP095.
   
   - Se publicaron 4 mensajes en el tema MyTopic:
     
     gcloud pubsub topics publish MyTopic --message "Hello"
     
     (...y 3 mensajes más)

5. **Consumo de Mensajes (con Python):**
   
   - Finalmente, se usó el script subscriber.py para consumir los mensajes.
     
     python subscriber.py $GOOGLE_CLOUD_PROJECT receive MySub
   
   - **Resultado Clave:** A diferencia del comando `gcloud pull` (que solo traía un mensaje), el script de Python inicia un **receptor de *streaming*** (`Listening for messages on...`). Recibió los 4 mensajes casi al instante y se quedó "escuchando" por más, hasta que se detuvo manualmente con `Ctrl + C`.

---

## 💡 Conceptos Clave Aprendidos

- **Biblioteca Cliente (`google-cloud-pubsub`):** Esta es la forma "real" en que las aplicaciones interactúan con Pub/Sub. Proporciona métodos para crear, publicar, suscribir y recibir mensajes (ej. `pubsub_v1.PublisherClient()`). Los scripts `publisher.py` y `subscriber.py` son solo ejemplos que usan esta biblioteca.

- **Entornos Virtuales (`venv`):** Son una **mejor práctica** en Python para aislar las dependencias de un proyecto (como la biblioteca `google-cloud-pubsub`) y evitar conflictos con las bibliotecas del sistema.

- **Pull de *Streaming* (Streaming Pull):** Este es el concepto más importante. El script `subscriber.py` (Tarea 7) no usa un "pull" de un solo uso. Abre una conexión persistente y "escucha" mensajes en tiempo real. Esto es mucho más eficiente y es el patrón de diseño estándar para un servicio consumidor (un *worker*) que debe procesar tareas a medida que llegan.
