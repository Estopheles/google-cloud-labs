# 🚀 Google Cloud Platform - Laboratorios Prácticos

![GCP](https://img.shields.io/badge/Google_Cloud-4285F4?style=for-the-badge&logo=google-cloud&logoColor=white)
![Status](https://img.shields.io/badge/status-active-success?style=for-the-badge)
![Labs](https://img.shields.io/badge/labs_completados-44+-blue?style=for-the-badge)
![Last Update](https://img.shields.io/badge/última_actualización-diciembre_2025-orange?style=for-the-badge)
![GitHub stars](https://img.shields.io/github/stars/christhianrodriguez/gcp-labs-practicas?style=for-the-badge)
![GitHub forks](https://img.shields.io/github/forks/christhianrodriguez/gcp-labs-practicas?style=for-the-badge)

> Repositorio de documentación técnica de laboratorios hands-on para la preparación de **Google Cloud Certified Cloud Engineer**. Incluye soluciones a problemas reales, troubleshooting, comparaciones con AWS y capturas de pantalla del proceso completo.

---

## 📋 Tabla de Contenidos

- [Sobre este Proyecto](#-sobre-este-proyecto)
- [Certificación](#-certificación)
- [Prerrequisitos](#-prerrequisitos)
- [Estructura del Repositorio](#-estructura-del-repositorio)
- [Laboratorios Completados](#-laboratorios-completados)
  - [Networking & Compute](#1-networking--compute)
  - [Serverless & Containers](#2-serverless--containers)
  - [Storage & Databases](#3-storage--databases)
  - [Load Balancing](#4-load-balancing)
  - [DevOps & Monitoring](#5-devops--monitoring)
  - [Messaging](#6-messaging)
  - [Security & IAM](#7-security--iam)
  - [Kubernetes & GKE](#8-kubernetes--gke)
  - [Infrastructure as Code (Terraform)](#9-infrastructure-as-code-terraform)
  - [Data & Analytics](#10-data--analytics)
  - [Marketplace](#11-marketplace)
- [Tecnologías y Servicios](#️-tecnologías-y-servicios)
- [Comparación GCP vs AWS](#-comparación-gcp-vs-aws)
- [Cómo Usar este Repositorio](#-cómo-usar-este-repositorio)
- [Contribuciones](#-contribuciones)
- [Licencia](#-licencia)
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

## 🎓 Certificación

![Google Cloud Certified](https://img.shields.io/badge/Google_Cloud-Associate_Cloud_Engineer-4285F4?style=for-the-badge&logo=google-cloud&logoColor=white)
![Valid Until](https://img.shields.io/badge/Válido_Hasta-Febrero_2026-success?style=for-the-badge)

**Associate Cloud Engineer** - Google Cloud Platform  
**Fecha de Certificación**: Febrero 2024  
**Validez**: Hasta Febrero 2026  
**Credential ID**: Ver [certificado](certificado/)

Esta certificación valida habilidades en:
- Configuración de entornos de soluciones en la nube
- Planificación y configuración de soluciones en la nube
- Implementación de soluciones en la nube
- Garantía del funcionamiento exitoso de soluciones en la nube
- Configuración de acceso y seguridad

---

## 📋 Prerrequisitos

- **Cuenta de Google Cloud Platform** (nivel gratuito disponible)
- **Conocimientos básicos** de cloud computing
- **Familiaridad con línea de comandos** (opcional pero recomendado)
- **Navegador web** actualizado para acceder a la consola de GCP

---

## 📁 Estructura del Repositorio

```
gcp-labs-practicas/
├── certificado/                                       # Certificación Associate Cloud Engineer
├── labs/
│   ├── networking/                                    # Redes VPC, firewalls, conectividad
│   ├── cloud-run/                                     # Despliegues serverless
│   ├── compute-sql-storage/                           # Arquitecturas de 3 capas
│   ├── marketplace/                                   # Soluciones preconfiguradas
│   ├── load-balancing/                                # L4 y L7 load balancers
│   ├── dev-environment/                               # Cloud Functions, Pub/Sub, IAM, Monitoring
│   ├── security-operations/                           # Security Command Center, threat detection
│   │   ├── security-basics/                           # IAM, KMS, VPC Peering, IAP, GKE
│   │   └── scc-threat-mitigation/                     # Security Command Center labs
│   ├── develop-network/                               # GKE, BigQuery, SQL
│   ├── Terraform/                                     # Infrastructure as Code
│   └── docs/                                          # Documentación y PDFs de referencia
├── images/                                            # Screenshots y diagramas
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

#### 📦 [Cloud Storage: Qwik Start (Consola)](labs/dev-environment/Qwik%20Start%20-%20Bucket/📄%20Documentación%20del%20Lab:%20GSP073%20-%20Cloud%20Storage:%20Qwik%20Start%20(Consola).md)

**Lab ID**: GSP073  
**Servicios**: `Cloud Storage`

#### 💻 [Cloud Storage: Qwik Start (CLI/SDK)](labs/dev-environment/Quick%20Start%20-%20%20CLI_SDK/📄%20Documentación%20del%20Lab:%20Cloud%20Storage:%20Qwik%20Start%20(CLI).md)

**Lab ID**: GSP074  
**Servicios**: `Cloud Storage` • `gcloud CLI`

---

### 4. Load Balancing

#### ⚖️ [Network Load Balancer (L4)](labs/load-balancing/network-load-balancer/Configuración%20de%20un%20Balanceador%20de%20Cargas%20de%20Red%20(GSP007)%20en%20Google%20Cloud.md)

**Lab ID**: GSP007  
**Nivel**: Intermediate  
**Tipo**: Layer 4 (Transporte)

**Servicios**: `Load Balancing` • `Compute Engine` • `Health Checks`

#### 🌐 [Application Load Balancer (L7)](labs/load-balancing/application-load-balancer/Configuración%20de%20un%20Balanceador%20de%20Cargas%20de%20Aplicaciones%20(GSP155).md)

**Lab ID**: GSP155  
**Nivel**: Intermediate  
**Tipo**: Layer 7 (Aplicación)

**Servicios**: `HTTP(S) Load Balancing` • `Backend Services` • `URL Maps`

#### 🔒 [Internal Application Load Balancer](labs/load-balancing/internal-application-load-balancer/Proyecto%20de%20Portafolio:%20Lab%20GSP041%20-%20Configuración%20de%20un%20Balanceador%20de%20Cargas%20de%20Aplicaciones%20Interno.md)

**Lab ID**: GSP041  
**Nivel**: Advanced  
**Tipo**: Internal L7

**Servicios**: `Internal Load Balancing` • `Private VPC`

#### 🏆 [Challenge Lab: Implementación L4 y L7](labs/load-balancing/challenge-l4-l7/Implementación%20de%20Balanceo%20de%20Cargas%20(L4%20y%20L7).md)

**Lab ID**: GSP313  
**Nivel**: Advanced  
**Tipo**: Desafío sin instrucciones

---

### 5. DevOps & Monitoring

#### 📊 [Cloud Monitoring: Qwik Start](labs/dev-environment/Cloud%20Monitoring:%20Qwik%20Start%0A/📄%20Documentación%20del%20Lab:%20GSP089%20-%20Cloud%20Monitoring:%20Qwik%20Start.md)

**Lab ID**: GSP089  
**Servicios**: `Cloud Monitoring` • `Metrics` • `Alerting`

#### ⚡ [Cloud Run Functions: Qwik Start (Consola)](labs/dev-environment/Cloud%20Run%20Functions:%20Quick%20Start/📄%20Documentación%20del%20Lab:%20GSP081%20-%20Cloud%20Run%20Functions:%20Qwik%20Start%20(Consola).md)

**Lab ID**: GSP081  
**Servicios**: `Cloud Functions` • `Event-driven Architecture`

#### 🖥️ [Cloud Run Functions: Qwik Start (CLI)](labs/dev-environment/Cloud%20Run%20Functions:%20Qwik%20Start%20-%20Línea%20de%20comandos/CloudRun.md)

**Servicios**: `Cloud Functions` • `gcloud CLI`

#### 🏆 [Lab de Desafío GSP315](labs/dev-environment/Desafio%20-%20lab/Lab%20de%20Desafío%20GSP315.md)

**Lab ID**: GSP315  
**Nivel**: Expert

---

### 6. Messaging

#### 📮 [Pub/Sub: Qwik Start (Consola)](labs/dev-environment/Pub_Sub:%20Qwik%20Start%20-%20Consola/QuickStart-Pup_Sub.md)

**Servicios**: `Pub/Sub` • `Topics` • `Subscriptions`

#### 💻 [Pub/Sub: Qwik Start (CLI)](labs/dev-environment/Pub_Sub:%20Qwik%20Start%20-%20Línea%20de%20comandos/LineaDeComandos.md)

**Servicios**: `Pub/Sub` • `gcloud CLI`

#### 🐍 [Pub/Sub: Qwik Start (Python)](labs/dev-environment/Pub_Sub:%20Qwik%20Start%20(Python)/Python.md)

**Servicios**: `Pub/Sub` • `Python Client Library`

---

### 7. Security & IAM

#### 🔐 [Identity and Access Management (IAM): Qwik Start](labs/dev-environment/Quick%20Start%20-%20%20Cloud%20IAM/📄%20Documentación%20del%20Lab:%20GSP064%20-%20Identity%20and%20Access%20Management%20(IAM):%20Qwik%20Start.md)

**Lab ID**: GSP064  
**Servicios**: `Cloud IAM` • `Roles` • `Permissions`

#### 🛡️ [Identity-Aware Proxy (IAP): Protege Máquinas Virtuales](labs/secure-network-creation/Protege%20máquinas%20virtuales%20con%20Chrome%20Enterprise%20Premium/Google%20Cloud:%20Identity-Aware%20Proxy%20(IAP).md)

**Duración**: ~60 minutos  
**Nivel**: Intermediate

**Lo que aprenderás**:

- Configurar Identity-Aware Proxy para proteger recursos
- Controlar acceso a VMs sin VPN
- Implementar autenticación basada en identidad
- Troubleshooting de permisos IAP

**Servicios**: `Identity-Aware Proxy` • `Cloud IAM` • `Compute Engine`

#### 🔐 [Service Accounts y Roles](labs/security-operations/security-basics/Aspectos%20principales%20de%20las%20cuentas%20de%20servicio%20y%20los%20roles/Implementación%20Segura%20de%20Identidades%20de%20Máquina%20en%20Google%20Cloud.md)

**Nivel**: Intermediate | **Duración**: ~45 min

**Lo que aprenderás**:
- Crear y gestionar Service Accounts
- Aplicar principio de menor privilegio
- Autenticación máquina-a-máquina

**Servicios**: `Service Accounts` • `IAM Roles` • `BigQuery`

#### 🎨 [Roles Personalizados de IAM](labs/security-operations/security-basics/Roles%20personalizados%20de%20IAM/Roles%20personalizados%20de%20IAM.md)

**Nivel**: Advanced | **Duración**: ~40 min

**Servicios**: `Custom IAM Roles` • `Permissions`

#### 🔒 [Cloud KMS](labs/security-operations/security-basics/Empieza%20a%20usar%20Cloud%20KMS/EmpiezaA_usar_Cloud_KMS.md)

**Nivel**: Intermediate | **Duración**: ~35 min

**Servicios**: `Cloud KMS` • `Encryption`

#### 🌐 [VPC Peering](labs/security-operations/security-basics/Intercambio%20de%20tráfico%20entre%20redes%20de%20VPC/Reporte%20de%20Laboratorio:%20Intercambio%20de%20Tráfico%20entre%20Redes%20VPC%20(VPC%20Peering).md)

**Nivel**: Intermediate | **Duración**: ~50 min

**Servicios**: `VPC Peering` • `Routing`

#### 🔐 [Autenticación con IAP](labs/security-operations/security-basics/Autenticación%20de%20Usuarios%20con%20Identity-Aware%20Proxy%20(IAP)/Autenticación%20de%20Usuarios%20con%20Identity-Aware%20Proxy.md)

**Nivel**: Advanced | **Duración**: ~60 min

**Servicios**: `Identity-Aware Proxy` • `OAuth`

#### 🛡️ [Cloud Armor](labs/security-operations/secure-network-creation/Balanceador%20de%20cargas%20de%20aplicaciones%20con%20Cloud%20Armor/Balanceador%20de%20cargas%20de%20aplicaciones%20con%20Cloud%20Armor.md)

**Nivel**: Advanced | **Duración**: ~55 min

**Servicios**: `Cloud Armor` • `DDoS Protection`

#### 🏆 [Challenge: Arquitectura Segura GSP322](labs/security-operations/secure-network-creation/Lab%20de%20desafío_GSP322/Arquitectura%20de%20Red%20Segura%20y%20Modelo%20Zero%20Trust%20en%20Google%20Cloud.md)

**Lab ID**: GSP322 | **Nivel**: Expert

**Servicios**: `Zero Trust` • `VPC` • `IAP`

#### 🐛 [Security Command Center](labs/security-operations/scc-threat-mitigation/)

**Nivel**: Advanced | **Labs**: 5 (Setup, Vulnerabilities, Web Scanning, Threat Detection, Challenge)

**Servicios**: `Security Command Center` • `Threat Detection`

---

### 8. Kubernetes & GKE

#### ☸️ [Administración de Deployments en GKE](labs/develop-network/Cómo%20administrar%20implementaciones%20con%20Kubernetes%20Engine/Administración%20de%20Implementaciones%20con%20Google%20Kubernetes%20Engine.md)

**Nivel**: Intermediate | **Duración**: ~60 min

**Lo que aprenderás**:
- Crear y gestionar deployments en GKE
- Rolling updates y rollbacks
- Scaling de aplicaciones

**Servicios**: `GKE` • `Kubernetes` • `Deployments`

#### 🔒 [Private GKE Cluster](labs/security-operations/security-basics/Cómo%20configurar%20un%20clúster%20de%20Kubernetes%20privado/Cómo_configurar_un_clúster_de_Kubernetes_privado.md)

**Nivel**: Advanced | **Duración**: ~55 min

**Lo que aprenderás**:
- Private nodes y master endpoint
- Network policies
- Pod security

**Servicios**: `GKE` • `Private Cluster` • `Network Policies`

#### 🏆 [Challenge: Secure GKE](labs/security-operations/security-basics/Desafio:%20Implementación%20de%20Infraestructura%20Segura%20en%20Google%20Kubernetes%20Engine/Reporte%20Técnico:%20Implementación%20de%20Infraestructura%20Segura%20en%20Google%20Kubernetes%20Engine.md)

**Nivel**: Expert | **Duración**: ~90 min

**Servicios**: `GKE` • `RBAC` • `Workload Identity`

#### 🏆 [Challenge: Desarrolla tu Red](labs/develop-network/Desarrolla%20tu%20red%20de%20Google%20Cloud:%20Lab%20de%20desafío/Desarrolla%20tu%20red%20de%20Google%20Cloud:%20Lab%20de%20desafío.md)

**Nivel**: Expert | **Duración**: ~75 min

**Servicios**: `VPC` • `Load Balancing` • `Firewall`

---

### 9. Infrastructure as Code (Terraform)

#### 🏗️ [Módulos de Terraform](labs/Terraform/Cómo%20interactuar%20con%20los%20módulos%20de%20Terraform/GSP751.md)

**Lab ID**: GSP751 | **Nivel**: Intermediate

**Servicios**: `Terraform` • `IaC` • `Modules`

#### 📦 [Estado de Terraform](labs/Terraform/Administra%20el%20estado%20de%20Terraform/AdministraelestadodeTerraform.md)

**Nivel**: Advanced | **Duración**: ~45 min

**Servicios**: `Terraform` • `State Management`

#### 🏆 [Challenge: Terraform](labs/Terraform/Lab%20de%20desafio/LabDesafio.md)

**Nivel**: Expert | **Duración**: ~60 min

**Servicios**: `Terraform` • `IaC`

---

### 10. Data & Analytics

#### 📊 [BigQuery and Cloud SQL](labs/develop-network/Introduction%20to%20SQL%20for%20BigQuery%20and%20Cloud%20SQL/BigQueryLabs.md)

**Nivel**: Intermediate | **Duración**: ~60 min

**Servicios**: `BigQuery` • `Cloud SQL` • `SQL`

---

### 11. Marketplace

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
   - [Cloud Storage Qwik Start](labs/dev-environment/Qwik%20Start%20-%20Bucket/)
   - [Cloud IAM Basics](labs/dev-environment/Quick%20Start%20-%20%20Cloud%20IAM/)

2. **Avanza a servicios intermedios**:
   
   - [Cloud Run](labs/cloud-run/)
   - [Arquitectura 3 capas](labs/compute-sql-storage/)
   - [Network Load Balancer](labs/load-balancing/network-load-balancer/)

3. **Desafíate con labs avanzados**:
   
   - [Internal Load Balancer](labs/load-balancing/internal-application-load-balancer/)
   - [Challenge Labs](labs/load-balancing/challenge-l4-l7/)

### Para quienes vienen de AWS

- Revisa las secciones de **"Comparación con AWS"** en cada lab
- Consulta la [tabla de equivalencias](#-comparación-gcp-vs-aws) arriba
- Los labs incluyen analogías con servicios de AWS

### Para Troubleshooting

- Cada lab documenta **errores reales** encontrados y sus soluciones
- Busca en los archivos `.md` palabras como "Problema", "Error", "Solución"

---

## 🤝 Contribuciones

¿Encontraste un error o tienes una mejora? ¡Tu contribución es bienvenida!

- 🐛 **Reportar errores**: Abre un [Issue](../../issues)
- 💡 **Sugerir mejoras**: Abre un [Issue](../../issues) con tu propuesta
- 🔧 **Enviar correcciones**: Envía un [Pull Request](../../pulls)
- ⭐ **Apoyar el proyecto**: Dale una estrella si te resulta útil

### Guías para contribuir:
1. Fork el repositorio
2. Crea una rama para tu feature (`git checkout -b feature/nueva-funcionalidad`)
3. Commit tus cambios (`git commit -am 'Agregar nueva funcionalidad'`)
4. Push a la rama (`git push origin feature/nueva-funcionalidad`)
5. Abre un Pull Request

---

## 📄 Licencia

Este proyecto está bajo la **Licencia MIT** - ver el archivo [LICENSE](LICENSE) para más detalles.

### Resumen de la licencia:
- ✅ Uso comercial permitido
- ✅ Modificación permitida
- ✅ Distribución permitida
- ✅ Uso privado permitido
- ❗ Incluir aviso de copyright
- ❗ Incluir texto de licencia

---

## 📧 Contacto

**Christhian Rodriguez**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/christhianrodriguez)
[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/christhianrodriguez)

---

## 📝 Notas

- ✅ **Todos los labs fueron completados exitosamente**
- 📸 **Incluye capturas de pantalla del proceso completo**
- 🐛 **Documenta problemas reales y soluciones**
- 🔄 **Comparaciones con AWS cuando es relevante**
- 📅 **Período de realización**: Octubre - Diciembre 2025

---

> 💡 **Tip**: Este repositorio se actualiza continuamente. Dale ⭐ para seguir el progreso.

**Última actualización**: Diciembre 2025
