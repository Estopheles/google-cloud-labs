# 📄 Documentación del Lab: GSP073 - Cloud Storage: Qwik Start (Consola)

## 🎯 Objetivo del Laboratorio

El objetivo de este laboratorio es aprender los fundamentos de **Google Cloud Storage** utilizando la **Consola de Cloud**. Las tareas cubren el ciclo de vida básico de la gestión de objetos y *buckets*: creación, carga de archivos, configuración de permisos para acceso público y eliminación de recursos.

---

## ✅ Resumen de Tareas Realizadas

### 1. Creación de un Bucket

Se creó un nuevo *bucket* de Cloud Storage con las siguientes características:

- **Nombre:** Se utilizó el ID del Proyecto de Qwiklabs (ej: `student-03-a6a275dcac74@qwiklabs.net`) para asegurar un nombre único a nivel global.

- **Tipo de Ubicación:** Región

- **Ubicación:** `us-east1`

- **Clase de Almacenamiento:** Standard

- **Control de Acceso:** Uniforme

- **Acceso Público:** Se **desmarcó** la opción "Aplicar la prevención de acceso público a este bucket" para permitir que los objetos se hagan públicos manualmente.

### 2. Carga de un Objeto

Se descargó una imagen de muestra (`kitten.png`) y se subió directamente a la raíz del *bucket* recién creado.

### 3. Configuración de Acceso Público

Para hacer que el objeto `kitten.png` fuera accesible públicamente a través de Internet, se modificaron los permisos del *bucket*:

- Se navegó a la pestaña **Permisos**.

- Se hizo clic en **Otorgar Acceso**.

- **Principales nuevas:** Se añadió la principal especial `allUsers`.

- **Rol asignado:** Se seleccionó el rol `Cloud Storage > Visualizador de objetos de Storage` (Storage Object Viewer).

Esto generó una URL pública (ej: `https://storage.googleapis.com/[BUCKET_NAME]/kitten.png`) que permite a cualquier persona ver la imagen.

### 4. Creación de Carpetas

Se demostró la creación de una estructura de "carpetas" anidadas.

- Se creó `folder1` en la raíz del *bucket*.

- Dentro de `folder1`, se creó `folder2`.

- Se subió el archivo `kitten.png` dentro de la subcarpeta `folder1/folder2/`.

### 5. Limpieza de Recursos

Como paso final, se eliminó el *bucket* completo para limpiar todos los recursos utilizados en el lab (incluyendo todos los objetos y carpetas que contenía).

---

## 💡 Conceptos Clave Aprendidos

- **Nomenclatura Global:** Los nombres de los *buckets* de Cloud Storage deben ser **únicos a nivel global**, no solo dentro de un proyecto.

- **Jerarquía Plana (Simulación de Carpetas):** Aunque la consola muestra "carpetas", Cloud Storage en realidad opera con una **estructura plana**. Las carpetas son una simulación visual; el sistema simplemente crea objetos cuyos nombres contienen el carácter `/` (ej. `folder1/folder2/kitten.png`).

- **Control de Acceso (IAM):** El método estándar para hacer un objeto público (con control Uniforme) es asignar el rol `roles/storage.objectViewer` a la principal `allUsers`.

- **Prevención de Acceso Público:** Por defecto, Google Cloud bloquea el acceso público a los *buckets*. Para este lab, fue necesario **desactivar explícitamente** esta medida de seguridad a nivel de *bucket* para poder asignar permisos públicos a los objetos.
