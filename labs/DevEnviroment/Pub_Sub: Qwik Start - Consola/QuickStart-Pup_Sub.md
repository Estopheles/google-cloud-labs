# 📄 Documentación del Lab: GSP096 - Pub/Sub: Qwik Start (Consola)

## 🎯 Objetivo del Laboratorio

El objetivo de este laboratorio es aprender los conceptos y el flujo de trabajo fundamentales del servicio de mensajería asíncrona **Pub/Sub**. Se utiliza la **Consola de Cloud** para configurar la infraestructura (Temas y Suscripciones) y **Cloud Shell** para simular un consumidor de mensajes.

---

## 💡 Conceptos Clave Aprendidos

Este laboratorio se centra en el modelo de **Publicador/Suscriptor**, que sirve para desacoplar servicios:

- **Tema (Topic):** Es el "canal" o punto de ingesta donde los **productores (publishers)** envían sus mensajes. No sabe (ni le importa) quién recibirá el mensaje.

- **Suscripción (Subscription):** Es el "buzón" que se conecta a un tema. Recibe una copia de todos los mensajes enviados a ese tema después de que la suscripción es creada. Los **consumidores (subscribers)** leen los mensajes desde la suscripción.

- **Desacoplamiento:** El productor (quien publica) y el consumidor (quien lee) **no se conocen entre sí**. El productor solo conoce el **Tema**, y el consumidor solo conoce la **Suscripción**. Esto permite que los servicios escalen y fallen de forma independiente.

- **Tipo de Entrega (Pull vs. Push):**
  
  - **Extracción (Pull):** El tipo usado en este lab. El servicio consumidor debe *solicitar* activamente los mensajes desde la suscripción.
  
  - **Empuje (Push):** El tipo alternativo. Pub/Sub *envía* (empuja) el mensaje a un *endpoint* (una URL o Webhook) tan pronto como lo recibe.

---

## ✅ Resumen de Tareas Realizadas

1. **Creación del Tema (Topic):**
   
   - Se navegó a la sección de **Pub/Sub** en la consola.
   
   - Se creó un nuevo **Tema** con el ID: `MyTopic`.
   
   - Este es el "canal" donde se publicarán los mensajes.

2. **Creación de la Suscripción (Subscription):**
   
   - Desde la página de `MyTopic`, se seleccionó la opción para crear una suscripción.
   
   - Se creó una **Suscripción** con el ID: `MySub`.
   
   - Se configuró el **Tipo de entrega** como **`Extracción` (Pull)**.
   
   - Esto "conectó" el buzón `MySub` al canal `MyTopic`.

3. **Publicación de un Mensaje (Simulando un Productor):**
   
   - Se regresó a la página de detalles del tema `MyTopic`.
   
   - Se seleccionó la pestaña **`Mensajes`**.
   
   - Se usó la función **`Publicar mensaje`** de la consola para enviar el texto "Hello World" al tema.

4. **Consumo del Mensaje (Simulando un Consumidor):**
   
   - **Importante:** Este paso se realizó en **Cloud Shell**, no en la consola.
   
   - Se ejecutó un comando de `gcloud` para actuar como un servicio consumidor que "extrae" mensajes de la suscripción `MySub`.
   
   - **Comando:** `gcloud pubsub subscriptions pull --auto-ack MySub`
   
   - **`--auto-ack`:** Este *flag* es clave. Le dice a Pub/Sub "Mensaje recibido y procesado correctamente" (ACKnowledgement) de forma automática. Sin el "ack", Pub/Sub pensaría que el mensaje no se procesó y lo intentaría entregar de nuevo.
   
   - **Resultado:** La terminal mostró el mensaje "Hello World" en el campo `DATA`.
