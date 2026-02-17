# 🚀 Google Cloud Platform - Hands-on Labs

<!-- Certification Badge -->
![GCP Certified](https://img.shields.io/badge/GCP-Associate_Cloud_Engineer-4285F4?style=for-the-badge&logo=google-cloud&logoColor=white)
![Valid Until](https://img.shields.io/badge/Valid_Until-Jan_2029-success?style=for-the-badge)

<!-- Google Cloud Skill Badges -->
![Terraform](https://img.shields.io/badge/Skill_Badge-Terraform_Infrastructure-7B42BC?style=for-the-badge&logo=terraform&logoColor=white)
![Network Development](https://img.shields.io/badge/Skill_Badge-Network_Development-4285F4?style=for-the-badge&logo=google-cloud&logoColor=white)
![Secure Network](https://img.shields.io/badge/Skill_Badge-Secure_Network-00B4D8?style=for-the-badge&logo=google-cloud&logoColor=white)
![Security Fundamentals](https://img.shields.io/badge/Skill_Badge-Security_Fundamentals-00B4D8?style=for-the-badge&logo=google-cloud&logoColor=white)
![Load Balancing](https://img.shields.io/badge/Skill_Badge-Load_Balancing-4285F4?style=for-the-badge&logo=google-cloud&logoColor=white)
![App Dev Environment](https://img.shields.io/badge/Skill_Badge-App_Dev_Environment-4285F4?style=for-the-badge&logo=google-cloud&logoColor=white)
![Security Command Center](https://img.shields.io/badge/Skill_Badge-Security_Command_Center-EA4335?style=for-the-badge&logo=google-cloud&logoColor=white)

<!-- Additional Certification -->
![Blue Team](https://img.shields.io/badge/Security_Blue_Team-Junior_Analyst-0066CC?style=for-the-badge&logo=security&logoColor=white)

<!-- Repository Stats -->
![Status](https://img.shields.io/badge/status-active-success?style=for-the-badge)
![Labs](https://img.shields.io/badge/labs_completed-44+-blue?style=for-the-badge)
![Last Update](https://img.shields.io/badge/last_update-february_2026-orange?style=for-the-badge)
![GitHub stars](https://img.shields.io/github/stars/christhianrodriguez/gcp-labs-practicas?style=for-the-badge)
![GitHub forks](https://img.shields.io/github/forks/christhianrodriguez/gcp-labs-practicas?style=for-the-badge)

> Technical documentation repository of hands-on labs for **Google Cloud Certified Cloud Engineer** preparation. Includes real-world problem solutions, troubleshooting, AWS comparisons, and complete process screenshots.

---

## 📋 Table of Contents

- [About This Project](#-about-this-project)
- [Certification](#-certification)
- [Prerequisites](#-prerequisites)
- [Repository Structure](#-repository-structure)
- [Completed Labs](#-completed-labs)
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
- [Technologies & Services](#️-technologies--services)
- [GCP vs AWS Comparison](#-gcp-vs-aws-comparison)
- [How to Use This Repository](#-how-to-use-this-repository)
- [Contributions](#-contributions)
- [License](#-license)
- [Contact](#-contact)

---

## 🎯 About This Project

This repository documents my learning journey in **Google Cloud Platform** as part of my preparation for the **Cloud Engineer** certification. Each lab includes:

- ✅ **Detailed step-by-step documentation**
- 🐛 **Real troubleshooting** of errors encountered during practice
- 📸 **Screenshots** of each process
- 🔄 **AWS comparisons** for multi-cloud context
- 💡 **Learnings and best practices**

**Goal**: Create a practical and realistic technical reference to help others in their GCP learning journey.

---

## 🎓 Certification

![Google Cloud Certified](https://img.shields.io/badge/Google_Cloud-Associate_Cloud_Engineer-4285F4?style=for-the-badge&logo=google-cloud&logoColor=white)
![Valid Until](https://img.shields.io/badge/Valid_Until-January_2029-success?style=for-the-badge)

**Associate Cloud Engineer** - Google Cloud Platform  
**Certification Date**: January 2026  
**Valid Until**: January 2029  
**Credential ID**: See [certificate](certificado/)

This certification validates skills in:
- Setting up cloud solution environments
- Planning and configuring cloud solutions
- Deploying cloud solutions
- Ensuring successful operation of cloud solutions
- Configuring access and security

### 🏅 Google Cloud Skill Badges

1. **Mitigate Threats and Vulnerabilities with Security Command Center** (Feb 2026)
2. **Build Infrastructure with Terraform on Google Cloud** (Dec 2025)
3. **Develop Your Google Cloud Network** (Dec 2025)
4. **Implement Cloud Security Fundamentals on Google Cloud** (Nov 2025)
5. **Build a Secure Google Cloud Network** (Nov 2025)
6. **Set Up an App Dev Environment on Google Cloud** (Nov 2025)
7. **Implement Load Balancing on Compute Engine** (Nov 2025)

### 🛡️ Additional Certifications

**Blue Team Junior Analyst Pathway Bundle** - Security Blue Team (Nov 2025)  
**Credential ID**: 918007510  
**Skills**: OSINT, Digital Forensics, Vulnerability Management, DarkWeb Operations, Threat Hunting, Network Analysis

---

## 📋 Prerequisites

- **Google Cloud Platform account** (free tier available)
- **Basic knowledge** of cloud computing
- **Command line familiarity** (optional but recommended)
- **Updated web browser** to access GCP console

---

## 📁 Repository Structure

```
gcp-labs-practicas/
├── certificado/                                       # Associate Cloud Engineer Certification
├── labs/
│   ├── networking/                                    # VPC networks, firewalls, connectivity
│   ├── cloud-run/                                     # Serverless deployments
│   ├── compute-sql-storage/                           # 3-tier architectures
│   ├── marketplace/                                   # Pre-configured solutions
│   ├── load-balancing/                                # L4 and L7 load balancers
│   ├── dev-environment/                               # Cloud Functions, Pub/Sub, IAM, Monitoring
│   ├── security-operations/                           # Security Command Center, threat detection
│   │   ├── security-basics/                           # IAM, KMS, VPC Peering, IAP, GKE
│   │   └── scc-threat-mitigation/                     # Security Command Center labs
│   ├── develop-network/                               # GKE, BigQuery, SQL
│   ├── Terraform/                                     # Infrastructure as Code
│   └── docs/                                          # Documentation and reference PDFs
├── images/                                            # Screenshots and diagrams
└── README.md
```

---

## 🧪 Completed Labs

### 1. Networking & Compute

#### 🌐 [Introduction to VPC and Compute Engine](labs/networking/mi-aventura-google-cloud-redes-vpc-vms.md)

**Lab ID**: Network Fundamentals  
**Duration**: ~45 minutes  
**Level**: Beginner

**What you'll learn**:

- Create and delete custom VPC networks
- Configure firewall rules
- Connectivity between VMs in different regions
- Network connectivity troubleshooting

**Services**: `Compute Engine` • `VPC` • `Firewall Rules`

---

### 2. Serverless & Containers

#### 🐳 [Hello Cloud Run - Serverless Container Deployment](labs/cloud-run/mi-bitacora-laboratorio-hola-cloud-run.md)

**Lab ID**: Cloud Run Basics  
**Duration**: ~40 minutes  
**Level**: Beginner

**What you'll learn**:

- Containerize Node.js applications
- Build images with Cloud Build
- Deploy to Cloud Run
- **Error resolution**: `Cannot find module 'index.js'`

**Services**: `Cloud Run` • `Cloud Build` • `Artifact Registry`

---

### 3. Storage & Databases

#### 🗄️ [3-Tier Architecture: Compute + SQL + Storage](labs/compute-sql-storage/mi-experiencia-practica-compute-engine-cloud-sql-storage-gcp.md)

**Lab ID**: 3-Tier Architecture  
**Duration**: ~60 minutes  
**Level**: Intermediate

**What you'll learn**:

- Integrate Compute Engine with Cloud SQL
- Configure Cloud Storage buckets
- Service connectivity
- Complete web architecture

**Services**: `Compute Engine` • `Cloud SQL` • `Cloud Storage`

#### 📦 [Cloud Storage: Qwik Start (Console)](labs/dev-environment/Qwik%20Start%20-%20Bucket/📄%20Documentación%20del%20Lab:%20GSP073%20-%20Cloud%20Storage:%20Qwik%20Start%20(Consola).md)

**Lab ID**: GSP073  
**Services**: `Cloud Storage`

#### 💻 [Cloud Storage: Qwik Start (CLI/SDK)](labs/dev-environment/Quick%20Start%20-%20%20CLI_SDK/📄%20Documentación%20del%20Lab:%20Cloud%20Storage:%20Qwik%20Start%20(CLI).md)

**Lab ID**: GSP074  
**Services**: `Cloud Storage` • `gcloud CLI`

---

### 4. Load Balancing

#### ⚖️ [Network Load Balancer (L4)](labs/load-balancing/network-load-balancer/Configuración%20de%20un%20Balanceador%20de%20Cargas%20de%20Red%20(GSP007)%20en%20Google%20Cloud.md)

**Lab ID**: GSP007  
**Level**: Intermediate  
**Type**: Layer 4 (Transport)

**Services**: `Load Balancing` • `Compute Engine` • `Health Checks`

#### 🌐 [Application Load Balancer (L7)](labs/load-balancing/application-load-balancer/Configuración%20de%20un%20Balanceador%20de%20Cargas%20de%20Aplicaciones%20(GSP155).md)

**Lab ID**: GSP155  
**Level**: Intermediate  
**Type**: Layer 7 (Application)

**Services**: `HTTP(S) Load Balancing` • `Backend Services` • `URL Maps`

#### 🔒 [Internal Application Load Balancer](labs/load-balancing/internal-application-load-balancer/Proyecto%20de%20Portafolio:%20Lab%20GSP041%20-%20Configuración%20de%20un%20Balanceador%20de%20Cargas%20de%20Aplicaciones%20Interno.md)

**Lab ID**: GSP041  
**Level**: Advanced  
**Type**: Internal L7

**Services**: `Internal Load Balancing` • `Private VPC`

#### 🏆 [Challenge Lab: L4 and L7 Implementation](labs/load-balancing/challenge-l4-l7/Implementación%20de%20Balanceo%20de%20Cargas%20(L4%20y%20L7).md)

**Lab ID**: GSP313  
**Level**: Advanced  
**Type**: Challenge without instructions

---

### 5. DevOps & Monitoring

#### 📊 [Cloud Monitoring: Qwik Start](labs/dev-environment/Cloud%20Monitoring:%20Qwik%20Start%0A/📄%20Documentación%20del%20Lab:%20GSP089%20-%20Cloud%20Monitoring:%20Qwik%20Start.md)

**Lab ID**: GSP089  
**Services**: `Cloud Monitoring` • `Metrics` • `Alerting`

#### ⚡ [Cloud Run Functions: Qwik Start (Console)](labs/dev-environment/Cloud%20Run%20Functions:%20Quick%20Start/📄%20Documentación%20del%20Lab:%20GSP081%20-%20Cloud%20Run%20Functions:%20Qwik%20Start%20(Consola).md)

**Lab ID**: GSP081  
**Services**: `Cloud Functions` • `Event-driven Architecture`

#### 🖥️ [Cloud Run Functions: Qwik Start (CLI)](labs/dev-environment/Cloud%20Run%20Functions:%20Qwik%20Start%20-%20Línea%20de%20comandos/CloudRun.md)

**Services**: `Cloud Functions` • `gcloud CLI`

#### 🏆 [Challenge Lab GSP315](labs/dev-environment/Desafio%20-%20lab/Lab%20de%20Desafío%20GSP315.md)

**Lab ID**: GSP315  
**Level**: Expert

---

### 6. Messaging

#### 📮 [Pub/Sub: Qwik Start (Console)](labs/dev-environment/Pub_Sub:%20Qwik%20Start%20-%20Consola/QuickStart-Pup_Sub.md)

**Services**: `Pub/Sub` • `Topics` • `Subscriptions`

#### 💻 [Pub/Sub: Qwik Start (CLI)](labs/dev-environment/Pub_Sub:%20Qwik%20Start%20-%20Línea%20de%20comandos/LineaDeComandos.md)

**Services**: `Pub/Sub` • `gcloud CLI`

#### 🐍 [Pub/Sub: Qwik Start (Python)](labs/dev-environment/Pub_Sub:%20Qwik%20Start%20(Python)/Python.md)

**Services**: `Pub/Sub` • `Python Client Library`

---

### 7. Security & IAM

#### 🔐 [Identity and Access Management (IAM): Qwik Start](labs/dev-environment/Quick%20Start%20-%20%20Cloud%20IAM/📄%20Documentación%20del%20Lab:%20GSP064%20-%20Identity%20and%20Access%20Management%20(IAM):%20Qwik%20Start.md)

**Lab ID**: GSP064  
**Services**: `Cloud IAM` • `Roles` • `Permissions`

#### 🛡️ [Identity-Aware Proxy (IAP): Protect Virtual Machines](labs/secure-network-creation/Protege%20máquinas%20virtuales%20con%20Chrome%20Enterprise%20Premium/Google%20Cloud:%20Identity-Aware%20Proxy%20(IAP).md)

**Duration**: ~60 minutes  
**Level**: Intermediate

**What you'll learn**:

- Configure Identity-Aware Proxy to protect resources
- Control VM access without VPN
- Implement identity-based authentication
- IAP permissions troubleshooting

**Services**: `Identity-Aware Proxy` • `Cloud IAM` • `Compute Engine`

#### 🔐 [Service Accounts and Roles](labs/security-operations/security-basics/Aspectos%20principales%20de%20las%20cuentas%20de%20servicio%20y%20los%20roles/Implementación%20Segura%20de%20Identidades%20de%20Máquina%20en%20Google%20Cloud.md)

**Level**: Intermediate | **Duration**: ~45 min

**What you'll learn**:
- Create and manage Service Accounts
- Apply principle of least privilege
- Machine-to-machine authentication

**Services**: `Service Accounts` • `IAM Roles` • `BigQuery`

#### 🎨 [Custom IAM Roles](labs/security-operations/security-basics/Roles%20personalizados%20de%20IAM/Roles%20personalizados%20de%20IAM.md)

**Level**: Advanced | **Duration**: ~40 min

**Services**: `Custom IAM Roles` • `Permissions`

#### 🔒 [Cloud KMS](labs/security-operations/security-basics/Empieza%20a%20usar%20Cloud%20KMS/EmpiezaA_usar_Cloud_KMS.md)

**Level**: Intermediate | **Duration**: ~35 min

**Services**: `Cloud KMS` • `Encryption`

#### 🌐 [VPC Peering](labs/security-operations/security-basics/Intercambio%20de%20tráfico%20entre%20redes%20de%20VPC/Reporte%20de%20Laboratorio:%20Intercambio%20de%20Tráfico%20entre%20Redes%20VPC%20(VPC%20Peering).md)

**Level**: Intermediate | **Duration**: ~50 min

**Services**: `VPC Peering` • `Routing`

#### 🔐 [Authentication with IAP](labs/security-operations/security-basics/Autenticación%20de%20Usuarios%20con%20Identity-Aware%20Proxy%20(IAP)/Autenticación%20de%20Usuarios%20con%20Identity-Aware%20Proxy.md)

**Level**: Advanced | **Duration**: ~60 min

**Services**: `Identity-Aware Proxy` • `OAuth`

#### 🛡️ [Cloud Armor](labs/security-operations/secure-network-creation/Balanceador%20de%20cargas%20de%20aplicaciones%20con%20Cloud%20Armor/Balanceador%20de%20cargas%20de%20aplicaciones%20con%20Cloud%20Armor.md)

**Level**: Advanced | **Duration**: ~55 min

**Services**: `Cloud Armor` • `DDoS Protection`

#### 🏆 [Challenge: Secure Architecture GSP322](labs/security-operations/secure-network-creation/Lab%20de%20desafío_GSP322/Arquitectura%20de%20Red%20Segura%20y%20Modelo%20Zero%20Trust%20en%20Google%20Cloud.md)

**Lab ID**: GSP322 | **Level**: Expert

**Services**: `Zero Trust` • `VPC` • `IAP`

#### 🐛 [Security Command Center](labs/security-operations/scc-threat-mitigation/)

**Level**: Advanced | **Labs**: 5 (Setup, Vulnerabilities, Web Scanning, Threat Detection, Challenge)

**Services**: `Security Command Center` • `Threat Detection`

---

### 8. Kubernetes & GKE

#### ☸️ [Managing Deployments in GKE](labs/develop-network/Cómo%20administrar%20implementaciones%20con%20Kubernetes%20Engine/Administración%20de%20Implementaciones%20con%20Google%20Kubernetes%20Engine.md)

**Level**: Intermediate | **Duration**: ~60 min

**What you'll learn**:
- Create and manage GKE deployments
- Rolling updates and rollbacks
- Application scaling

**Services**: `GKE` • `Kubernetes` • `Deployments`

#### 🔒 [Private GKE Cluster](labs/security-operations/security-basics/Cómo%20configurar%20un%20clúster%20de%20Kubernetes%20privado/Cómo_configurar_un_clúster_de_Kubernetes_privado.md)

**Level**: Advanced | **Duration**: ~55 min

**What you'll learn**:
- Private nodes and master endpoint
- Network policies
- Pod security

**Services**: `GKE` • `Private Cluster` • `Network Policies`

#### 🏆 [Challenge: Secure GKE](labs/security-operations/security-basics/Desafio:%20Implementación%20de%20Infraestructura%20Segura%20en%20Google%20Kubernetes%20Engine/Reporte%20Técnico:%20Implementación%20de%20Infraestructura%20Segura%20en%20Google%20Kubernetes%20Engine.md)

**Level**: Expert | **Duration**: ~90 min

**Services**: `GKE` • `RBAC` • `Workload Identity`

#### 🏆 [Challenge: Develop Your Network](labs/develop-network/Desarrolla%20tu%20red%20de%20Google%20Cloud:%20Lab%20de%20desafío/Desarrolla%20tu%20red%20de%20Google%20Cloud:%20Lab%20de%20desafío.md)

**Level**: Expert | **Duration**: ~75 min

**Services**: `VPC` • `Load Balancing` • `Firewall`

---

### 9. Infrastructure as Code (Terraform)

#### 🏗️ [Terraform Modules](labs/Terraform/Cómo%20interactuar%20con%20los%20módulos%20de%20Terraform/GSP751.md)

**Lab ID**: GSP751 | **Level**: Intermediate

**Services**: `Terraform` • `IaC` • `Modules`

#### 📦 [Terraform State Management](labs/Terraform/Administra%20el%20estado%20de%20Terraform/AdministraelestadodeTerraform.md)

**Level**: Advanced | **Duration**: ~45 min

**Services**: `Terraform` • `State Management`

#### 🏆 [Challenge: Terraform](labs/Terraform/Lab%20de%20desafio/LabDesafio.md)

**Level**: Expert | **Duration**: ~60 min

**Services**: `Terraform` • `IaC`

---

### 10. Data & Analytics

#### 📊 [BigQuery and Cloud SQL](labs/develop-network/Introduction%20to%20SQL%20for%20BigQuery%20and%20Cloud%20SQL/BigQueryLabs.md)

**Level**: Intermediate | **Duration**: ~60 min

**Services**: `BigQuery` • `Cloud SQL` • `SQL`

---

### 11. Marketplace

#### 🛒 [Getting Started with Google Cloud Marketplace](labs/marketplace/mi-informe-laboratorio-primeros-pasos-google-cloud-marketplace.md)

**Duration**: ~20 minutes  
**Level**: Beginner

**What you'll learn**:

- Deploy pre-configured solutions
- One-click LAMP stack
- AWS Marketplace comparison

**Services**: `Cloud Marketplace` • `Click to Deploy`

---

## 🛠️ Technologies & Services

### Compute

- **Compute Engine**: Scalable virtual machines
- **Cloud Run**: Fully managed serverless containers
- **Cloud Functions**: Event-driven serverless functions

### Networking

- **VPC**: Global private virtual networks
- **Cloud Load Balancing**: L4 and L7 load balancers
- **Firewall Rules**: Network security

### Storage & Databases

- **Cloud Storage**: Object storage
- **Cloud SQL**: Managed relational databases

### DevOps

- **Cloud Build**: CI/CD for containers
- **Artifact Registry**: Container registry
- **Cloud Monitoring**: Observability and alerting

### Messaging & Integration

- **Pub/Sub**: Asynchronous messaging

### Security

- **Cloud IAM**: Identity and Access Management

---

## 🔄 GCP vs AWS Comparison

| GCP Service         | AWS Service | Function                    | Key Differences                                                       |
| ------------------- | ----------- | --------------------------- | --------------------------------------------------------------------- |
| **Compute Engine**  | EC2         | Virtual machines            | GCP: per-second billing; AWS: per-hour (on-demand instances)          |
| **Cloud Run**       | Fargate     | Serverless containers       | Cloud Run: scales to zero; Fargate: minimum 1 task                    |
| **Cloud Functions** | Lambda      | Serverless functions        | Similar, different triggers and runtimes                              |
| **Cloud SQL**       | RDS         | Relational databases        | GCP: native VPC integration; AWS: more engines available              |
| **Cloud Storage**   | S3          | Object storage              | S3: more storage classes; GCP: simpler                                |
| **VPC**             | VPC         | Virtual networks            | GCP: VPC is global; AWS: VPC per region                               |
| **Load Balancing**  | ELB/ALB/NLB | Load balancers              | GCP: single load balancer can be global                               |
| **Cloud Build**     | CodeBuild   | CI/CD                       | Similar, different integrations                                       |
| **Pub/Sub**         | SNS/SQS     | Messaging                   | Pub/Sub: both patterns in one; AWS: separate services                 |
| **Cloud IAM**       | IAM         | Identity management         | Similar models, different syntax                                      |
| **Marketplace**     | Marketplace | Pre-configured solutions    | Equivalent functionality                                              |

---

## 📖 How to Use This Repository

### For GCP Beginners

1. **Start with fundamentals**:
   
   - [VPC and Compute Engine](labs/networking/mi-aventura-google-cloud-redes-vpc-vms.md)
   - [Cloud Storage Qwik Start](labs/dev-environment/Qwik%20Start%20-%20Bucket/)
   - [Cloud IAM Basics](labs/dev-environment/Quick%20Start%20-%20%20Cloud%20IAM/)

2. **Progress to intermediate services**:
   
   - [Cloud Run](labs/cloud-run/)
   - [3-tier Architecture](labs/compute-sql-storage/)
   - [Network Load Balancer](labs/load-balancing/network-load-balancer/)

3. **Challenge yourself with advanced labs**:
   
   - [Internal Load Balancer](labs/load-balancing/internal-application-load-balancer/)
   - [Challenge Labs](labs/load-balancing/challenge-l4-l7/)

### For Those Coming from AWS

- Review **"AWS Comparison"** sections in each lab
- Check the [equivalence table](#-gcp-vs-aws-comparison) above
- Labs include analogies with AWS services

### For Troubleshooting

- Each lab documents **real errors** encountered and their solutions
- Search `.md` files for words like "Problem", "Error", "Solution"

---

## 🤝 Contributions

Found an error or have an improvement? Your contribution is welcome!

- 🐛 **Report bugs**: Open an [Issue](../../issues)
- 💡 **Suggest improvements**: Open an [Issue](../../issues) with your proposal
- 🔧 **Submit corrections**: Send a [Pull Request](../../pulls)
- ⭐ **Support the project**: Give it a star if you find it useful

### Contributing guidelines:
1. Fork the repository
2. Create a branch for your feature (`git checkout -b feature/new-feature`)
3. Commit your changes (`git commit -am 'Add new feature'`)
4. Push to the branch (`git push origin feature/new-feature`)
5. Open a Pull Request

---

## 📄 License

This project is under the **MIT License** - see the [LICENSE](LICENSE) file for details.

### License summary:
- ✅ Commercial use allowed
- ✅ Modification allowed
- ✅ Distribution allowed
- ✅ Private use allowed
- ❗ Include copyright notice
- ❗ Include license text

---

## 📧 Contact

**Christhian Rodriguez**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/christhianrodriguez)
[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/christhianrodriguez)

---

## 📝 Notes

- ✅ **All labs successfully completed**
- 📸 **Includes complete process screenshots**
- 🐛 **Documents real problems and solutions**
- 🔄 **AWS comparisons when relevant**
- 📅 **Completion period**: October - February 2026

---

> 💡 **Tip**: This repository is continuously updated. Give it a ⭐ to follow the progress.

**Last update**: February 2026

> 📝 **Note**: Lab documentation is primarily in Spanish as these represent my personal learning journey. Technical implementations, code, and architectures are universal. English translations available upon request.
