# 📄 Documentación del Lab: Cloud Storage: Qwik Start (CLI)

## 🎯 Objetivo del Laboratorio

El objetivo de este laboratorio es aprender a interactuar con **Google Cloud Storage** utilizando la **línea de comandos (Cloud Shell)**. Se cubren las operaciones fundamentales de creación de *buckets*, carga y gestión de objetos, y la configuración de permisos de acceso público usando los comandos `gcloud storage` y `gsutil`.

---

## 🛠️ Comandos Clave Utilizados

Este laboratorio introduce dos conjuntos de comandos para interactuar con Cloud Storage:

- **`gcloud storage`**: Es la herramienta más moderna y recomendada, parte del SDK principal de `gcloud`.

- **`gsutil`**: Es la herramienta "clásica", que aún es necesaria para tareas específicas como la gestión de Listas de Control de Acceso (ACLs).

| **Comando**                                   | **Propósito en el Lab**                                           |
| --------------------------------------------- | ----------------------------------------------------------------- |
| `gcloud storage buckets create gs://...`      | Creación de un nuevo *bucket*.                                    |
| `gcloud storage cp [LOCAL_FILE] gs://...`     | Subir un archivo desde Cloud Shell al *bucket*.                   |
| `gcloud storage cp -r gs://... [DEST]`        | Descargar un objeto del *bucket* a Cloud Shell.                   |
| `gcloud storage cp gs://... gs://.../folder/` | Copiar un objeto para simular la creación de una "carpeta".       |
| `gcloud storage ls gs://...`                  | Listar el contenido de un *bucket* o "carpeta".                   |
| `gcloud storage ls -l gs://...`               | Listar el contenido con detalles (tamaño, fecha).                 |
| `gcloud storage rm gs://...`                  | Eliminar un objeto del *bucket*.                                  |
| `curl [URL] --output [FILE]`                  | Descargar un archivo de internet a Cloud Shell.                   |
| `gsutil acl ch -u AllUsers:R gs://...`        | **Hacer un objeto público** (Conceder rol "Reader" a "AllUsers"). |
| `gsutil acl ch -d AllUsers gs://...`          | **Quitar acceso público** (Eliminar la entrada de "AllUsers").    |

---

## ✅ Resumen de Tareas Realizadas

1. **Configuración:** Se activó **Cloud Shell** y se configuró la región por defecto con `gcloud config set compute/region "REGION"`.

2. **Creación de un Bucket:** Se utilizó `gcloud storage buckets create` para crear un nuevo *bucket*. Se usó el ID del proyecto para garantizar un nombre único.
   
   - `gcloud storage buckets create gs://[PROJECT_ID]`

3. **Carga de un Objeto:** Se descargó una imagen (`ada.jpg`) desde una URL pública a la instancia de Cloud Shell usando `curl`. Luego, se subió esa imagen al *bucket* con `gcloud storage cp`.
   
   - `curl https://.../Ada_Lovelace_portrait.jpg --output ada.jpg`
   
   - `gcloud storage cp ada.jpg gs://[BUCKET_NAME]`

4. **Creación de "Carpetas":** Se simuló la creación de una carpeta (`image-folder`) copiando el archivo `ada.jpg` a una nueva ruta de objeto que contenía un `/`.
   
   - `gcloud storage cp gs://[BUCKET_NAME]/ada.jpg gs://[BUCKET_NAME]/image-folder/`

5. **Gestión de Acceso Público (ACLs):**
   
   - **Conceder Acceso:** Se utilizó `gsutil` (no `gcloud storage`) para modificar la Lista de Control de Acceso (ACL) del objeto `ada.jpg`, dándole permisos de lectura (`:R`) al grupo `AllUsers`.
     
     - `gsutil acl ch -u AllUsers:R gs://[BUCKET_NAME]/ada.jpg`
   
   - **Revocar Acceso:** Se volvió a usar `gsutil` para eliminar (`-d`) la entrada de `AllUsers` de la ACL, haciendo que el objeto volviera a ser privado.
     
     - `gsutil acl ch -d AllUsers gs://[BUCKET_NAME]/ada.jpg`

6. **Limpieza de Recursos:** Finalmente, se eliminó el objeto `ada.jpg` de la raíz del *bucket* (dejando la copia en `image-folder/`) usando el comando `rm`.
   
   - `gcloud storage rm gs://[BUCKET_NAME]/ada.jpg`

---

## 💡 Conceptos Clave Aprendidos

- **`gcloud storage` vs. `gsutil`:** Este lab demuestra que, aunque `gcloud storage` es el conjunto de comandos principal y moderno para la mayoría de las operaciones (crear, copiar, listar, eliminar), la herramienta `gsutil` sigue siendo indispensable para la gestión de permisos detallados a nivel de objeto, como las **ACLs**.

- **Jerarquía Plana (CLI):** El concepto de "carpetas" simuladas es muy evidente desde la CLI. Al copiar `ada.jpg` a `image-folder/`, simplemente se creó un nuevo objeto con el nombre `image-folder/ada.jpg`. No existe una entidad de "carpeta" real.

- **Permisos de Objeto (ACLs):** A diferencia del lab de la consola (donde se usó IAM a nivel de *bucket*), este lab se enfoca en las **ACLs** a nivel de objeto. El comando `gsutil acl ch -u AllUsers:R` es el método clásico y directo para hacer público un solo archivo sin cambiar la política de todo el *bucket*.
