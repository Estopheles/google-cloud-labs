# Lab de Desafío GSP315: Mi Documentación y Aprendizaje

## 🎯 ¿Qué Construí?

En este desafío, configuré un **pipeline de procesamiento de imágenes totalmente sin servidor (serverless)**.

El objetivo era que cada vez que un usuario subiera una imagen a un *bucket* de Cloud Storage, el sistema automáticamente creara una versión en miniatura (thumbnail) de esa imagen y la guardara en el mismo *bucket*. Además, el sistema debía notificar a través de Pub/Sub que el trabajo estaba hecho.

El flujo final fue este:

1. **Usuario** ➔ Sube `imagen.jpg` al **Bucket de Cloud Storage**.

2. **Cloud Storage** ➔ Emite un evento que **activa (trigger)** la...

3. **Cloud Run Function** ➔ (Esta lee `imagen.jpg`, la procesa y...)

4. **Cloud Run Function** ➔ Guarda `imagen_64x64_thumbnail.jpg` en el **Bucket**.

5. **Cloud Run Function** ➔ Publica un mensaje ("¡Terminé!") en el **Tema de Pub/Sub**.

<!--

Aquí puedes poner una captura de tu Bucket de Cloud Storage (como la que tomaste al final)

donde se vea la imagen original Y la miniatura generada.

Ej: 2025-11-17 23.39.39 console.cloud.google.com 941ab02f95ac.png (modificada para mostrar ambas imágenes)

-->

## 🚀 ¿Cómo lo Logré? (El Proceso y la Depuración)

A diferencia de un Qwik Start, aquí no había instrucciones, solo objetivos. Este fue mi proceso:

### 1. La Infraestructura Base (Tareas 1 y 2)

Primero, creé los "contenedores" que mi aplicación necesitaría:

- **Cloud Storage:** Creé el *bucket* (`qwiklabs-gcp-02-246628995177-bucket`) para almacenar las imágenes.

- **Pub/Sub:** Creé el *tema* (`topic-memories-281`) para que la función publicara sus notificaciones.

<!--

Aquí va la captura de la creación del Bucket:

"2025-11-17 23.38.33 console.cloud.google.com f9f9831ad2e0.png"

-->

<!--

Y aquí la captura de la creación del Tema de Pub/Sub:

"2025-11-17 23.38.49 console.cloud.google.com 62ade57b38e7.png"

-->

### 2. El Cerebro: La Cloud Run Function (Tarea 3)

Aquí es donde estuvo el verdadero desafío. El proceso fue:

1. Crear una nueva **Cloud Run Function** (Gen 2).

2. Pegar el código de `index.js` y `package.json` que me proporcionó el lab.

3. **¡Aquí falló!** El primer despliegue dio un error: `Container failed to start...`

### 3. La Depuración: ¡Las Trampas del Desafío!

El error `Container failed to start...` fue la pista clave. Después de investigar, descubrí **dos trampas** que había que resolver:

#### Trampa 1: El código `index.js` estaba incompleto.

El código que te dan tiene dos líneas vacías que **debes rellenar** manualmente:

- **La línea `const topicName = "";`:** Estaba vacía. Tuve que editarla para que apuntara a mi tema de Pub/Sub.
  
  - **Antes:** `const topicName = "";`
  
  - **Después:** `const topicName = "topic-memories-281";`

- **La línea `functions.cloudEvent('', ...);`:** También estaba vacía. Esta define el nombre de la función que se debe ejecutar. Tuve que poner el "Punto de entrada" (Entry Point) que me pedían las instrucciones.
  
  - **Antes:** `functions.cloudEvent('', async cloudEvent => {`
  
  - **Después:** `functions.cloudEvent('memories-thumbnail-maker', async cloudEvent => {`

#### Trampa 2: El "Punto de Entrada" (Entry Point) no estaba configurado.

Este fue el error clave. El código `index.js` no es un servidor web, es una **función de evento**.

- **El Problema:** Cloud Run intentaba iniciar un servidor web (porque es su modo por defecto), pero como mi código no tenía uno, el contenedor fallaba al iniciarse.

- **La Solución:** En la configuración de Cloud Run, tuve que especificar el **"Punto de entrada" (Function entry point)** como `memories-thumbnail-maker`. Esto le dice a Cloud Run: "No intentes iniciar un servidor web; en su lugar, simplemente carga esta función llamada `memories-thumbnail-maker` de mi código y tenla lista".

<!--

¡Esta es la captura clave! Muestra el código corregido y el Punto de Entrada configurado:

"2025-11-17 23.39.12 console.cloud.google.com 303f3fc044d9.png"

-->

#### (Trampa Opcional) El Activador (Trigger)

El error `Container failed to start...` también puede ocurrir si dejas el activador como HTTP (el predeterminado). La solución es establecer el "Punto de entrada" (como hice) y asegurarse de que el **Activador (Trigger)** esté configurado para **Eventarc** (escuchando a Cloud Storage), no para HTTP.

### 4. La Prueba Final

Después de corregir el `index.js` y el `Punto de entrada`, desplegué la función. Para probarla:

1. Subí la imagen `car_sunset...jpg` al *bucket*.

2. Esperé unos 30 segundos.

3. Refresqué la página del *bucket* y ¡ahí estaba! `car_sunset..._64x64_thumbnail.jpg`.

¡El pipeline funcionó!

## 🧠 ¿Qué Aprendí?

- **Arquitectura Orientada a Eventos:** Aprendí a conectar servicios de forma desacoplada. Cloud Storage no sabe nada de Cloud Run, y Cloud Run no sabe quién subió la imagen. Simplemente reaccionan a **eventos**.

- **"Serverless" no es magia:** "Sin servidor" significa que no gestiono VMs, pero la *configuración* es crucial. El error `Container failed to start...` es un síntoma clásico de una configuración incorrecta.

- **Depuración de Cloud Run:** Aprendí que ese error no significa que el *código* esté mal, sino que el *contrato* entre Cloud Run y mi código está roto (puerto incorrecto, tipo de servicio incorrecto o, en mi caso, un **Punto de Entrada** incorrecto).

- **El código de los labs a veces es una trampa:** Los campos vacíos (`topicName = ""`) están ahí a propósito para forzarte a leer y entender el código que estás pegando, no solo a copiarlo a ciegas.

## 💡 ¿Para Qué Sirve Este Tipo de Sistema?

Este patrón (Storage ➔ Función ➔ Storage) es increíblemente poderoso y común en el mundo real. Se usa para cualquier tarea automatizada que deba ocurrir cuando llega un archivo:

- **Generar miniaturas (thumbnails)** (¡Este lab!)

- **Convertir archivos:** Cambiar el formato de videos (de `.mov` a `.mp4`).

- **Analizar contenido:** Usar IA para extraer texto (OCR) de PDFs o imágenes subidas.

- **Seguridad:** Ejecutar un análisis de virus en cada archivo nuevo.

- **Notificaciones:** Avisar a un equipo en Slack (vía Pub/Sub) cada vez que un cliente sube un documento importante.
