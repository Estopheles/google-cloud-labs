# Reporte Técnico: Implementación Segura de Identidades de Máquina en Google Cloud

Laboratorio: Service Accounts and Roles: Fundamentals (GSP199)

Fecha: 26 de Noviembre, 2025

Plataforma: Google Cloud Platform (GCP)

Enfoque: Gestión de Identidades y Accesos (IAM) / Seguridad en la Nube

## 1. Resumen Ejecutivo

El objetivo de este laboratorio fue diseñar e implementar una arquitectura de **autenticación de máquina a máquina** segura. Se configuró una instancia de cómputo (VM) para acceder a un almacén de datos (BigQuery) utilizando una **Cuenta de Servicio (Service Account)** en lugar de credenciales de usuario o claves API estáticas. Esto demuestra la aplicación de mejores prácticas de seguridad para evitar la fuga de credenciales y gestionar el ciclo de vida de las identidades no humanas.

## 2. Evidencia de Implementación

### Fase 1: Gestión de Identidades vía CLI

Se utilizó `gcloud CLI` para automatizar la creación de identidades, demostrando capacidades de *Infraestructura como Código*.

- **Acción:** Creación de la Service Account `my-sa-123` y asignación de roles (IAM Binding).

- **Importancia:** La automatización reduce el error humano en la asignación de permisos.

![2025-11-26 22.10.27 console.cloud.google.com 7690b169054c.png](Fotos/22cf2081116c0546c78a9bcc848a58483b176253.png)

> **Evidencia 1:** Ejecución de comandos `gcloud projects add-iam-policy-binding` para asociar roles a la identidad creada.

### Fase 2: Auditoría de Identidades en Consola

Verificación visual de las cuentas de servicio activas en el proyecto para asegurar que no existan cuentas huérfanas o no autorizadas.

- **Acción:** Revisión del panel de IAM y Administración.

- **Observación:** Se identificaron cuentas por defecto (Compute Engine default) y cuentas dedicadas (`bigquery-qwiklab`).

![b47aff543f1781a59825874b7abc4097f3c52811.png](Fotos/3c95f9ab872ea3a2d8a177d518068c199444317a.png)

> **Evidencia 2:** Panel de control mostrando las identidades gestionadas y sus ID únicos de correo electrónico.

### Fase 3: Validación de Acceso (Prueba de Concepto)

Ejecución de un script en Python dentro de la VM para consultar datos de natalidad en BigQuery.

- **Resultado:** El script se autenticó exitosamente utilizando la identidad de la VM (sin logueo manual) y extrajo los datos solicitados.

- **Datos:** Tabla de `year` vs `num_babies`.

![Screenshot From 2025-11-26 22-43-33.png](Fotos/57c08604c5690995bfc814e8c6c6e22f0da06f97.png)

> **Evidencia 3:** Output exitoso de la consulta SQL ejecutada desde Python, confirmando el flujo de autorización correcto.

## 3. Análisis de Ciberseguridad

### A. Eliminación de Credenciales de Larga Duración

En un entorno inseguro tradicional, los desarrolladores suelen hardcodear claves (ej. `API_KEY="12345"`) en el código fuente.

- **Solución implementada:** Al usar Service Accounts adjuntas a la VM, Google gestiona y rota las claves criptográficas automáticamente. El código Python utiliza `google.auth.compute_engine.Credentials()` para solicitar un token temporal de corta duración.

- **Beneficio:** Si el código fuente es robado, el atacante no obtiene credenciales válidas persistentes.

### B. Principio de Menor Privilegio (Least Privilege)

Durante el laboratorio, nos enfrentamos a un error de autorización (HTTP 403 Forbidden).

- **Incidente:** La cuenta tenía el rol `BigQuery Data Viewer` (solo lectura), pero el script intentaba crear un "Job" de consulta.

- **Resolución:** Se elevó el privilegio específicamente al rol `BigQuery User`.

- **Lección:** No otorgamos el rol `Owner` o `Editor` (que dan control total). Solo dimos el permiso exacto necesario para ejecutar la tarea. Esto minimiza el "radio de explosión" si la cuenta es comprometida.

### C. Identidad como Perímetro

La seguridad no se basó únicamente en firewalls de red (IPs), sino en la **Identidad**. La base de datos (BigQuery) no está expuesta a "todo internet", sino que solo responde a peticiones autenticadas y autorizadas de una identidad específica (`bigquery-qwiklab`).

## 4. Resolución de Problemas (Troubleshooting)

Durante la implementación, se diagnosticaron y resolvieron dos incidentes críticos:

1. **Error de Identidad (404 Not Found):**
   
   - *Causa:* La VM se desplegó con la cuenta de servicio predeterminada en lugar de la cuenta dedicada segura.
   
   - *Corrección:* Se detuvo la instancia y se reconfiguró la identidad asociada.

2. **Error de Autorización (403 Forbidden):**
   
   - *Causa:* Falta del permiso `bigquery.jobs.create`.
   
   - *Corrección:* Actualización de políticas IAM para agregar el rol necesario.

## 5. Conclusión y Aprendizaje

Este laboratorio reforzó la importancia de desacoplar las identidades humanas de las identidades de servicio. Aprendí a:

1. Crear y auditar Service Accounts.

2. Diagnosticar errores de IAM (diferencia entre autenticación y autorización).

3. Implementar accesos seguros a APIs de Google Cloud sin comprometer secretos en el código.

Herramientas: Google Cloud Platform, Python, Linux, Bash.
