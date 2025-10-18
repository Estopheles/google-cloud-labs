# Mi Informe del Laboratorio: "Primeros Pasos con Google Cloud Marketplace"

En este informe, quiero resumir mi experiencia y los conocimientos que adquirí durante el laboratorio, enfocado en desplegar mi primera solución desde Google Cloud Marketplace.

## ¿Qué Hice? Resumen de Mi Experiencia

Mi objetivo en este laboratorio fue implementar un entorno de servidor web completo (una pila LAMP) de la manera más rápida y eficiente posible. Para lograrlo, estos fueron los pasos que seguí:

1. **Acceso al Entorno de Laboratorio:** Primero, inicié sesión en la Consola de Google Cloud con las credenciales temporales que me dieron.

2. **Navegación a Cloud Marketplace:** Desde el menú principal de la consola, me dirigí a **Marketplace**, que es el catálogo de aplicaciones y servicios de Google Cloud.
   
   ![Screenshot From 2025-10-15 12-16-43.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-15%2012-16-43.png)
   
   ![Screenshot From 2025-10-15 12-16-58.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-15%2012-16-58.png)

3. **Búsqueda de la Solución:** En la barra de búsqueda de Marketplace, escribí "LAMP" y elegí la solución específica **"LAMP Stack by Google Click to Deploy"**.
   
   **Configuración de la Implementación:** Hice clic en "COMENZAR" y configuré los parámetros básicos para mi servidor:

4. - **Nombre de la implementación:** Dejé el que venía por defecto, `lamp-1`.
   
   - **Zona:** Seleccioné la zona que me asignó el laboratorio.
   
   - **Tipo de máquina:** Configuré la serie a **E2** y el tipo a **e2-medium**. Con esto, definí los recursos de CPU y RAM que tendría mi máquina virtual.
   
   ![Screenshot From 2025-10-15 12-10-56.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-15%2012-10-56.png)
   
   ![Screenshot From 2025-10-15 12-12-05.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-15%2012-12-05.png)

5. **Despliegue de la Pila LAMP:** Acepté los términos y lancé la implementación. En ese momento, Google Cloud se encargó de todo el trabajo pesado por mí:
   
   - Creó una nueva máquina virtual en **Compute Engine**.
   
   - Instaló el sistema operativo Linux.
   
   - Instaló y configuró el servidor web Apache, la base de datos MySQL y el intérprete de PHP.
   
   Aquí puedes poner tu captura de pantalla del proceso de despliegue.
   
   [Imagen mostrando el mensaje "Se está implementando lamp-1..."]

6. **Verificación Final:** Una vez que todo terminó, la plataforma me mostró los detalles de la instancia, incluyendo la **URL del sitio** (la IP pública del servidor). Hice clic en el enlace y, al ver la página de bienvenida en mi navegador, confirmé que todo había funcionado a la perfección.
   
   ![Screenshot From 2025-10-15 12-14-06.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-15%2012-14-06.png)
   
   ![Screenshot From 2025-10-15 12-16-04.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-15%2012-16-04.png)
   
   
   
   ## ¿Qué Aprendí? Mis Conclusiones Clave

Este laboratorio me pareció una introducción muy práctica a varios conceptos fundamentales de Google Cloud. Esto es lo que me llevo:

- **El Poder de Google Cloud Marketplace:** Mi primera impresión es que Marketplace es una herramienta de productividad increíble. Me permitió desplegar una solución de software compleja, que a mano me hubiera llevado horas, en solo unos minutos.

- **¿Qué es una Pila LAMP?:** Ahora entiendo mejor qué es "LAMP": el acrónimo de **L**inux, **A**pache, **M**ySQL y **P**HP. Juntos, forman la base para muchísimos sitios y aplicaciones web.

- **Comparación con AWS:** Este concepto de "tienda de aplicaciones" no es exclusivo de Google. Por ejemplo, **Amazon Web Services (AWS) tiene su propio AWS Marketplace**. El objetivo es el mismo: simplificar el despliegue de software usando imágenes preconfiguradas (en AWS se llaman AMIs o *Amazon Machine Images*). La gran lección para mí es que, aunque cada nube tiene sus propias herramientas, el principio de automatizar y simplificar la infraestructura es un estándar en la industria. Saber usar Marketplace en GCP me da una idea clara de cómo funcionan servicios similares en otras nubes.

- **Infraestructura como Servicio (IaaS) en Acción:** Aunque todo fue muy automático, tuve que tomar decisiones sobre la infraestructura. Al elegir el tipo de máquina (`e2-medium`) y la `zona`, estuve interactuando directamente con **Compute Engine**, el servicio IaaS de Google. Esto me demostró lo fácil que es "alquilar" poder de cómputo a la medida.

- **La Importancia de las IP Públicas:** Comprendí que para que un servicio sea visible en Internet, es indispensable una dirección IP pública. Marketplace no solo la asignó, sino que también configuró las reglas de firewall para que mi servidor pudiera recibir visitas.

En resumen, este laboratorio me enseñó cómo puedo **aprovechar soluciones preconfiguradas para desplegar infraestructura de forma rápida y segura**, un pilar de la agilidad que busco al aprender sobre la nube.
