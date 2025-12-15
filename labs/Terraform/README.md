# 🏗️ Infrastructure as Code con Terraform

Esta sección cubre la gestión de infraestructura como código usando Terraform en Google Cloud Platform, desde conceptos básicos hasta gestión avanzada de estado y módulos.

## 📋 Laboratorios de Terraform

### 🔧 State Management & Backends

#### [Administra el Estado de Terraform](Administra%20el%20estado%20de%20Terraform/)
**Lab ID**: GSP752 | **Nivel**: Advanced | **Duración**: ~60 min

Gestión profesional del estado de Terraform con backends remotos.

**Lo que aprenderás**:
- Migrar estado local a Google Cloud Storage
- State locking y colaboración en equipo
- Importación de infraestructura legacy
- Troubleshooting de version drift

**Conceptos clave**: Remote backends, State migration, Resource import

---

### 📦 Modules & Reusability

#### [Interacción con Módulos de Terraform](Cómo%20interactuar%20con%20los%20módulos%20de%20Terraform/)
**Lab ID**: GSP751 | **Nivel**: Intermediate | **Duración**: ~45 min

Creación y uso de módulos reutilizables de Terraform.

**Lo que aprenderás**:
- Diseñar módulos reutilizables
- Versionado y distribución de módulos
- Input variables y outputs
- Module composition patterns

---

### 🏆 Challenge Labs

#### [🏆 Lab de Desafío](Lab%20de%20desafio/)
**Nivel**: Expert | **Duración**: ~90 min

Implementación completa de infraestructura sin instrucciones paso a paso.

**Desafíos**:
- Arquitectura multi-tier con Terraform
- Gestión de dependencias complejas
- Troubleshooting independiente
- Best practices de IaC

## 🛠️ Conceptos Fundamentales

### Infrastructure as Code (IaC)
```
Declarative Configuration → Terraform Plan → Infrastructure Deployment
         ↓                        ↓                      ↓
    Version Control         Preview Changes        Consistent State
```

### Terraform Workflow
1. **Write**: Definir infraestructura en archivos `.tf`
2. **Plan**: Revisar cambios antes de aplicar
3. **Apply**: Ejecutar cambios en la infraestructura
4. **Destroy**: Limpiar recursos cuando no se necesiten

## 🏗️ Arquitecturas con Terraform

### Basic Web Application
```hcl
# VPC Network
resource "google_compute_network" "vpc" {
  name = "webapp-vpc"
}

# Compute Instance
resource "google_compute_instance" "web" {
  name         = "web-server"
  machine_type = "e2-micro"
  zone         = var.zone
}

# Load Balancer
resource "google_compute_global_forwarding_rule" "lb" {
  name       = "webapp-lb"
  target     = google_compute_target_http_proxy.proxy.id
  port_range = "80"
}
```

### Multi-Environment Setup
```
environments/
├── dev/
│   ├── main.tf
│   ├── variables.tf
│   └── terraform.tfvars
├── staging/
│   ├── main.tf
│   ├── variables.tf
│   └── terraform.tfvars
└── prod/
    ├── main.tf
    ├── variables.tf
    └── terraform.tfvars
```

## 📦 Gestión de Módulos

### Module Structure
```
modules/
├── compute/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf
│   └── README.md
├── networking/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf
│   └── README.md
└── storage/
    ├── main.tf
    ├── variables.tf
    ├── outputs.tf
    └── README.md
```

### Module Usage
```hcl
module "networking" {
  source = "./modules/networking"
  
  project_id = var.project_id
  region     = var.region
  vpc_name   = "production-vpc"
}

module "compute" {
  source = "./modules/compute"
  
  network_id = module.networking.network_id
  subnet_id  = module.networking.subnet_id
}
```

## 🔄 State Management

### Local vs Remote State

| Aspecto | Local State | Remote State (GCS) |
|---------|-------------|-------------------|
| **Colaboración** | ❌ Individual | ✅ Equipo |
| **Locking** | ❌ No | ✅ Sí |
| **Backup** | ❌ Manual | ✅ Automático |
| **Seguridad** | ⚠️ Local disk | ✅ Encrypted |
| **Versioning** | ❌ No | ✅ Sí |

### Backend Configuration
```hcl
terraform {
  backend "gcs" {
    bucket = "terraform-state-bucket"
    prefix = "terraform/state"
  }
}
```

## 🚨 Best Practices

### Code Organization
1. **Separation of Concerns**: Un módulo por responsabilidad
2. **DRY Principle**: Reutilizar código con módulos
3. **Version Control**: Todo en Git con tags
4. **Documentation**: README en cada módulo

### State Management
1. **Remote Backend**: Siempre usar GCS o similar
2. **State Locking**: Prevenir modificaciones concurrentes
3. **Backup Strategy**: Versionado automático
4. **Access Control**: IAM para el bucket de estado

### Security
1. **Sensitive Variables**: Usar `sensitive = true`
2. **Secrets Management**: Integrar con Secret Manager
3. **Least Privilege**: IAM roles específicos para Terraform
4. **Audit Logging**: Registrar todas las operaciones

## 🔧 Troubleshooting Común

### State Issues
```bash
# Verificar estado actual
terraform show

# Refrescar estado desde infraestructura real
terraform refresh

# Importar recurso existente
terraform import google_compute_instance.example projects/PROJECT/zones/ZONE/instances/INSTANCE

# Mover recurso en el estado
terraform state mv google_compute_instance.old google_compute_instance.new
```

### Provider Issues
```bash
# Actualizar providers
terraform init -upgrade

# Verificar versiones
terraform version

# Limpiar cache de providers
rm -rf .terraform/
terraform init
```

### Planning Issues
```bash
# Plan detallado
terraform plan -detailed-exitcode

# Plan con target específico
terraform plan -target=google_compute_instance.web

# Validar configuración
terraform validate
```

## 📊 Workflow de CI/CD

### GitOps Pipeline
```yaml
# .github/workflows/terraform.yml
name: Terraform
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  terraform:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - uses: hashicorp/setup-terraform@v1
    
    - name: Terraform Init
      run: terraform init
      
    - name: Terraform Plan
      run: terraform plan
      
    - name: Terraform Apply
      if: github.ref == 'refs/heads/main'
      run: terraform apply -auto-approve
```

### Environment Promotion
```
Feature Branch → Dev Environment → Staging Environment → Production Environment
      ↓               ↓                    ↓                      ↓
   terraform plan  terraform apply    terraform plan      terraform apply
```

## 🎯 Casos de Uso Avanzados

### Multi-Cloud Deployment
```hcl
# Google Cloud Provider
provider "google" {
  project = var.gcp_project
  region  = var.gcp_region
}

# AWS Provider
provider "aws" {
  region = var.aws_region
}

# Azure Provider
provider "azurerm" {
  features {}
}
```

### Blue-Green Deployment
```hcl
resource "google_compute_instance_group_manager" "blue" {
  count = var.active_environment == "blue" ? 1 : 0
  # Blue environment configuration
}

resource "google_compute_instance_group_manager" "green" {
  count = var.active_environment == "green" ? 1 : 0
  # Green environment configuration
}
```

## 📚 Ruta de Aprendizaje

### Nivel 1: Fundamentos
1. **Terraform Basics**: Sintaxis HCL, providers, resources
2. **GCP Provider**: Compute, networking, storage resources
3. **State Basics**: Local state, terraform commands

### Nivel 2: Gestión Avanzada
4. [**State Management**](Administra%20el%20estado%20de%20Terraform/) - Remote backends, import
5. [**Modules**](Cómo%20interactuar%20con%20los%20módulos%20de%20Terraform/) - Reutilización y organización
6. **Variables & Outputs**: Parametrización y composición

### Nivel 3: Producción
7. **CI/CD Integration**: GitOps workflows
8. **Security**: Secrets, IAM, compliance
9. [**🏆 Challenge Lab**](Lab%20de%20desafio/) - Validación completa

## 🔗 Integraciones

### Con GCP Services
- **Cloud Build**: CI/CD pipelines
- **Secret Manager**: Gestión de secretos
- **Cloud Storage**: State backend
- **IAM**: Access control

### Con Herramientas DevOps
- **Git**: Version control
- **GitHub Actions**: CI/CD
- **Atlantis**: Pull request automation
- **Terragrunt**: DRY configurations

## 📖 Recursos Adicionales

- [Terraform GCP Provider](https://registry.terraform.io/providers/hashicorp/google/latest/docs)
- [Terraform Best Practices](https://www.terraform.io/docs/cloud/guides/recommended-practices/index.html)
- [GCP Terraform Samples](https://github.com/terraform-google-modules)
- [Terraform Module Registry](https://registry.terraform.io/browse/modules?provider=google)

## 🎓 Certificaciones Relacionadas

- **HashiCorp Certified: Terraform Associate**
- **Google Cloud Professional Cloud Architect**
- **Google Cloud Professional DevOps Engineer**

## 💡 Tips para el Examen

1. **State Management**: Entender backends remotos y locking
2. **Module Design**: Principios de reutilización y composición
3. **Provider Versions**: Gestión de dependencias
4. **Import/Export**: Migración de infraestructura legacy
5. **Troubleshooting**: Comandos de diagnóstico y recuperación