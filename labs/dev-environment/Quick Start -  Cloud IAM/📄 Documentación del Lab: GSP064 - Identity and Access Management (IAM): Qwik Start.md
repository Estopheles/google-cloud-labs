¡Claro que sí! Este laboratorio es fundamental para entender IAM.

Basado en el texto del lab **GSP064**, aquí tienes la documentación que resume los aprendizajes y el flujo de trabajo.

---

# 📄 Documentación del Lab: GSP064 - Identity and Access Management (IAM): Qwik Start

## 🎯 Objetivo del Laboratorio

El objetivo de este laboratorio es experimentar de forma práctica cómo **Cloud IAM** controla el acceso a los recursos de Google Cloud. Se utilizan dos cuentas de usuario (Propietario y Visualizador) para demostrar cómo se otorgan, se prueban y se revocan los permisos, y para comparar los roles **primitivos (básicos)** con los roles **predefinidos (granulares)**.

---

## 👥 Roles Clave del Laboratorio

Este lab es único porque se utilizan dos identidades para simular un escenario real de gestión de permisos:

- **`Username 1` (Propietario):** Tiene el rol primitivo `Propietario` (Owner). Esta cuenta tiene control total sobre el proyecto, incluyendo la capacidad de crear recursos y gestionar los roles IAM de otros usuarios.

- **`Username 2` (Visualizador):** Comienza con el rol primitivo `Visualizador` (Viewer). Esta cuenta solo puede ver recursos (acceso de solo lectura) y no puede modificar nada ni gestionar permisos.

---

## ✅ Resumen de Tareas Realizadas

El laboratorio sigue una "historia" en la que se modifican los permisos de `Username 2` y se observa el resultado.

### 1. Exploración de Permisos (Propietario vs. Visualizador)

- **`Username 1 (Propietario)`:** Pudo navegar a la consola de **IAM y Administración** y vio el botón `+ OTORGAR ACCESO` habilitado. Pudo ver y modificar los permisos de todos los usuarios.

- **`Username 2 (Visualizador)`:** Pudo navegar a la consola de IAM, pero el botón `+ OTORGAR ACCESO` estaba **deshabilitado**. No podía realizar ningún cambio en los permisos.

### 2. Creación de Recursos y Prueba de Acceso de "Visualizador"

- **`Username 1 (Propietario)`:** Creó un *bucket* de Cloud Storage y subió un archivo (`sample.txt`).

- **`Username 2 (Visualizador)`:** Navegó a Cloud Storage y pudo **ver exitosamente** el *bucket* y el archivo `sample.txt`, confirmando sus permisos de solo lectura a nivel de proyecto.

### 3. Revocación de Acceso de "Visualizador"

- **`Username 1 (Propietario)`:** Regresó a la consola de IAM, editó los permisos de `Username 2` y **eliminó** el rol de `Visualizador`.

- **`Username 2 (Visualizador)`:** Al actualizar la página de Cloud Storage (después de un breve tiempo de propagación), recibió un **error de permisos**. Su acceso al proyecto fue completamente revocado.

### 4. Asignación de un Rol Granular (Predefinido)

- **`Username 1 (Propietario)`:** Volvió a otorgar acceso a `Username 2`, pero esta vez no usó un rol primitivo. Le asignó el rol predefinido y mucho más específico: **`Cloud Storage > Visualizador de objetos de Storage`**.

- **`Username 2 (Visualizador)`:**
  
  - **Consola de Cloud:** Al intentar ver la lista de *buckets* en la consola de Cloud Storage, seguía obteniendo un error. Esto se debe a que el rol `Visualizador de objetos de Storage` no incluye el permiso `storage.buckets.list` (permiso para ver *todos* los buckets del proyecto).
  
  - **Cloud Shell (CLI):** Sin embargo, al usar Cloud Shell y ejecutar un comando `gsutil` que especificaba el nombre exacto del *bucket* (`gsutil ls gs://[YOUR_BUCKET_NAME]`), el comando **funcionó** y pudo ver el archivo `sample.txt`.

---

## 💡 Conceptos Clave Aprendidos

- **Roles Primitivos (Básicos):** Son roles muy amplios (`Propietario`, `Editor`, `Visualizador`) que se aplican a **todos los servicios** dentro de un proyecto. Son fáciles de asignar, pero no siguen el principio de menor privilegio.

- **Roles Predefinidos (Granulares):** Son roles específicos de un servicio (como `roles/storage.objectViewer`) que otorgan un conjunto de permisos definidos por Google. Este es el método recomendado para seguir el **principio de menor privilegio**.

- **Diferencia entre Consola y CLI:** Este lab demuestra perfectamente que la Consola de Cloud a menudo requiere permisos más amplios (como permisos de `list`) para poder mostrar la interfaz gráfica. En cambio, la CLI (Cloud Shell) permite realizar acciones muy específicas (como listar el contenido de un *bucket* cuyo nombre ya se conoce) con permisos mucho más restringidos.

- **Propagación de IAM:** Los cambios en IAM (otorgar o revocar permisos) no siempre son instantáneos y pueden tardar unos segundos (hasta ~80 segundos, según el lab) en propagarse por el sistema.
