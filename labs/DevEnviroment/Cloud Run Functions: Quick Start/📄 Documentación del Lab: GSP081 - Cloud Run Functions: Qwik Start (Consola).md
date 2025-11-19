# 📄 Documentación del Lab: GSP081 - Cloud Run Functions: Qwik Start (Consola)

## 🎯 Objetivo del Laboratorio

El objetivo de este laboratorio es aprender el flujo de trabajo básico para crear, desplegar y probar una **Función de Cloud Run (Cloud Run Function)** utilizando la **Consola de Cloud** y su editor de código integrado. Este lab se enfoca en crear una función simple que responde a un evento HTTP.

---

## ✅ Resumen de Tareas Realizadas

### 1. Habilitación de APIs

- Al ser la primera vez que se utiliza el servicio en el proyecto, la consola solicitó y se procedió a **habilitar** las APIs necesarias (como la API de Cloud Run y Cloud Build).

### 2. Creación y Configuración de la Función

Se navegó a **Cloud Run** y se seleccionó `ESCRIBIR UNA FUNCIÓN` para crear un nuevo servicio con la siguiente configuración:

- **Nombre del servicio:** `gcfunction`

- **Región:** Se seleccionó la región asignada por el lab.

- **Autenticación:** Se eligió **`Permitir el acceso público`** para que la función pudiera ser invocada a través de Internet sin credenciales.

- **Entorno de ejecución:** Se especificó **`Segunda generación`** (Gen 2).

- **Escalamiento:** Se limitó la `Cantidad máxima de instancias` a **5**.

### 3. Implementación del Código (Editor Directo)

- Se utilizó el **Editor Directo** (inline editor) proporcionado en la consola.

- Se dejó el código de muestra `helloHttp` (Node.js) que venía por defecto en el archivo `index.js`. Este código está diseñado para leer un mensaje desde un cuerpo JSON (`request.body.message`) y responder con él.

- Se hizo clic en **`GUARDAR Y VOLVER A IMPLEMENTAR`** para compilar e implementar la función.

### 4. Prueba de la Función

La función se probó directamente desde la consola de Cloud Run:

- Se navegó a la pestaña **`PRUEBA`**.

- En el campo **Evento de activación (JSON)**, se ingresó el siguiente *payload*:
  
  JSON
  
  ```
  {
    "message": "Hello World!"
  }
  ```

- Al ejecutar la prueba, se confirmó que la función respondió correctamente con el texto "Hello World!".

### 5. Visualización de Registros (Logs)

- Para verificar la ejecución, se navegó a la pestaña **`Observabilidad`** y se seleccionó **`Registros`**.

- En el explorador de registros (Log Explorer), se pudieron observar los *logs* generados por la función, confirmando su inicio y finalización exitosa.

---

## 💡 Conceptos Clave Aprendidos

- **Cloud Run Functions (Serverless):** Es un servicio de "cómputo sin servidor" (*serverless*). Google Cloud gestiona toda la infraestructura subyacente, y el servicio solo se ejecuta (y se cobra) cuando es invocado por un evento.

- **Eventos y Activadores (Triggers):** Las funciones se ejecutan en respuesta a "eventos". En este lab, el activador fue una **solicitud HTTP**, que es el tipo de activador más común (como lo indica la pregunta de opción múltiple del lab).

- **Entornos de Ejecución (Gen 1 vs. Gen 2):** El lab especifica el uso de la **Segunda Generación (Gen 2)**, que se basa en Cloud Run (mientras que la Gen 1 era una plataforma más antigua). Esto proporciona un mejor rendimiento y más flexibilidad.

- **Editor Directo (Inline Editor):** Para funciones simples y prototipos, es posible escribir, editar y desplegar el código directamente desde la consola de Google Cloud, sin necesidad de configurar un entorno de desarrollo local.

- **Observabilidad Integrada:** Los registros (logs) de todas las ejecuciones de la función se envían automáticamente a **Cloud Logging** y son accesibles a través de la pestaña `Observabilidad`.
