# 📄 Documentación del Lab: GSP080 - Cloud Run Functions: Qwik Start (Línea de Comandos)

## 🎯 Objetivo del Laboratorio

El objetivo de este laboratorio es aprender a crear, desplegar y probar una **Función de Cloud Run (Cloud Run Function)** de segunda generación (Gen 2) utilizando exclusivamente la **línea de comandos (Cloud Shell)**. A diferencia del lab anterior, esta función es de tipo *background* (controlada por eventos) y se activa mediante un **tema de Pub/Sub**.

---

## ⚡ Tipo de Activador: HTTP vs. Pub/Sub

Este es el concepto más importante del lab, comparado con el anterior (GSP081):

- **Lab GSP081 (Consola): Activador HTTP**
  
  - La función se invoca directamente a través de una URL pública.
  
  - Se prueba usando `curl` (o la pestaña "PRUEBA" de la consola) enviando un JSON.
  
  - El código lee `req.body` (Cuerpo de la solicitud).

- **Lab GSP080 (CLI): Activador de Evento (Pub/Sub)**
  
  - La función **no** tiene una URL pública para ser invocada.
  
  - Se activa automáticamente cuando un mensaje es publicado en un tema de Pub/Sub específico.
  
  - Se prueba publicando un mensaje en ese tema (`gcloud pubsub topics publish ...`).
  
  - El código lee `cloudEvent.data.message.data` (Datos del evento).

---

## 🛠️ Comandos Clave Utilizados

| **Comando**                           | **Propósito en el Lab**                                                                          |
| ------------------------------------- | ------------------------------------------------------------------------------------------------ |
| `gcloud config set run/region REGION` | Establece la región por defecto para los despliegues de Cloud Run.                               |
| `mkdir gcf_hello_world && cd $_`      | Crea un directorio para el proyecto y se mueve a él.                                             |
| `nano index.js`                       | Abre el editor de texto para crear el código fuente de la función.                               |
| `nano package.json`                   | Abre el editor de texto para definir las dependencias (ej. `@google-cloud/functions-framework`). |
| `npm install`                         | Descarga las dependencias listadas en `package.json`.                                            |
| `gcloud functions deploy ...`         | El comando principal para desplegar la función en Google Cloud.                                  |
| `gcloud pubsub topics publish ...`    | **Prueba la función** publicando un mensaje en el tema que la activa.                            |
| `gcloud functions logs read ...`      | **Verifica el resultado** leyendo los registros (logs) de la función.                            |

---

## ✅ Resumen de Tareas Realizadas

1. **Preparación del Entorno:** Se activó Cloud Shell y se estableció la región por defecto (`gcloud config set run/region ...`).

2. **Creación del Código Fuente:** Se creó un directorio (`mkdir gcf_hello_world`) y dentro de él se crearon dos archivos usando `nano`:
   
   - **`index.js`:** Contenía el código Node.js. Se usó `functions.cloudEvent('helloPubSub', ...)` para registrar una función que escucha eventos. El código decodifica el mensaje de Pub/Sub (que viene en formato **Base64**) y lo imprime en la consola (`console.log(\`Hello, ${name}!`);`).
   
   - **`package.json`:** Definió la dependencia `@google-cloud/functions-framework`.
   
   - Se ejecutó `npm install` para instalar la dependencia.

3. Despliegue de la Función (Comando Clave):
   
   Se utilizó el siguiente comando para desplegar la función:
   
   Bash
   
   ```
   gcloud functions deploy nodejs-pubsub-function \
    --gen2 \
    --runtime=nodejs20 \
    --region=REGION \
    --source=. \
    --entry-point=helloPubSub \
    --trigger-topic cf-demo \
    --allow-unauthenticated
   ```
   
   **Flags más importantes de este comando:**
   
   - `--gen2`: Especifica el uso de la 2ª generación de Cloud Functions (basada en Cloud Run).
   
   - `--source=.`: Indica que el código fuente está en el directorio actual.
   
   - `--entry-point=helloPubSub`: Le dice a Cloud Functions qué función específica (dentro de `index.js`) debe ejecutar. Debe coincidir con el nombre registrado en el código (`functions.cloudEvent('helloPubSub', ...)`).
   
   - `--trigger-topic cf-demo`: Este es el activador. Le ordena a Google Cloud que cree (o use) un tema de Pub/Sub llamado `cf-demo` y que, automáticamente, invoque esta función cada vez que se publique un mensaje en él.

4. Prueba de la Función:
   
   Como es una función de Pub/Sub, no se prueba con curl. Se prueba publicando un mensaje en el tema cf-demo:
   
   gcloud pubsub topics publish cf-demo --message="Cloud Function Gen2"

5. Verificación de Registros:
   
   Finalmente, se verificó que la función se ejecutó correctamente leyendo sus registros (logs). El resultado esperado era ver el mensaje "Hello, Cloud Function Gen2!".
   
   gcloud functions logs read nodejs-pubsub-function --region=REGION
