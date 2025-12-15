# 🛡️ Reporte de Laboratorio: Autenticación de Usuarios con Identity-Aware Proxy (IAP)

**Laboratorio:** GSP499 - User Authentication: Identity-Aware Proxy

**Plataforma:** Google Cloud Platform (GCP)

**Tecnología Principal:** App Engine, IAM, IAP (Zero Trust Security)

**Autor:** Christhian Rodriguez

## 1. Introducción y Objetivo

El objetivo de este laboratorio fue transformar una aplicación web pública y sin seguridad en una aplicación interna segura utilizando el modelo **"Zero Trust"** (Cero Confianza) de Google.

En lugar de utilizar firewalls tradicionales o VPNs complejas, implementamos **Identity-Aware Proxy (IAP)**. IAP actúa como un "guardia de seguridad" inteligente que intercepta todas las solicitudes web, verifica la identidad del usuario contra Google Identity Services y solo permite el paso si el usuario tiene los permisos IAM correctos.

### ¿Qué es realmente IAP?

IAP es un servicio global de GCP que permite controlar el acceso a aplicaciones HTTPs (en App Engine, Compute Engine o Kubernetes) basándose en la **identidad** del usuario y el **contexto** de la solicitud, no solo en su dirección IP de red. Es la base del modelo *BeyondCorp* de Google, permitiendo a los empleados trabajar desde cualquier lugar sin VPN.

## 2. Desarrollo del Laboratorio

### Fase 1: Despliegue Inicial de la Aplicación

Comenzamos desplegando una aplicación básica en Python ("Hello World") en **Google App Engine Standard Environment**.

**Comandos Clave:**

- `sed -i 's/python37/python313/g' app.yaml`: Actualizamos la configuración para usar una versión moderna de Python (3.13).

- `gcloud app deploy`: Empaqueta el código y lo sube a la infraestructura de Google.

> Evidencia de Despliegue:
> 
> Aquí se muestra la terminal confirmando que la aplicación se subió correctamente a App Engine y la URL pública generada.
> 
> ![2025-11-27 22.01.51 console.cloud.google.com ce167cac4599.png](Fotos/31bf89dc89e94a1b83cd1a7d0f496450db4ad539.png)

> Estado Inicial:
> 
> La aplicación es accesible públicamente por cualquier persona en internet. No hay seguridad.
> 
> ![2025-11-27 22.01.34 qwiklabs-gcp-01-28ffd5b8a37d.uc.r.appspot.com cc5e75b8e782.png](Fotos/ab52f17531fa07b1b12319047320ad875c42a23f.png)

### Fase 2: Restricción de Acceso con IAP

Para proteger la aplicación, configuramos la **Pantalla de Consentimiento OAuth** (necesaria para que IAP pueda "loguear" usuarios) y activamos el interruptor de IAP.

> Configuración OAuth:
> 
> Se creó la configuración básica interna para permitir la autenticación.
> 
> ![2025-11-27 22.10.40 console.cloud.google.com 1d8e8fe21698.png](Fotos/82d51cdbeed8e11fdb69ca2aa1eeef2f212f3563.png)

Activación de IAP:

> En la consola de Seguridad, encendimos IAP para el recurso de App Engine. En este punto, el tráfico se corta para todos.
> 
> La Prueba de Fuego:
> 
> ![2025-11-27 22.13.13 console.cloud.google.com 1d3078a450cc.png](Fotos/82d6e0042e9cd350b6cb462ff8fc035ae6739325.png)
> 
> Al intentar acceder a la web nuevamente, el acceso fue denegado. Esto confirma que IAP está interceptando el tráfico. Aunque me autentiqué con Google, mi usuario no tenía permiso para pasar.

> Acceso Denegado:
> 
> IAP bloquea la solicitud porque mi usuario no está autorizado explícitamente.
> 
> ![2025-11-27 22.13.21 qwiklabs-gcp-01-28ffd5b8a37d.uc.r.appspot.com 9d63e40bc6ba.png](Fotos/b57840694f16942a9ed18922a98cc45c13e9c931.png)

Resolución:

Agregamos al usuario estudiante al rol IAM IAP-secured Web App User.

> Gestión de IAM:
> 
> Asignación del rol específico que permite "atravesar" el proxy de identidad.
> 
> ![2025-11-27 22.15.50 console.cloud.google.com 6427f061041c.png](Fotos/dc4928412511cf7ba62e740894ed35257834ffcf.png)

### Fase 3: Identidad del Usuario y Vulnerabilidades

Actualizamos la aplicación para que leyera los encabezados (headers) que IAP inyecta en la petición (`X-Goog-Authenticated-User-Email`).

Sin embargo, descubrimos un riesgo: **Si IAP se apaga accidentalmente, cualquiera puede falsificar esos encabezados.**

Realizamos un ataque de "Spoofing" simulado usando `curl` mientras IAP estaba apagado.

> Simulación de Ataque:
> 
> Usando curl, inyecté un header falso (totally fake email). Como la app confiaba ciegamente en el header sin verificar la firma, creyó que ese era mi usuario.
> 
> ![2025-11-27 22.23.31 console.cloud.google.com 99b0ad9616a7.png](Fotos/91596d80654230e2f5f45f79f9f8f8f47eeb6761.png)

### Fase 4: Verificación Criptográfica (Solución Robusta)

Para solucionar la vulnerabilidad anterior, implementamos una validación del header `X-Goog-IAP-JWT-Assertion`. Este es un token firmado criptográficamente por Google.

La aplicación ahora:

1. Recibe el token.

2. Descarga las claves públicas de Google.

3. Verifica que el token sea auténtico y no haya sido alterado.

> Despliegue Final:
> 
> Subiendo la versión segura del código (3-HelloVerifiedUser) que incluye las librerías de validación criptográfica.
> 
> ![2025-11-27 22.26.48 console.cloud.google.com 011e71112f0a.png](Fotos/dec19cb314bf6e5b04d02d9f96eaf173b6d471b5.png)

Resultado Final:

Con IAP activado nuevamente y el código seguro, la aplicación muestra la identidad real y verificada. Ya no es posible engañarla con un simple curl.

> Usuario Verificado:
> 
> La aplicación muestra los datos extraídos del JWT verificado. Seguridad completa.
> 
> ![77824d020a2c6d2dbc34f073627dd64ec94a582b.png](Fotos/fff99c450311c22d7d6f80f742e1afd79edff5a0.png)

> Consola IAP Final:
> 
> Estado final del servicio protegiendo el recurso.
> 
> ![2025-11-27 22.27.26 qwiklabs-gcp-01-28ffd5b8a37d.uc.r.appspot.com 5ab6169983e0.png](Fotos/ff9d81224dcee08626d9f4ce93010ec6205aa3b9.png)

## 3. Lecciones Aprendidas y Conclusiones

1. **Seguridad Perimetral:** IAP simplifica drásticamente la seguridad. No tuvimos que configurar firewalls complejos ni VPNs para restringir el acceso a usuarios corporativos internos.

2. **Defensa en Profundidad:** No basta con confiar en que IAP está encendido. La aplicación debe ser responsable de verificar la autenticidad de la información que recibe (validación JWT).

3. **Roles IAM:** La seguridad en GCP es granular. Un usuario autenticado no es sinónimo de autorizado; se requiere el rol específico `IAP-secured Web App User`.

### Glosario de Comandos Utilizados

| **Comando**                  | **Descripción**                                                                                               |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------- |
| `gcloud auth list`           | Muestra la cuenta activa y las credenciales actuales.                                                         |
| `gcloud config list project` | Verifica en qué proyecto de GCP estamos trabajando.                                                           |
| `gcloud app deploy`          | Despliega el código local a App Engine.                                                                       |
| `gcloud app browse`          | Abre la URL de la aplicación desplegada en el navegador.                                                      |
| `curl -X GET -H "..."`       | Herramienta para hacer peticiones HTTP manuales; usada aquí para simular un ataque inyectando headers falsos. |
