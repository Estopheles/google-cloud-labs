# ⚖️ Load Balancing en Google Cloud

Esta sección cubre los diferentes tipos de balanceadores de carga disponibles en GCP, desde conceptos básicos hasta implementaciones avanzadas y labs de desafío.

## 📋 Laboratorios Incluidos

### 🌐 [Network Load Balancer (L4)](network-load-balancer/)
**Lab ID**: GSP007 | **Nivel**: Intermediate | **Duración**: ~45 min

Implementación de un balanceador de cargas de red (Layer 4) que distribuye tráfico TCP.

**Lo que aprenderás**:
- Configurar Target Pools y Health Checks
- Crear Forwarding Rules
- Distribución de tráfico a nivel de transporte
- Troubleshooting de conectividad

**Servicios**: `Network Load Balancing` • `Compute Engine` • `Health Checks`

---

### 🌍 [Application Load Balancer (L7)](application-load-balancer/)
**Lab ID**: GSP155 | **Nivel**: Intermediate | **Duración**: ~50 min

Configuración de un balanceador HTTP(S) con capacidades de enrutamiento avanzado.

**Lo que aprenderás**:
- Backend Services y Instance Groups
- URL Maps y Host Rules
- Balanceo basado en contenido HTTP
- SSL/TLS termination

**Servicios**: `HTTP(S) Load Balancing` • `Backend Services` • `URL Maps`

---

### 🔒 [Internal Application Load Balancer](internal-application-load-balancer/)
**Lab ID**: GSP041 | **Nivel**: Advanced | **Duración**: ~60 min

Implementación de balanceador interno para tráfico privado dentro de la VPC.

**Lo que aprenderás**:
- Load balancing interno (sin IP pública)
- Arquitecturas multi-tier seguras
- Proxy-only subnets
- Conectividad privada entre servicios

**Servicios**: `Internal Load Balancing` • `Private VPC` • `Proxy Subnets`

---

### 🏆 [Challenge Lab: L4 y L7](challenge-l4-l7/)
**Lab ID**: GSP313 | **Nivel**: Expert | **Duración**: ~75 min

Lab de desafío sin instrucciones paso a paso. Implementación completa de ambos tipos.

**Desafíos**:
- Configurar Network LB y HTTP LB simultáneamente
- Resolver problemas sin guía
- Validar funcionamiento end-to-end
- Optimizar configuraciones

**Servicios**: `Multiple Load Balancers` • `Advanced Networking`

## 🔄 Comparación: L4 vs L7

| Característica | Network LB (L4) | Application LB (L7) |
|----------------|-----------------|---------------------|
| **Capa OSI** | Transporte (TCP/UDP) | Aplicación (HTTP/HTTPS) |
| **Velocidad** | ⚡ Muy rápida | 🚀 Rápida |
| **Funciones** | Básicas | Avanzadas |
| **Enrutamiento** | IP + Puerto | URL, Headers, Cookies |
| **SSL Termination** | ❌ No | ✅ Sí |
| **Casos de Uso** | Bases de datos, TCP | Aplicaciones web, APIs |

## 🛠️ Conceptos Clave

### Health Checks
- **HTTP Health Checks**: Para servicios web (L7)
- **TCP Health Checks**: Para servicios de red (L4)
- **Configuración**: Intervalos, timeouts, thresholds

### Backend Services
- **Instance Groups**: Managed/Unmanaged
- **Balancing Mode**: UTILIZATION, RATE, CONNECTION
- **Session Affinity**: CLIENT_IP, COOKIE

### Forwarding Rules
- **Global**: Para HTTP(S) Load Balancers
- **Regional**: Para Network Load Balancers
- **Internal**: Para tráfico privado

## 🎯 Casos de Uso Reales

### Network Load Balancer (L4)
- **Bases de datos**: MySQL, PostgreSQL clusters
- **Servicios TCP**: Aplicaciones legacy
- **Gaming**: Servidores de juegos en tiempo real
- **IoT**: Dispositivos con protocolos personalizados

### Application Load Balancer (L7)
- **Aplicaciones web**: Sitios web, SPAs
- **APIs REST**: Microservicios HTTP
- **Content-based routing**: A/B testing
- **SSL offloading**: Terminación de certificados

### Internal Load Balancer
- **Microservicios**: Comunicación interna
- **Arquitecturas multi-tier**: Frontend → Backend → DB
- **Compliance**: Tráfico que no debe salir de la VPC

## 🚨 Troubleshooting Común

### Problemas Frecuentes
1. **Health Check Failures**
   - Verificar firewall rules
   - Validar puertos y paths
   - Revisar logs de aplicación

2. **502/503 Errors**
   - Backend services down
   - Capacity insuficiente
   - Timeouts mal configurados

3. **Conectividad Issues**
   - Forwarding rules incorrectas
   - Target pools vacíos
   - Problemas de DNS

### Comandos de Diagnóstico
```bash
# Verificar health status
gcloud compute backend-services get-health BACKEND_SERVICE

# Listar forwarding rules
gcloud compute forwarding-rules list

# Verificar target pools
gcloud compute target-pools describe POOL_NAME
```

## 📚 Recursos Adicionales

- [Documentación oficial de Load Balancing](https://cloud.google.com/load-balancing/docs)
- [Choosing a load balancer](https://cloud.google.com/load-balancing/docs/choosing-load-balancer)
- [Best practices](https://cloud.google.com/load-balancing/docs/best-practices)

## 🎓 Orden Recomendado

1. **Empezar con**: [Network Load Balancer](network-load-balancer/) - Conceptos fundamentales
2. **Continuar con**: [Application Load Balancer](application-load-balancer/) - Funciones avanzadas  
3. **Avanzar a**: [Internal Load Balancer](internal-application-load-balancer/) - Arquitecturas complejas
4. **Desafiarse con**: [Challenge Lab](challenge-l4-l7/) - Validar conocimientos