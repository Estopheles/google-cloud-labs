# 📄 Documentación del Lab: GSP089 - Cloud Monitoring: Qwik Start

## 🎯 Objetivo del Laboratorio

El objetivo de este laboratorio es aprender a configurar y utilizar **Cloud Monitoring** y **Cloud Logging** para supervisar una instancia de Compute Engine. Esto incluye la instalación del agente de observabilidad, la creación de chequeos de disponibilidad (uptime checks), la configuración de políticas de alertas y la visualización de métricas y registros en *dashboards* personalizados.

---

## ✅ Resumen de Tareas Realizadas

### 1. Preparación de la Instancia (VM)

- Se creó una instancia de Compute Engine llamada **`lamp-1-vm`** (tipo `e2-medium`, SO Debian 12).

- Se habilitó el tráfico **HTTP** a través de las reglas de firewall de la VM.

- Se accedió a la instancia vía SSH y se instaló un servidor web Apache2 (`sudo apt-get install apache2`).

### 2. Instalación del Agente de Operaciones (Ops Agent)

Esta es la parte central del lab. Para recopilar métricas detalladas (como tráfico de red) y registros (logs) del sistema operativo de la VM, se instaló el **Agente de Operaciones de Google Cloud**.

- Se descargó el script de instalación: `curl -sSO https://dl.google.com/cloudagents/add-google-cloud-ops-agent-repo.sh`

- Se ejecutó el script para instalar el agente (que combina las funciones de Monitoring y Logging): `sudo bash add-google-cloud-ops-agent-repo.sh --also-install`

### 3. Creación de un Chequeo de Disponibilidad (Uptime Check)

Para monitorear la VM desde *fuera* y asegurar que el servidor web Apache estuviera respondiendo, se configuró un *Uptime Check*.

- **Nombre:** `Lamp Uptime Check`

- **Protocolo:** HTTP

- **Recurso:** Instancia `lamp-1-vm`

- **Frecuencia:** 1 minuto

- Se verificó con el botón **Probar** que la conexión era exitosa.

### 4. Creación de una Política de Alertas (Alerting Policy)

Para recibir notificaciones proactivas sobre el estado de la VM, se creó una política de alertas.

- **Nombre:** `Inbound Traffic Alert`

- **Métrica:** Se usó una métrica recopilada por el *Ops Agent*: `Network traffic` (`agent.googleapis.com/interface/traffic`).

- **Condición:** Se configuró para dispararse si el tráfico superaba los **500 B/s** (`Por encima del umbral`).

- **Canal de Notificación:** Se creó un nuevo canal de tipo **Email** y se asoció a la política de alertas.

### 5. Creación de un Dashboard Personalizado

Para visualizar las métricas clave de la VM en un solo lugar, se creó un *dashboard* personalizado.

- **Nombre:** `Cloud Monitoring LAMP Qwik Start Dashboard`

- **Widget 1 (Gráfico de Línea):** "CPU Load", mostrando la métrica `CPU load (1m)`.

- **Widget 2 (Gráfico de Línea):** "Received packets", mostrando la métrica `Received packets`.

### 6. Verificación de Logs y Pruebas

Finalmente, se probó la integración de los servicios.

- Se utilizó el **Explorador de Registros (Log Explorer)** para filtrar y ver los registros provenientes exclusivamente de la instancia `lamp-1-vm`.

- Se **detuvo** (`Stop`) la instancia de VM desde la consola de Compute Engine.

- Se observó en el **Log Explorer** cómo aparecían los nuevos registros correspondientes a la detención de la VM.

- Se observó en **Cloud Monitoring** cómo el `Lamp Uptime Check` comenzó a fallar (marcas rojas).

- Se **inició** (`Start`) la instancia nuevamente y se vio cómo los registros y el *Uptime Check* volvían a la normalidad.

- Se verificó la bandeja de entrada del correo electrónico para confirmar la recepción de las notificaciones de alerta.

---

## 💡 Conceptos Clave Aprendidos

- **Google Cloud Ops Agent:** Es el componente fundamental que se instala *dentro* de la VM. Es el agente unificado que recopila tanto **métricas** (para Cloud Monitoring) como **registros** (para Cloud Logging) y los envía a la plataforma de Google Cloud.

- **Métricas de Agente vs. Métricas de Hipervisor:** El lab utiliza métricas de ambos tipos. `CPU load (1m)` puede ser vista por el hipervisor, pero métricas detalladas como `Network traffic` (`agent.googleapis.com...`) solo están disponibles gracias al **Ops Agent** instalado.

- **Cloud Monitoring: Tres Pilares:**
  
  1. **Dashboards:** Para la visualización pasiva y personalizada de métricas.
  
  2. **Uptime Checks:** Para el monitoreo externo (caja negra) de la disponibilidad de un servicio (ej. un servidor web).
  
  3. **Alerting:** Para la notificación proactiva cuando una métrica cruza un umbral definido.

- **Integración de Logging y Monitoring:** Los servicios están fuertemente integrados. Un evento (como detener una VM) genera **registros (logs)** que se pueden consultar en el Log Explorer y, al mismo tiempo, provoca un cambio en las **métricas** (como el Uptime Check) que puede disparar alertas.
