# Mi Bitácora del Laboratorio: Hola, Cloud Run

Este documento resume todos los pasos, comandos y problemas que encontramos durante el laboratorio "Hola, Cloud Run". El objetivo era desplegar una aplicación de Node.js como un contenedor *serverless*.

## Tarea 1. Habilitar API y Configurar el Entorno

Primero, preparamos el proyecto y el entorno de Cloud Shell.

1. **Habilitar la API de Cloud Run:**
   
   ```bash
   gcloud services enable run.googleapis.com
   ```

2. **Configurar la Región:** (En mi caso, usé la región que me asignó el lab)
   
   ```bash
   gcloud config set compute/region "REGION"
   ```

3. **Crear variable de entorno para la región:**
   
   ```bash
   LOCATION="Region"
   ```

![Screenshot From 2025-10-17 14-35-57.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2014-35-57.png)

## Tarea 2. Escribir la Aplicación de Ejemplo

Creamos los archivos base para la aplicación de Node.js.

1. **Crear directorio del proyecto:**
   
   ```bash
   mkdir helloworld && cd helloworld
   ```

2. **Crear `package.json`:** Este archivo define las dependencias del proyecto.
   
   ```bash
   nano package.json
   ```
   
   **Contenido:**
   
   ```json
   {
     "name": "helloworld",
     "description": "Simple hello world sample in Node",
     "version": "1.0.0",
     "main": "index.js",
     "scripts": {
       "start": "node index.js"
     },
     "author": "Google LLC",
     "license": "Apache-2.0",
     "dependencies": {
       "express": "^4.17.1"
     }
   }
   ```

3. ![Screenshot From 2025-10-17 14-38-07.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2014-38-07.png)
   
   **Crear `index.js`:** Este es el código de la aplicación.
   
   ```bash
   nano index.js
   ```
   
   **Contenido Original:**
   
   ```javascript
   const express = require('express');
   const app = express();
   const port = process.env.PORT || 8080;
   
   app.get('/', (req, res) => {
     const name = process.env.NAME || 'World';
     res.send(`Hello ${name}!`);
   });
   
   app.listen(port, () => {
     console.log(`helloworld: listening on port ${port}`);
   });
   ```

## Tarea 3. "Containerizar" y Subir a Artifact Registry

Creamos la "receta" del contenedor (Dockerfile) y lo construimos con Cloud Build.

1. **Crear `Dockerfile`:**
   
   ```bash
   nano Dockerfile
   ```
   
   **Contenido:**
   
   ```dockerfile
   # Use the official lightweight Node.js 12 image.
   # [https://hub.docker.com/_/node](https://hub.docker.com/_/node)
   FROM node:12-slim
   
   # Create and change to the app directory.
   WORKDIR /usr/src/app
   
   # Copy application dependency manifests to the container image.
   COPY package*.json ./
   
   # Install production dependencies.
   RUN npm install --only=production
   
   # Copy local code to the container image.
   COPY . ./
   
   # Run the web service on container startup.
   CMD [ "npm", "start" ]
   ```

2. **Construir el contenedor:**
   
   ```bash
   gcloud builds submit --tag gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld
   ```

![Screenshot From 2025-10-17 14-38-07.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2014-38-07.png)

![Screenshot From 2025-10-17 14-39-58.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2014-39-58.png)

---

## **El Problema: `Error: Cannot find module 'index.js'`**

Aquí es donde nos topamos con el problema principal. Al intentar probar el contenedor localmente, falló.

1. **Intento de ejecución local (fallido):**
   
   ```bash
   docker run -d -p 8080:8080 gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld
   curl localhost:8080
   ```
   
   El `curl` falló.

2. **Diagnóstico:** Ejecutamos el contenedor en modo interactivo para ver los logs.
   
   ```bash
   docker run -p 8080:8080 gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld
   ```

3. **El Error:** Vimos claramente el error: `Error: Cannot find module '/usr/src/app/index.js'`.

4. **Causa Raíz:** El archivo `index.js` **nunca se creó** en el directorio local. La primera compilación (`gcloud builds submit`) se ejecutó sin él, por lo que el contenedor no lo tenía.

5. **Solución (Paso a Paso):**
   
   * **Paso 1:** Creamos el archivo `index.js` que faltaba (con `nano index.js` y el código de la Tarea 2).
   
   * **Paso 2:** Verificamos que los 3 archivos existieran.
     
     ```bash
     ls -l
     ```
   
   * **Paso 3:** Limpiamos los contenedores viejos.
     
     ```bash
     docker rm -f $(docker ps -aq)
     ```
   
   * **Paso 4:** Re-construimos la imagen, esta vez con el `index.js` incluido.
     
     ```bash
     gcloud builds submit --tag gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld
     ```
   
   * **Paso 5:** Forzamos a Docker a descargar la nueva imagen (para evitar usar la versión en caché local).
     
     ```bash
     docker pull gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld
     ```
   
   * **Paso 6:** Ejecutamos el contenedor corregido localmente. ¡Éxito!
     
     ```bash
     docker run -p 8080:8080 gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld
     ```
     
       La terminal mostró: `helloworld: listening on port 8080`
   
   ![Screenshot From 2025-10-17 14-55-22.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2014-55-22.png)

---

## Tarea 4. Implementar en Cloud Run

Con el contenedor corregido y probado, lo desplegamos al público.

1. **Detener el contenedor local:** Presionamos `Ctrl + C` en la terminal.

2. **Desplegar en Cloud Run:**
   
   ```bash
   gcloud run deploy --image gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld --allow-unauthenticated --region=$LOCATION
   ```

3. **Confirmación:** Presionamos `Enter` para aceptar el nombre de servicio `helloworld`.
   
   ![Screenshot From 2025-10-17 15-03-56.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2015-03-56.png)

## Bonus: ¡Personalizando la Página Web!

Decidimos ir un paso más allá y reemplazar el "Hello World" por una página personalizada con animaciones.

1. **Editar `index.js`:** Reemplazamos todo el contenido por este nuevo código que sirve HTML y CSS.
   
   ```bash
   nano index.js
   ```
   
   **Contenido Final (con animaciones):**
   
   ```javascript
   const express = require('express');
   const app = express();
   const port = process.env.PORT || 8080;
   
   // Aquí está todo el HTML, CSS y animaciones en una sola variable
   const htmlPage = `
   <!DOCTYPE html>
   <html>
   <head>
       <title>¡Hola Cloud Run!</title>
       <style>
           /* Importamos una fuente de Google */
           @import url('[https://fonts.googleapis.com/css2?family=Roboto:wght@300;700&display=swap](https://fonts.googleapis.com/css2?family=Roboto:wght@300;700&display=swap)');
   
           body {
               font-family: 'Roboto', sans-serif;
               background-color: #1a1a1a; /* Fondo oscuro */
               color: #f0f0f0;
               display: flex;
               justify-content: center;
               align-items: center;
               height: 100vh;
               margin: 0;
               text-align: center;
               overflow: hidden;
           }
   
           .container {
               /* Animación para que aparezca el contenido */
               animation: fadeIn 2s ease-in-out;
           }
   
           @keyframes fadeIn {
               from { opacity: 0; transform: translateY(20px); }
               to { opacity: 1; transform: translateY(0); }
           }
   
           h1 {
               font-size: 5rem;
               font-weight: 700;
               /* El truco del gradiente animado */
               background: linear-gradient(90deg, #4285F4, #34A853, #FBBC05, #EA4335);
               -webkit-background-clip: text;
               -webkit-text-fill-color: transparent;
               background-size: 400% 400%;
               animation: gradientAnimation 10s ease infinite;
           }
   
           /* Animación que mueve el gradiente */
           @keyframes gradientAnimation {
               0% { background-position: 0% 50%; }
               50% { background-position: 100% 50%; }
               100% { background-position: 0% 50%; }
           }
   
           p {
               font-size: 1.5rem;
               font-weight: 300;
               color: #bdc1c6; /* Un gris claro */
           }
       </style>
   </head>
   <body>
       <div class="container">
           <h1>¡Hola Mundo!</h1>
           <p>Esta es mi app con animaciones en Cloud Run.</p>
       </div>
   </body>
   </html>
   `;
   
   // Cuando alguien visite la ruta raíz "/", enviamos nuestra página HTML
   app.get('/', (req, res) => {
     res.send(htmlPage);
   });
   
   // El servidor escucha en el puerto
   app.listen(port, () => {
     console.log(`helloworld: listening on port ${port}`);
   });
   ```

2. **Re-Construir la Imagen:** (Para incluir el nuevo `index.js`)
   
   ```bash
   gcloud builds submit --tag gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld
   ```

3. **Re-Desplegar el Servicio:** (Para actualizar la versión en vivo)
   
   ```bash
   gcloud run deploy --image gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld --allow-unauthenticated --region=$LOCATION
   ```
   
   ![Screenshot From 2025-10-17 15-05-50.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2015-05-50.png)

## Tarea 5. Limpieza

Finalmente, borramos los recursos para no generar costos.

1. **Borrar la imagen del contenedor:**
   
   ```bash
   gcloud container images delete gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld
   ```
   
   (Confirmamos con `Y`)

2. **Borrar el servicio de Cloud Run:**
   
   ```bash
   gcloud run services delete helloworld --region="REGION"
   ```
   
   (Confirmamos con `Y`)
   
   ![Screenshot From 2025-10-17 15-06-57.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2015-06-57.png)

## Conclusión

Este laboratorio fue un excelente recorrido por todo el flujo de trabajo de DevOps en la nube: desde escribir código, empaquetarlo, depurar un error de compilación, y desplegarlo, hasta actualizarlo con una nueva versión.
