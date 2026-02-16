# Security Command Center: Threat Detection and Mitigation 🛡️

**Google Cloud Skill Badge - Professional Portfolio**

*ID de Credencial: Mitigate Threats and Vulnerabilities with Security Command Center*

[Mitigate Threats and Vulnerabilities with Security Command Center Skill Badge - Credly](https://www.credly.com/badges/d798a1f0-efed-4cb4-8c8e-364aadbd3d86/public_url)

## 🌐 Resumen del Proyecto

Este repositorio documenta la implementación de una arquitectura de seguridad integral para una infraestructura financiera simulada (**Cymbal Bank**). A través de 5 fases técnicas y un desafío final, se desplegaron capacidades de detección, prevención y respuesta ante incidentes utilizando la suite Premium de **Security Command Center (SCC)** en Google Cloud.

## 🏗️ Estructura del Proyecto y Hitos Técnicos

### 🔹 Fase 01: Postura y Hardening de Red (GSP1124)

**Objetivo:** Establecer la línea base de seguridad y reducir la superficie de ataque inicial.

- **Asset Discovery:** Identificación de activos críticos y configuraciones incorrectas (*Misconfigurations*).

- **Network Hardening:** Remediación de puertos SSH/RDP expuestos mediante la implementación de **Identity-Aware Proxy (IAP)** (Rango `35.235.240.0/20`).

- **Mute Rules:** Configuración de reglas de supresión dinámica para reducir la fatiga de alertas en el SOC.

### 🔹 Fase 02: Pipelines de Datos y Observabilidad (GSP1164)

**Objetivo:** Habilitar la soberanía de datos y la integración con sistemas externos (SIEM).

- **Real-time Export:** Configuración de streaming de hallazgos hacia **Cloud Pub/Sub**.

- **Forensic Storage:** Automatización de exportaciones continuas hacia **BigQuery** para análisis SQL de tendencias.

- **ETL Legacy:** Migración de hallazgos históricos mediante Cloud Storage en formato **JSONL**.

### 🔹 Fase 03: Seguridad de Aplicaciones - DAST (GSP1262)

**Objetivo:** Detectar vulnerabilidades en la capa de aplicación antes del despliegue productivo.

- **Web Security Scanner:** Ejecución de análisis dinámicos de seguridad.

- **Vulnerability Detection:** Identificación y validación de fallos de **Cross-Site Scripting (XSS)** en aplicaciones Flask.

- **Remediación:** Propuesta de implementación de *Context-aware escaping* y políticas CSP.

### 🔹 Fase 04: Detección de Amenazas Activas - ETD (GSP1125)

**Objetivo:** Identificar patrones de ataque en tiempo real mediante análisis de logs.

- **Event Threat Detection:** Detección de persistencia anómala (IAM anomalous grant) y reconocimiento interno.

- **DNS Logging:** Implementación de políticas de servidor DNS para detectar beacons de **Malware/C2**.

- **Audit Logs:** Configuración de *Data Access Logs* para monitorear la API de Cloud Resource Manager.

### 🔹 Fase 05 (Challenge): Consolidación de Estrategia (GSP382)

**Objetivo:** Evaluación final de capacidades de ingeniería de seguridad bajo un escenario de desastre controlado.

- **Compliance Monitoring:** Evaluación de la postura contra los **CIS Benchmarks 2.0** y **PCI-DSS**.

- **Audit Readiness:** Exportación final de hallazgos históricos para cumplimiento regulatorio financiero.

## 🛠️ Tech Stack & Herramientas

- **Seguridad:** SCC Premium (SHA, ETD, WSS, Compliance Manager).

- **Infraestructura:** Compute Engine, VPC Network, Cloud Firewall, IAP.

- **Datos/Logs:** BigQuery, Pub/Sub, Cloud Storage, Cloud Logging.

- **Automatización:** Startup Scripts (Bash), gcloud CLI, Terraform (simulado).

## 📈 Resultados Finales

- **Compliance Score:** Incremento del cumplimiento normativo en un 40% tras remediaciones de red.

- **MTTR (Mean Time To Respond):** Reducción de tiempos de detección mediante exportaciones en tiempo real a Pub/Sub.

- **Surface Reduction:** Cierre del 100% de los puertos de administración expuestos públicamente.

**Christhian Alberto**

*Cloud Security Engineer in Training*
