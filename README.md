# 🚀 Google Cloud Platform - Laboratorios Prácticos

![GCP](https://img.shields.io/badge/Google_Cloud-4285F4?style=for-the-badge&logo=google-cloud&logoColor=white)
![Status](https://img.shields.io/badge/status-active-success?style=for-the-badge)
![Labs](https://img.shields.io/badge/labs_completados-19-blue?style=for-the-badge)
![Last Update](https://img.shields.io/badge/última_actualización-noviembre_2024-orange?style=for-the-badge)

> Repositorio de documentación técnica de laboratorios hands-on para la preparación de **Google Cloud Certified Cloud Engineer**. Incluye soluciones a problemas reales, troubleshooting, comparaciones con AWS y capturas de pantalla del proceso completo.

---

## 📋 Tabla de Contenidos

- [Sobre este Proyecto](#-sobre-este-proyecto)
- [Estructura del Repositorio](#-estructura-del-repositorio)
- [Laboratorios Completados](#-laboratorios-completados)
  - [Networking & Compute](#1-networking--compute)
  - [Serverless & Containers](#2-serverless--containers)
  - [Storage & Databases](#3-storage--databases)
  - [Load Balancing](#4-load-balancing)
  - [DevOps & Monitoring](#5-devops--monitoring)
  - [Messaging](#6-messaging)
  - [Security & IAM](#7-security--iam)
- [Tecnologías y Servicios](#️-tecnologías-y-servicios)
- [Comparación GCP vs AWS](#-comparación-gcp-vs-aws)
- [Cómo Usar este Repositorio](#-cómo-usar-este-repositorio)
- [Contacto](#-contacto)

---

## 🎯 Sobre este Proyecto

Este repositorio documenta mi viaje de aprendizaje en **Google Cloud Platform** como parte de mi preparación para la certificación **Cloud Engineer**. Cada laboratorio incluye:

- ✅ **Documentación detallada** paso a paso
- 🐛 **Troubleshooting real** de errores encontrados durante la práctica
- 📸 **Capturas de pantalla** de cada proceso
- 🔄 **Comparaciones con AWS** para contexto multi-cloud
- 💡 **Aprendizajes y best practices**

**Objetivo**: Crear una referencia técnica práctica y realista que ayude a otros en su camino de aprendizaje en GCP.

---

## 📁 Estructura del Repositorio

```
gcp-labs-practicas/
├── labs/
│   ├── networking/              # Redes VPC, firewalls, conectividad
│   ├── cloud-run/               # Despliegues serverless
│   ├── compute-sql-storage/     # Arquitecturas de 3 capas
│   ├── marketplace/             # Soluciones preconfiguradas
│   ├── Load Balancing/          # L4 y L7 load balancers
│   └── DevEnviroment/           # Cloud Functions, Pub/Sub, IAM, Monitoring
├── images/                      # Screenshots y diagramas
└── README.md
```

---

## 🧪 Laboratorios Completados

### 1. Networking & Compute

#### 🌐 [Introducción a VPC y Compute Engine](labs/networking/mi-aventura-google-cloud-redes-vpc-vms.md)

**Lab ID**: Fundamentos de redes  
**Duración**: ~45 minutos  
**Nivel**: Beginner

**Lo que aprenderás**:

- Crear y eliminar redes VPC personalizadas
- Configurar reglas de firewall
- Conectividad entre VMs en diferentes regiones
- Troubleshooting de conectividad de red

**Servicios**: `Compute Engine` • `VPC` • `Firewall Rules`

---

### 2. Serverless & Containers

#### 🐳 [Hello Cloud Run - Despliegue de Contenedores Serverless](labs/cloud-run/mi-bitacora-laboratorio-hola-cloud-run.md)

**Lab ID**: Cloud Run Basics  
**Duración**: ~40 minutos  
**Nivel**: Beginner

**Lo que aprenderás**:

- Containerizar aplicaciones Node.js
- Construir imágenes con Cloud Build
- Desplegar en Cloud Run
- **Resolución de error**: `Cannot find module 'index.js'`

**Servicios**: `Cloud Run` • `Cloud Build` • `Artifact Registry`

---

### 3. Storage & Databases

#### 🗄️ [Arquitectura de 3 Capas: Compute + SQL + Storage](labs/compute-sql-storage/mi-experiencia-practica-compute-engine-cloud-sql-storage-gcp.md)

**Lab ID**: 3-Tier Architecture  
**Duración**: ~60 minutos  
**Nivel**: Intermediate

**Lo que aprenderás**:

- Integrar Compute Engine con Cloud SQL
- Configurar Cloud Storage buckets
- Conectividad entre servicios
- Arquitectura web completa

**Servicios**: `Compute Engine` • `Cloud SQL` • `Cloud Storage`

#### 📦 [Cloud Storage: Qwik Start (Consola)](labs/DevEnviroment/Qwik%20Start%20-%20Bucket/📄%20Documentación%20del%20Lab:%20GSP073%20-%20Cloud%20Storage:%20Qwik%20Start%20(Consola).md)

**Lab ID**: GSP073  
**Servicios**: `Cloud Storage`

#### 💻 [Cloud Storage: Qwik Start (CLI/SDK)](labs/DevEnviroment/Quick%20Start%20-%20%20CLI_SDK/📄%20Documentación%20del%20Lab:%20Cloud%20Storage:%20Qwik%20Start%20(CLI).md)

**Lab ID**: GSP074  
**Servicios**: `Cloud Storage` • `gcloud CLI`

---

### 4. Load Balancing

#### ⚖️ [Network Load Balancer (L4)](labs/Load%20Balancing%20/network-load-balancer/Configuración%20de%20un%20Balanceador%20de%20Cargas%20de%20Red%20(GSP007)%20en%20Google%20Cloud.md)

**Lab ID**: GSP007  
**Nivel**: Intermediate  
**Tipo**: Layer 4 (Transporte)

**Servicios**: `Load Balancing` • `Compute Engine` • `Health Checks`

#### 🌐 [Application Load Balancer (L7)](labs/Load%20Balancing%20/application-load-balancer/Configuración%20de%20un%20Balanceador%20de%20Cargas%20de%20Aplicaciones%20(GSP155).md)

**Lab ID**: GSP155  
**Nivel**: Intermediate  
**Tipo**: Layer 7 (Aplicación)

**Servicios**: `HTTP(S) Load Balancing` • `Backend Services` • `URL Maps`

#### 🔒 [Internal Application Load Balancer](labs/Load%20Balancing%20/internal-application-load-balancer/Proyecto%20de%20Portafolio:%20Lab%20GSP041%20-%20Configuración%20de%20un%20Balanceador%20de%20Cargas%20de%20Aplicaciones%20Interno.md)

**Lab ID**: GSP041  
**Nivel**: Advanced  
**Tipo**: Internal L7

**Servicios**: `Internal Load Balancing` • `Private VPC`

#### 🏆 [Challenge Lab: Implementación L4 y L7](labs/Load%20Balancing%20/challenge-l4-l7/Implementación%20de%20Balanceo%20de%20Cargas%20(L4%20y%20L7).md)

**Lab ID**: GSP313  
**Nivel**: Advanced  
**Tipo**: Desafío sin instrucciones

---

### 5. DevOps & Monitoring

#### 📊 [Cloud Monitoring: Qwik Start](labs/DevEnviroment/Cloud%20Monitoring:%20Qwik%20Start%0A/📄%20Documentación%20del%20Lab:%20GSP089%20-%20Cloud%20Monitoring:%20Qwik%20Start.md)

**Lab ID**: GSP089  
**Servicios**: `Cloud Monitoring` • `Metrics` • `Alerting`

#### ⚡ [Cloud Run Functions: Qwik Start (Consola)](labs/DevEnviroment/Cloud%20Run%20Functions:%20Quick%20Start/📄%20Documentación%20del%20Lab:%20GSP081%20-%20Cloud%20Run%20Functions:%20Qwik%20Start%20(Consola).md)

**Lab ID**: GSP081  
**Servicios**: `Cloud Functions` • `Event-driven Architecture`

#### 🖥️ [Cloud Run Functions: Qwik Start (CLI)](labs/DevEnviroment/Cloud%20Run%20Functions:%20Qwik%20Start%20-%20Línea%20de%20comandos/CloudRun.md)

**Servicios**: `Cloud Functions` • `gcloud CLI`

#### 🏆 [Lab de Desafío GSP315](labs/DevEnviroment/Desafio%20-%20lab/Lab%20de%20Desafío%20GSP315.md)

**Lab ID**: GSP315  
**Nivel**: Expert

---

### 6. Messaging

#### 📮 [Pub/Sub: Qwik Start (Consola)](labs/DevEnviroment/Pub_Sub:%20Qwik%20Start%20-%20Consola/QuickStart-Pup_Sub.md)

**Servicios**: `Pub/Sub` • `Topics` • `Subscriptions`

#### 💻 [Pub/Sub: Qwik Start (CLI)](labs/DevEnviroment/Pub_Sub:%20Qwik%20Start%20-%20Línea%20de%20comandos/LineaDeComandos.md)

**Servicios**: `Pub/Sub` • `gcloud CLI`

#### 🐍 [Pub/Sub: Qwik Start (Python)](labs/DevEnviroment/Pub_Sub:%20Qwik%20Start%20(Python)/Python.md)

**Servicios**: `Pub/Sub` • `Python Client Library`

---

### 7. Security & IAM

#### 🔐 [Identity and Access Management (IAM): Qwik Start](labs/DevEnviroment/Quick%20Start%20-%20%20Cloud%20IAM/📄%20Documentación%20del%20Lab:%20GSP064%20-%20Identity%20and%20Access%20Management%20(IAM):%20Qwik%20Start.md)

**Lab ID**: GSP064  
**Servicios**: `Cloud IAM` • `Roles` • `Permissions`

---

### 8. Marketplace

#### 🛒 [Primeros Pasos con Google Cloud Marketplace](labs/marketplace/mi-informe-laboratorio-primeros-pasos-google-cloud-marketplace.md)

**Duración**: ~20 minutos  
**Nivel**: Beginner

**Lo que aprenderás**:

- Desplegar soluciones preconfiguradas
- Stack LAMP con un click
- Comparación con AWS Marketplace

**Servicios**: `Cloud Marketplace` • `Click to Deploy`

---

## 🛠️ Tecnologías y Servicios

### Compute

- **Compute Engine**: Máquinas virtuales escalables
- **Cloud Run**: Contenedores serverless completamente administrados
- **Cloud Functions**: Funciones serverless event-driven

### Networking

- **VPC**: Redes virtuales privadas globales
- **Cloud Load Balancing**: Balanceadores L4 y L7
- **Firewall Rules**: Seguridad de red

### Storage & Databases

- **Cloud Storage**: Almacenamiento de objetos
- **Cloud SQL**: Bases de datos relacionales administradas

### DevOps

- **Cloud Build**: CI/CD para contenedores
- **Artifact Registry**: Registry de contenedores
- **Cloud Monitoring**: Observabilidad y alertas

### Messaging & Integration

- **Pub/Sub**: Mensajería asíncrona

### Security

- **Cloud IAM**: Identity and Access Management

---

## 🔄 Comparación GCP vs AWS

| Servicio GCP        | Servicio AWS | Función                     | Diferencias Clave                                                     |
| ------------------- | ------------ | --------------------------- | --------------------------------------------------------------------- |
| **Compute Engine**  | EC2          | Máquinas virtuales          | GCP: facturación por segundo; AWS: por hora (instancias bajo demanda) |
| **Cloud Run**       | Fargate      | Contenedores serverless     | Cloud Run: escala a cero; Fargate: mínimo 1 tarea                     |
| **Cloud Functions** | Lambda       | Funciones serverless        | Similares, diferentes triggers y runtimes                             |
| **Cloud SQL**       | RDS          | Bases de datos relacionales | GCP: integración nativa con VPC; AWS: más motores disponibles         |
| **Cloud Storage**   | S3           | Almacenamiento de objetos   | S3: más clases de almacenamiento; GCP: más simple                     |
| **VPC**             | VPC          | Redes virtuales             | GCP: VPC es global; AWS: VPC por región                               |
| **Load Balancing**  | ELB/ALB/NLB  | Balanceadores de carga      | GCP: un solo balanceador puede ser global                             |
| **Cloud Build**     | CodeBuild    | CI/CD                       | Similares, diferentes integraciones                                   |
| **Pub/Sub**         | SNS/SQS      | Mensajería                  | Pub/Sub: ambos patrones en uno; AWS: servicios separados              |
| **Cloud IAM**       | IAM          | Gestión de identidades      | Modelos similares, sintaxis diferente                                 |
| **Marketplace**     | Marketplace  | Soluciones preconfiguradas  | Funcionalidad equivalente                                             |

---

## 📖 Cómo Usar este Repositorio

### Para Principiantes en GCP

1. **Comienza con los fundamentos**:
   
   - [VPC y Compute Engine](labs/networking/mi-aventura-google-cloud-redes-vpc-vms.md)
   - [Cloud Storage Qwik Start](labs/DevEnviroment/Qwik%20Start%20-%20Bucket/)
   - [Cloud IAM Basics](labs/DevEnviroment/Quick%20Start%20-%20%20Cloud%20IAM/)

2. **Avanza a servicios intermedios**:
   
   - [Cloud Run](labs/cloud-run/)
   - [Arquitectura 3 capas](labs/compute-sql-storage/)
   - [Network Load Balancer](labs/Load%20Balancing%20/network-load-balancer/)

3. **Desafíate con labs avanzados**:
   
   - [Internal Load Balancer](labs/Load%20Balancing%20/internal-application-load-balancer/)
   - [Challenge Labs](labs/Load%20Balancing%20/challenge-l4-l7/)

### Para quienes vienen de AWS

- Revisa las secciones de **"Comparación con AWS"** en cada lab
- Consulta la [tabla de equivalencias](#-comparación-gcp-vs-aws) arriba
- Los labs incluyen analogías con servicios de AWS

### Para Troubleshooting

- Cada lab documenta **errores reales** encontrados y sus soluciones
- Busca en los archivos `.md` palabras como "Problema", "Error", "Solución"

---

## 📧 Contacto

**Christhian Rodriguez**

[](https://www.linkedin.com/in/christhianrodriguez/)
[](https://github.com/christhianrodriguez)

---

## 📝 Notas

- ✅ **Todos los labs fueron completados exitosamente**
- 📸 **Incluye capturas de pantalla del proceso completo**
- 🐛 **Documenta problemas reales y soluciones**
- 🔄 **Comparaciones con AWS cuando es relevante**
- 📅 **Período de realización**: Octubre - Noviembre 2024

---

> 💡 **Tip**: Este repositorio se actualiza continuamente. Dale ⭐ para seguir el progreso.

**Última actualización**: Noviembre 2025
