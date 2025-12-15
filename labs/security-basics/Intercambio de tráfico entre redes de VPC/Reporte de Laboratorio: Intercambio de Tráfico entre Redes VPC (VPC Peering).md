# Reporte de Laboratorio: Intercambio de Tráfico entre Redes VPC (VPC Peering)

**Laboratorio:** GSP193 - VPC Network Peering

**Fecha:** 27 de Noviembre de 2024

**Perfil:** Google Associate Cloud Engineer (ACE)

## 1. Objetivo del Laboratorio

El objetivo principal de esta práctica fue configurar una conexión privada y segura entre dos redes de Nube Privada Virtual (VPC) alojadas en proyectos diferentes de Google Cloud. Se buscó demostrar que es posible comunicar cargas de trabajo (Máquinas Virtuales) utilizando direcciones IP internas (RFC1918) sin exponer el tráfico a la internet pública, reduciendo la latencia y aumentando la seguridad.

## 2. Escenario de Arquitectura

Se simularon dos entornos separados (típicamente representando dos departamentos, dos organizaciones o una adquisición empresarial):

- **Proyecto A:** Contiene la `network-a` con el rango de IP `10.0.0.0/16`.

- **Proyecto B:** Contiene la `network-b` con el rango de IP `10.8.0.0/16`.

El desafío consistió en conectar estos dos entornos aislados para que sus servidores pudieran comunicarse directamente.

![i6fwOoVXTt4J7oToas+FV61tUgLuDiaw5y7zGEnr6lU=.png](Fotos/42433c548c0858e261987031ea36e84d7b2bdf3e.png)

*Figura 1: Esquema lógico de la separación de redes antes del Peering.*

## 3. Procedimiento Realizado

### Fase 1: Despliegue de Infraestructura

Utilizando la interfaz de línea de comandos (`gcloud CLI`) en Cloud Shell, aprovisionamos la infraestructura base en ambos proyectos. Se optó por redes de "modo personalizado" para tener control total sobre los rangos de IP y evitar superposiciones (overlap), lo cual es un requisito estricto para el VPC Peering.

**Acciones ejecutadas:**

1. Creación de VPCs personalizadas (`network-a` y `network-b`).

2. Creación de subredes en la región `us-central1`.

3. Despliegue de instancias de Compute Engine (`vm-a` y `vm-b`).

4. Configuración de reglas de Firewall para permitir SSH e ICMP.

![2025-11-27 18.01.07 console.cloud.google.com 8524d441da40.png](Fotos/7825cc40e9f578773f6d2fa98e24b03e2ca1a7dd.png)

Figura 2: Creación de recursos y reglas de firewall mediante CLI.

Validación de Recursos:

Se verificó la correcta creación de las redes y las instancias en la consola:

- Red A:
  
  ![2025-11-27 18.00.22 console.cloud.google.com b48a4b0c8838.png](Fotos/912ec154b67fe21ec92cfdcfb26af0059d0bbb41.png)

- Red B:
  
  ![2025-11-27 18.00.32 console.cloud.google.com cfeb549fbf20.png](Fotos/9a6e192839a5c44f2e69941f9f8e966381d90c4d.png)

### Fase 2: Configuración del VPC Peering

Se estableció la conexión de emparejamiento (Peering). Es crucial notar que el Peering es **bidireccional y no transitivo**.

1. Se configuró `peer-ab` desde la Red A hacia la Red B.

2. Se configuró `peer-ba` desde la Red B hacia la Red A.

Al completarse ambos lados, el estado cambió a `ACTIVE`, permitiendo el intercambio de rutas de subred.

![a3mCwnSLHBiYoGJjFqeP4kgj7HgaY87W9CevTJR0eK4=.png](Fotos/38e5a941fe9d50dd4c07da0d5d5b9c8d0f05b8a4.png)

*Figura 5: Flujo de tráfico activo entre VPCs.*

### Fase 3: Verificación y Troubleshooting

Se validaron las instancias creadas para realizar pruebas de conectividad.

- Instancia VM-A:
  
  ![2025-11-27 17.59.49 console.cloud.google.com 65f9e6517ff3.png](Fotos/62cad124f01e2b6adba6cfd8eb6cfe6debd79a5f.png)

- Instancia VM-B:
  
  ![2025-11-27 17.59.32 console.cloud.google.com c58e7d3ba6f6.png](Fotos/a7fefa58792fa58ac4d70b9ac88e85c0c0e23e07.png)

Desafío de Conectividad SSH:

Durante la prueba, se presentaron errores de autenticación SSH (Permission denied publickey). Esto se resolvió aplicando principios de gestión de identidades:

1. Generación manual de llaves RSA (`ssh-keygen`).

2. Inyección de la llave pública en los Metadatos del proyecto.

3. Identificación correcta de la **Zona de Disponibilidad** de la VM, ya que el comando por defecto apuntaba a una zona incorrecta.

## 4. Principios de Ciberseguridad Aplicados

Durante este laboratorio, se pusieron en práctica los siguientes principios fundamentales de seguridad en la nube:

1. Aislamiento de Red (Network Isolation):
   
   Las VPCs son globales pero privadas por defecto. Al usar VPC Peering, mantuvimos el tráfico dentro de la red troncal de Google (Google Backbone). Esto mitiga riesgos de ataques Man-in-the-Middle y Sniffing que son posibles cuando el tráfico viaja por la internet pública.

2. Principio de Mínimo Privilegio (Firewall):
   
   No abrimos todo el tráfico. Las reglas de firewall se configuraron explícitamente (--allow tcp:22,icmp).
   
   - **TCP:22:** Solo para administración remota segura (SSH).
   
   - ICMP: Solo para pruebas de conectividad (Ping).
     
     Cualquier otro puerto o protocolo está bloqueado por defecto (Deny all ingress).

3. Gestión de Identidad y Acceso (IAM & Keys):
   
   El problema de conexión SSH reforzó la importancia de la gestión de claves. No basta con tener conectividad de red (el cable); se necesita autenticación (la llave). La seguridad de las instancias depende de la custodia correcta de las llaves privadas SSH y la correcta propagación de las llaves públicas a través de los metadatos del proyecto o OS Login.

4. No Transitividad del Peering:
   
   Desde el diseño, el VPC Peering no es transitivo. Si A conecta con B, y B conecta con C, A no puede llegar a C automáticamente. Esto es un control de seguridad que evita que una red comprometida pueda saltar lateralmente a toda la organización sin configuración explícita.

## 5. Glosario de Comandos CLI Utilizados

A continuación, se explica la sintaxis y función de los comandos críticos usados en la práctica:

### Configuración de Proyecto

- `gcloud config set project [PROJECT_ID]`: Cambia el contexto de la CLI para actuar sobre un proyecto específico. Es vital en entornos multiproyecto para no desplegar recursos en el lugar equivocado.

### Redes y Subredes

- `gcloud compute networks create [NAME] --subnet-mode custom`:
  
  - Crea una red VPC vacía.
  
  - `--subnet-mode custom`: **Crucial**. Evita que Google cree subredes automáticas en todas las regiones del mundo, permitiéndonos definir rangos IP específicos para evitar superposiciones (IP Overlap) en el futuro peering.

- `gcloud compute networks subnets create [NAME] --network [VPC] --range [CIDR] --region [REGION]`:
  
  - Define un segmento de red específico (ej. `10.0.0.0/16`) dentro de la VPC creada anteriormente.

### Seguridad y Firewall

- `gcloud compute firewall-rules create [NAME] --network [VPC] --allow tcp:22,icmp`:
  
  - Crea una regla de entrada (Ingress).
  
  - `--allow`: Define la lista blanca de protocolos permitidos. Sin esto, la VPC bloquea todo el tráfico entrante a las VMs, incluso si el Peering es exitoso.

### Compute Engine (VMs)

- `gcloud compute instances create [NAME] --zone [ZONE] --subnet [SUBNET]`:
  
  - Aprovisiona la máquina virtual.
  
  - **Lección aprendida:** El flag `--zone` es mandatorio para saber dónde reside físicamente el recurso. Si intentamos conectar por SSH a una zona distinta, la conexión fallará (recurso no encontrado).

### VPC Peering

- `gcloud compute networks peerings create [NAME] --network [LOCAL_VPC] --peer-project [REMOTE_PROJECT] --peer-network [REMOTE_VPC]`:
  
  - Crea el "tubo" de conexión.
  
  - Requiere el ID del proyecto remoto porque estamos cruzando límites de proyectos.
  
  - Debe ejecutarse en **ambos sentidos** para que el estado pase de `INACTIVE` a `ACTIVE`.

### Conectividad y Diagnóstico

- `ssh-keygen -t rsa -b 4096 -C "[USER]"`: Genera un par de claves criptográficas (pública/privada) para autenticación segura.

- `gcloud compute ssh [VM_NAME] --zone [ZONE]`: Comando "wrapper" que gestiona las llaves SSH y conecta a la instancia.

- `ping -c 5 [IP_INTERNA]`: Envía paquetes ICMP para verificar que la ruta de red existe y está abierta.

Conclusión:

El laboratorio demostró exitosamente cómo interconectar infraestructuras de nube dispares de manera segura. A pesar de los desafíos iniciales con la autenticación SSH, se logró validar que el tráfico fluye entre redes privadas sin exposición pública, cumpliendo con los estándares de arquitectura segura en Google Cloud.
