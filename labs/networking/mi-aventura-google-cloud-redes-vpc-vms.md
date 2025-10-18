# Mi Aventura en Google Cloud: Explorando Redes VPC y VMs

Este documento es mi bitácora personal del laboratorio "Introducción a las redes de VPC y Google Compute Engine". Aquí resumo los pasos que seguí, mis descubrimientos y una pequeña comparación con su equivalente en el ecosistema de AWS.

## Tarea 1: Deconstruyendo la Red por Defecto

Todo proyecto en Google Cloud comienza con una red `default` preconfigurada. La primera tarea fue entender qué contenía y, más importante aún, por qué es indispensable.

Exploré sus componentes: subredes en cada región, rutas predefinidas y las famosas reglas de firewall que, por defecto, son bastante permisivas para empezar a trabajar (`allow-ssh`, `allow-icmp`, etc.).

![Aquí puedes insertar tu screenshot de la red 'default' con sus subredes.](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2012-32-53.png)

![Screenshot From 2025-10-17 12-40-02.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2012-40-02.png)

Luego, procedí con la demolición controlada:

1. **Eliminé las 4 reglas de Firewall** asociadas a la red.
2. **Eliminé la red VPC `default`** por completo.

El momento de la verdad llegó al intentar crear una instancia de VM. Como era de esperar, la consola me arrojó un error claro: **sin una red, no hay máquinas virtuales**. Esta fue la primera gran lección: la red es el cimiento sobre el cual se construye todo lo demás.

![Screenshot From 2025-10-17 12-41-28.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2012-41-28.png)

![Screenshot From 2025-10-17 12-47-17.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2012-47-17.png)

---

## Tarea 2: Construyendo Mi Propia Red desde Cero

Con el lienzo en blanco, era hora de crear mi propia infraestructura.

1. **Creé una nueva red VPC** llamada `mynetwork` en **modo automático**. Esto replicó la conveniencia de la red `default`, creando subredes en todas las regiones y aplicando las reglas de firewall estándar.
2. **Lancé dos instancias de VM (e2-micro)** en esta nueva red, pero estratégicamente ubicadas en regiones distintas para simular una infraestructura distribuida:
   * `mynet-us-vm`
   * `mynet-r2-vm`

El proceso fue sorprendentemente rápido. En pocos minutos, tenía mis dos máquinas virtuales listas, cada una con su IP interna (dentro de `mynetwork`) y una IP externa para acceder desde internet.

![Screenshot From 2025-10-17 12-52-28.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2012-52-28.png)

![Screenshot From 2025-10-17 12-54-18.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2012-54-18.png)

![Screenshot From 2025-10-17 12-58-12.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2012-58-12.png)

![Screenshot From 2025-10-17 12-58-30.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2012-58-30.png)

![Screenshot From 2025-10-17 12-59-12.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2012-59-12.png)

![Screenshot From 2025-10-17 12-59-20.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2012-59-20.png)



---

## Tarea 3: El Juego del Firewall y la Conectividad

Esta fue la parte más divertida y reveladora. Usando la conexión SSH a `mynet-us-vm` como mi centro de operaciones, comencé a probar la conectividad con `mynet-r2-vm`.

#### **Pruebas Iniciales (Todo Funciona)**

* **Ping a la IP interna:** `ping -c 3 10.140.0.2` -> **ÉXITO**. Gracias a la regla `mynetwork-allow-custom`.
* **Ping a la IP externa:** `ping -c 3 34.81.17.12` -> **ÉXITO**. Gracias a la regla `mynetwork-allow-icmp`.

![Screenshot From 2025-10-17 13-06-28.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2013-06-28.png)

![Screenshot From 2025-10-17 13-07-00.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2013-07-00.png)



#### **Eliminando Reglas y Observando el Caos**

Luego, fui eliminando las reglas una por una para ver el impacto directo:

1. **Eliminé `mynetwork-allow-icmp`**: Inmediatamente, el ping a la IP **externa** comenzó a fallar. La IP interna seguía respondiendo.
2. **Eliminé `mynetwork-allow-custom`**: Ahora, el ping a la IP **interna** también falló. Mis máquinas quedaron aisladas entre sí.
3. **Eliminé `mynetwork-allow-ssh`**: El golpe final. Mi sesión SSH activa se mantuvo, pero al intentar abrir una nueva, fue imposible conectar.

Esta secuencia demostró de forma práctica y contundente que las **reglas de firewall son los porteros de la red**. Sin ellas, aunque los cables virtuales estén conectados, no pasa ningún tipo de tráfico que no esté explícitamente permitido.



![Screenshot From 2025-10-17 12-41-28.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2012-41-28.png)

---

## Comparación Rápida: Google Cloud (GCP) vs. Amazon Web Services (AWS)

Como alguien interesado en el mundo cloud, es inevitable comparar. Aquí una tabla sencilla de los servicios que usé y sus contrapartes en AWS.

| Concepto / Servicio      | Google Cloud Platform (GCP)     | Amazon Web Services (AWS)       | Mi Observación Personal                                                                                                                                                                                  |
|:------------------------ |:------------------------------- |:------------------------------- |:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Nube Privada Virtual** | **VPC (Virtual Private Cloud)** | **VPC (Virtual Private Cloud)** | El nombre es el mismo, pero una gran diferencia es que las VPC de GCP son **globales** por defecto, mientras que en AWS están **atadas a una región**.                                                   |
| **Máquinas Virtuales**   | **Compute Engine**              | **EC2 (Elastic Compute Cloud)** | Son el corazón de IaaS en ambas nubes. La experiencia de creación es muy similar.                                                                                                                        |
| **Firewall de Red**      | **Reglas de Firewall de VPC**   | **Security Groups y NACLs**     | Aquí AWS es un poco más granular. Los *Security Groups* actúan a nivel de instancia (como las reglas de GCP), mientras que las *NACLs* actúan a nivel de subred, ofreciendo una capa extra de seguridad. |
| **Subredes**             | **Subnets**                     | **Subnets**                     | El concepto es idéntico, son divisiones lógicas de la red para organizar los recursos.                                                                                                                   |

---

## Conclusiones Finales

Este laboratorio fue una introducción fantástica y muy práctica a los fundamentos de redes en la nube. La lección más importante que me llevo es que la conectividad no es magia; es una serie de reglas lógicas y explícitas que dictan quién puede hablar con quién y a través de qué puertos. Eliminar la red `default` al principio fue un paso clave para forzarme a entender y construir desde la base. ¡Una experiencia muy valiosa!
