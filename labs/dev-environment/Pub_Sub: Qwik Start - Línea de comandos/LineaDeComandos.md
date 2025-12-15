# 📄 Documentación del Lab: GSP095 - Pub/Sub: Qwik Start (Línea de Comandos)

## 🎯 Objetivo del Laboratorio

El objetivo de este laboratorio es aprender a gestionar el ciclo de vida completo (crear, listar, eliminar) de **Temas (Topics)** y **Suscripciones (Subscriptions)** de Pub/Sub usando la **línea de comandos (`gcloud`)**. Además, se explora en detalle el comportamiento del comando `pull` (extracción de mensajes), incluyendo la extracción de mensajes uno por uno y en lotes.

---

## 🛠️ Comandos Clave Utilizados

Este laboratorio se centra en el conjunto de comandos `gcloud pubsub`:

| **Comando**                                                       | **Propósito en el Lab**                             |
| ----------------------------------------------------------------- | --------------------------------------------------- |
| `gcloud pubsub topics create [TEMA]`                              | Crea un nuevo tema.                                 |
| `gcloud pubsub topics list`                                       | Muestra todos los temas en el proyecto.             |
| `gcloud pubsub topics delete [TEMA]`                              | Elimina un tema.                                    |
| `gcloud pubsub subscriptions create --topic [TEMA] [SUSCRIPCIÓN]` | Crea una suscripción y la vincula a un tema.        |
| `gcloud pubsub topics list-subscriptions [TEMA]`                  | Muestra todas las suscripciones de un tema.         |
| `gcloud pubsub subscriptions delete [SUSCRIPCIÓN]`                | Elimina una suscripción.                            |
| `gcloud pubsub topics publish [TEMA] --message "..."`             | **Publica** un mensaje en un tema.                  |
| `gcloud pubsub subscriptions pull [SUSCRIPCIÓN] --auto-ack`       | **Extrae (consume)** un mensaje de una suscripción. |
| `gcloud pubsub subscriptions pull ... --limit=N`                  | Extrae un **lote** de N mensajes.                   |

---

## ✅ Resumen de Tareas Realizadas

1. **Gestión de Temas (Topics):**
   
   - Se creó el tema principal `myTopic`.
   
   - Se crearon dos temas temporales (`Test1`, `Test2`) para practicar.
   
   - Se listaron (`gcloud pubsub topics list`) y luego se eliminaron (`gcloud pubsub topics delete`) los temas temporales.

2. **Gestión de Suscripciones (Subscriptions):**
   
   - Se creó la suscripción principal `mySubscription` y se vinculó (`--topic`) a `myTopic`.
   
   - Se crearon dos suscripciones temporales (`Test1`, `Test2`), también vinculadas a `myTopic`.
   
   - Se listaron (`gcloud pubsub topics list-subscriptions myTopic`) y luego se eliminaron (`gcloud pubsub subscriptions delete`) las suscripciones temporales.

3. **Publicar y Extraer (Uno por Uno):**
   
   - Se publicaron 4 mensajes diferentes en `myTopic` usando el comando `gcloud pubsub topics publish ...`.
   
   - Se ejecutó `gcloud pubsub subscriptions pull mySubscription --auto-ack`.
   
   - **Observación Clave:** Solo se recibió **un mensaje** (el primero).
   
   - Se tuvo que ejecutar el mismo comando `pull` 3 veces más para recibir los 3 mensajes restantes, uno por cada ejecución.
   
   - Al ejecutarlo una 5ª vez, la terminal mostró "Listed 0 items.", confirmando que la cola estaba vacía.

4. **Publicar y Extraer (en Lote):**
   
   - Se publicaron 3 nuevos mensajes en `myTopic`.
   
   - Se usó el flag --limit=3 para extraer todos los mensajes en una sola solicitud:
     
     gcloud pubsub subscriptions pull mySubscription --limit=3
   
   - Esto confirmó la forma eficiente de consumir mensajes en lote.

---

## 💡 Conceptos Clave Aprendidos

- **Gestión por CLI:** El conjunto de comandos `gcloud pubsub` permite administrar todo el servicio de Pub/Sub (temas y suscripciones) sin necesidad de entrar a la consola gráfica.

- **Comportamiento de `pull` (Lo más importante):**
  
  - **Extracción Unitaria:** Por defecto, `gcloud pubsub subscriptions pull` está diseñado para extraer **un solo mensaje** a la vez. Esto simula cómo un trabajador (worker) procesaría tareas una por una.
  
  - **`--auto-ack` (Confirmación Automática):** Este *flag* es fundamental. El "ack" (acknowledgement) es la señal que el consumidor le envía a Pub/Sub para decirle "Recibí y procesé este mensaje, puedes borrarlo de la cola". Sin el `ack`, Pub/Sub asumiría que el mensaje falló y lo volvería a entregar. `--auto-ack` lo hace por nosotros en la CLI.
  
  - **`--limit=N` (Extracción en Lote):** Este *flag* es el método preferido para aplicaciones reales, ya que permite a un consumidor solicitar un *lote* de mensajes (ej. 100 a la vez), procesarlos y luego pedir más, lo cual es mucho más eficiente.


