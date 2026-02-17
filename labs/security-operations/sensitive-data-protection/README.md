# 🛡️ Google Cloud Sensitive Data Protection (SDP) & Privacy Engineering

Este repositorio documenta prácticas avanzadas de **Ingeniería de Privacidad** y **Seguridad de Datos** en Google Cloud Platform. El objetivo principal es implementar estrategias de **DLP (Data Loss Prevention)** para descubrir, clasificar y proteger información sensible (PII, PHI, PCI) en entornos de nube híbrida y moderna.

A través de estos laboratorios, se simulan escenarios reales de cumplimiento normativo (GDPR, PCI-DSS) protegiendo datos en reposo (Storage, BigQuery) y datos en tránsito hacia modelos de Inteligencia Artificial.

---

## 🛠️ Tech Stack & Herramientas
* **Google Cloud Sensitive Data Protection (antes DLP API)**
* **Discovery Service:** Perfilado automático de datos.
* **Inspection & De-identification Templates:** Reglas de enmascaramiento y tokenización.
* **Cloud Storage & BigQuery:** Protección de Data Lakes y Data Warehouses.
* **Generative AI Security:** Sanitización de prompts y respuestas de LLMs.
* **Security Command Center (SCC):** Centralización de hallazgos de vulnerabilidades.

---

## 📂 Contenido del Curso

### 1. [Lab] Descubrimiento y Protección en Cloud Storage
**Enfoque:** Seguridad en Datos No Estructurados.
* **Implementación:** Configuración de un perfilado continuo (Discovery Scan) para detectar automáticamente cuando se suben archivos con datos sensibles (tarjetas de crédito, SSN) a buckets de almacenamiento.
* **Técnica Clave:** Creación de **Plantillas de Desidentificación** para generar copias "sanitizadas" de los archivos originales, permitiendo su uso en entornos de desarrollo sin exponer datos reales.
* **Skills:** `Data Discovery`, `Automated Masking`, `Audit Logs`.

### 2. [Lab] Descubrimiento de Datos Sensibles en BigQuery
**Enfoque:** Seguridad en Data Warehousing y Analytics.
* **Implementación:** Escaneo de tablas masivas en BigQuery para identificar columnas de alto riesgo.
* **Técnica Clave:** Uso de **Data Profiles** para visualizar métricas de riesgo y sensibilidad a nivel de columna y tabla, integrando los resultados con Security Command Center para la gestión de posturas de seguridad.
* **Skills:** `BigQuery Security`, `Risk Analysis`, `Data Governance`.

### 3. [Lab] Protección de Datos en IA Generativa
**Enfoque:** AI Security (Securing LLMs).
* **Implementación:** Intercepción de llamadas a modelos de IA Generativa para inspeccionar tanto el *prompt* del usuario como la *respuesta* del modelo.
* **Técnica Clave:** Configuración de la API de DLP para censurar datos sensibles en tiempo real antes de que lleguen al modelo (evitando el entrenamiento con datos privados) y antes de que se muestren al usuario.
* **Skills:** `AI/ML Security`, `Prompt Injection Mitigation`, `Real-time Inspection`.

### 4. [Challenge] Desafío de Ecosistema SDP
**Enfoque:** Validación de Habilidades (Capstone).
* **Objetivo:** Configurar una solución integral sin guías paso a paso.
* **Tareas:**
    1.  Crear y lanzar trabajos de inspección para datasets heredados.
    2.  Diseñar plantillas de desidentificación personalizadas (Reemplazo y Enmascaramiento).
    3.  Asegurar pipelines de datos mediante la ocultación de PII antes del análisis.
* **Skills:** `Troubleshooting`, `End-to-End Implementation`.

---

## 🚀 Valor Profesional (Why this matters)
La implementación de Sensitive Data Protection es crítica para organizaciones reguladas (Fintech, Salud, Banca). Este proyecto demuestra la capacidad para:
1.  **Reducir la superficie de ataque** minimizando la exposición de datos sensibles.
2.  **Automatizar el cumplimiento** (Compliance as Code) mediante escaneos programados.
3.  **Habilitar la innovación segura**, permitiendo a los equipos de datos y de IA trabajar con información real pero anonimizada.

---
*Este proyecto fue realizado como parte de la certificación profesional y entrenamiento práctico en Google Cloud Platform.*