# Mi Experiencia Práctica: Conectando Compute Engine, Cloud SQL y Cloud Storage en GCP

Un laboratorio mas **"Aspectos básicos de Google Cloud: Introducción a Cloud Storage y Cloud SQL"**. Más que seguir un simple tutorial, fue una sesión de resolución de problemas en tiempo real que solidificó mi comprensión de cómo interactúan los servicios fundamentales de GCP para dar vida a una aplicación web.

A continuación, comparto mi bitácora personal de este recorrido, incluyendo los desafíos que encontré y cómo los resolví.

## Tarea 1 & 2: Despliegue del Servidor Web (Compute Engine)

El punto de partida fue crear una máquina virtual en **Compute Engine** para alojar un blog simple con Apache y PHP. La configuración inicial fue rápida, utilizando un *script de inicio* para automatizar la instalación del software.

```
# Script de inicio para la VM bloghost
apt-get update
apt-get install apache2 php php-mysql -y
service apache2 restart
```

**Spoiler:** Este script falló silenciosamente, algo que descubriría más tarde y que se convirtió en un excelente punto de aprendizaje.

## Tarea 3: Creación de un Bucket (Cloud Storage)

Para los archivos estáticos (la imagen del banner), utilicé **Cloud Storage**. En lugar de la interfaz gráfica, opté por la línea de comandos en Cloud Shell, una práctica mucho más eficiente y escalable.

```
# 1. Crear el bucket en la ubicación deseada
gcloud storage buckets create -l US gs://$DEVSHELL_PROJECT_ID

# 2. Subir la imagen al bucket
gcloud storage cp my-excellent-blog.png gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png

# 3. Hacer el objeto públicamente legible
gsutil acl ch -u allUsers:R gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png
```

Con esto, obtuve una URL pública para la imagen, lista para ser usada en la web.

![Screenshot From 2025-10-17 16-44-48.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2016-44-48.png)

## Tarea 4: Configuración de la Base de Datos (Cloud SQL)

Aquí es donde la experiencia se volvió más interesante. Configuré una instancia de **Cloud SQL** para MySQL y me enfrenté a varios desafíos comunes.

#### Desafío #1: Encontrar la "Zona de pruebas"

Las instrucciones mencionaban una "Zona de pruebas", pero la interfaz mostraba opciones como "Production" y "Sandbox".

Solución: Rápidamente identifiqué que "Sandbox" era la opción correcta, ideal para entornos de desarrollo y pruebas.

![Screenshot From 2025-10-17 16-45-50.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2016-45-50.png)

![Screenshot From 2025-10-17 16-47-12.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2016-47-12.png)

#### Desafío #2: No me dejaba guardar la configuración de red

Al intentar autorizar la IP de mi VM, el botón "Guardar" no funcionaba.

Solución: El truco estaba en un clic intermedio. Después de ingresar la IP, era necesario presionar el botón "Listo" (Done) antes de poder guardar la configuración general. Un pequeño detalle de la UI que es fácil pasar por alto.

![Screenshot From 2025-10-17 17-12-28.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2017-12-28.png)

## Tarea 5 & 6: Conectando las Piezas y Depurando

Con la infraestructura lista, accedí a la VM por SSH para desplegar el código.

#### Desafío #3: `apache2.service not found`

Al intentar reiniciar el servidor web, la terminal me devolvió un error.

Solución: El script de inicio había fallado. Lejos de ser un problema, fue una oportunidad para depurar. Ejecuté la instalación manualmente, solucionando el problema de raíz.

```
# Instalación manual tras el fallo del script de inicio
sudo apt-get update
sudo apt-get install apache2 php php-mysql -y
sudo service apache2 restart
```

![Screenshot From 2025-10-17 17-20-38.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2017-20-38.png)

#### El Código Final

Finalmente, edité el archivo `index.php` para conectar todas las piezas: la IP de la instancia de **Cloud SQL** y la URL de la imagen en **Cloud Storage**.

![Screenshot From 2025-10-17 17-29-54.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2017-29-54.png)

![Screenshot From 2025-10-17 17-28-14.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2017-28-14.png)

```
<html>
<head><title>Welcome to my excellent blog</title></head>
<body>

<!-- Imagen servida desde Cloud Storage -->
<img src='[https://storage.googleapis.com/](https://storage.googleapis.com/)[TU_ID_DE_PROYECTO]/my-excellent-blog.png'>

<h1>Welcome to my excellent blog</h1>

<?php
 // Conexión a Cloud SQL
 $dbserver = "[IP_PUBLICA_DE_CLOUDSQL]";
 $dbuser = "blogdbuser";
 $dbpassword = "[TU_CONTRASEÑA]";

 try {
  $conn = new PDO("mysql:host=$dbserver;dbname=mysql", $dbuser, $dbpassword);
  echo "Connected successfully";
 } catch(PDOException $e) {
  echo "Database connection failed: " . $e->getMessage();
 }
?>
</body></html>
```

![Screenshot From 2025-10-17 17-31-51.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2017-31-51.png)

## ¡El Resultado Final!

Al recargar la IP de mi VM en el navegador, el resultado fue un éxito. La página mostró la imagen servida desde **Cloud Storage** y el mensaje de conexión exitosa a **Cloud SQL**.

![Screenshot From 2025-10-17 17-35-53.png](/home/christhianrodriguez/Pictures/Screenshots/Screenshot%20From%202025-10-17%2017-35-53.png)

## Comparativa Rápida: GCP vs. AWS

Para contextualizar, así se traducen estos servicios a sus equivalentes en Amazon Web Services:

| **Servicio de Google Cloud (GCP)** | **Servicio de Amazon Web Services (AWS)**    | **Propósito**                                      |
| ---------------------------------- | -------------------------------------------- | -------------------------------------------------- |
| **Compute Engine (GCE)**           | **Amazon EC2** (Elastic Compute Cloud)       | Servidores virtuales para ejecutar aplicaciones.   |
| **Cloud SQL**                      | **Amazon RDS** (Relational Database Service) | Bases de datos relacionales administradas.         |
| **Cloud Storage (GCS)**            | **Amazon S3** (Simple Storage Service)       | Almacenamiento de objetos para archivos estáticos. |

## Conclusión

Este lab fue una excelente demostración práctica de una arquitectura web de 3 capas. Más allá de solo desplegar servicios, la verdadera lección estuvo en **configurar la conectividad, asegurar las conexiones y depurar problemas** del mundo real. Una base sólida y una gran experiencia para cualquier proyecto futuro en la nube.

Recientemente completé un laboratorio práctico de Google Cloud que simula el despliegue de una aplicación web de 3 capas. El objetivo era construir una aplicación web funcional desde cero, integrando los servicios fundamentales de cómputo, almacenamiento y bases de datos de GCP.

Esta experiencia me permitió conectar la teoría con la práctica, configurando la conectividad de red y los permisos entre servicios dispares para crear una solución unificada.

A continuación, detallo el proceso y las tecnologías que utilicé.
