# Reporte de Laboratorio: Introducción a Google Cloud KMS

**Autor:** [Tu Nombre]

**Fecha:** 28 de Noviembre, 2025

**Laboratorio:** GSP079 - Empieza a usar Cloud KMS

## 1. Resumen Ejecutivo y Objetivos

El objetivo de este laboratorio fue implementar un sistema de encriptación de datos utilizando **Google Cloud Key Management Service (KMS)**. En lugar de confiar en la encriptación transparente predeterminada de Google, realizamos una **encriptación del lado del cliente (Client-side encryption)** manual interactuando directamente con la API de KMS.

**Lo que logramos:**

1. Crear una infraestructura de llaves segura (KeyRing y CryptoKey).

2. Encriptar datos sensibles (correos electrónicos) antes de subirlos a la nube.

3. Administrar permisos de acceso (IAM) separando roles de administración y uso.

4. Auditar quién accedió a las llaves y cuándo.

## 2. Conceptos de Seguridad Aplicados

Para entender los comandos utilizados, es necesario definir los conceptos base:

- **Cloud KMS (Key Management Service):** Es el servicio que custodia las llaves criptográficas. Nos permite generar, usar, rotar y destruir llaves.
  
  - *¿Por qué usarlo?* Para cumplir con regulaciones bancarias o de salud que exigen que nosotros (y no Google) controlemos las llaves.

- **KeyRing (Llavero):** Es una agrupación lógica. Las llaves no pueden existir "flotando", deben vivir dentro de un Llavero (ej. Llavero de Finanzas, Llavero de RRHH).

- **CryptoKey:** Es la llave real que se usa para encriptar.

- **Base64:** Es un sistema de codificación.
  
  - *El problema:* La encriptación convierte texto en datos binarios (bytes ilegibles). Las APIs web (JSON) no entienden binario.
  
  - *La solución:* Usamos Base64 para traducir esos datos binarios a caracteres seguros (letras y números) para que puedan viajar por internet sin corromperse.

- **IAM (Separación de Funciones):** El principio de *mínimo privilegio*. El administrador de las llaves no debería poder leer los datos encriptados, y el usuario de los datos no debería poder borrar las llaves.

## 3. Desarrollo del Laboratorio

### Paso 1: Preparación del Entorno

Creamos un Bucket de Cloud Storage para almacenar los datos y descargamos la data de muestra (Corpus de correos de Enron).

**Comandos clave:**

```
# Crear variable y bucket
BUCKET_NAME="${DEVSHELL_PROJECT_ID}-enron_corpus"
gsutil mb gs://${BUCKET_NAME}

# Descargar correo de muestra
gsutil cp gs://enron_emails/allen-p/inbox/1. .
```

> **Evidencia:** Configuración inicial y descarga de datos.
> 
> ![2025-11-28 17.49.53 console.cloud.google.com 9793011c766d.png](Fotos/56a653c8a076b614c4d1b5571e9045895d1c8d62.png)

### Paso 2: Creación de Infraestructura KMS

Habilitamos la API y creamos la jerarquía de seguridad: `KeyRing` -> `CryptoKey`.

**Comandos clave:**

```
# Crear el Llavero (KeyRing)
gcloud kms keyrings create test --location global

# Crear la Llave (CryptoKey) dentro del llavero
gcloud kms keys create qwiklab --location global \
      --keyring test \
      --purpose encryption
```

### Paso 3: Encriptación Manual (Interacción con API)

Este fue el paso crítico. Simulamos cómo una aplicación enviaría datos a KMS para ser encriptados.

1. Tomamos el texto plano.

2. Lo convertimos a **Base64**.

3. Lo enviamos a la API de KMS usando `curl`.

4. Recibimos la respuesta (JSON) y extrajimos el texto cifrado.

**Comando de encriptación:**

```
curl -v "[https://cloudkms.googleapis.com/v1/projects/$DEVSHELL_PROJECT_ID/...:encrypt](https://cloudkms.googleapis.com/v1/projects/$DEVSHELL_PROJECT_ID/...:encrypt)" \
  -d "{\"plaintext\":\"$PLAINTEXT\"}" \
  ... \
| jq .ciphertext -r > 1.encrypted
```

> **Evidencia:** Ejecución del comando `curl` y respuesta de la API con el `ciphertext`.
> 
> ![2025-11-28 17.50.08 console.cloud.google.com e149adcd5694.png](Fotos/56b86ab1e4aec4e35aec5edd86d68739c67c0501.png)

(Opcional) Verificación de desencriptado:

Podemos confirmar que el proceso funciona a la inversa, recuperando el mensaje original.

> **Evidencia:** Mensaje original recuperado (West Position).
> 
> ![2025-11-28 17.50.27 console.cloud.google.com 35066ef18b6d.png](Fotos/32e40876a7315ba008daa278c827e292ac9a637d.png)

### Paso 4: Gestión de Identidad y Accesos (IAM)

Aplicamos el principio de seguridad de separación de permisos. Asignamos roles específicos a nuestra cuenta.

- **Role Admin:** `roles/cloudkms.admin` (Puede crear/borrar llaves).

- **Role Encrypter:** `roles/cloudkms.cryptoKeyEncrypterDecrypter` (Puede usar las llaves).

**Comando clave:**

```
gcloud kms keyrings add-iam-policy-binding $KEYRING_NAME \
    --location global \
    --member user:$USER_EMAIL \
    --role roles/cloudkms.cryptoKeyEncrypterDecrypter
```

> **Evidencia:** Asignación de permisos IAM en la terminal.
> 
> ![2025-11-28 17.52.51 console.cloud.google.com 05625f059251.png](Fotos/deabb85068eef3238fd599117b86b8a50f095524.png)

### Paso 5: Automatización y Respaldo Masivo

En un entorno real, no encriptamos archivo por archivo. Usamos scripts. Creamos un script en Bash que recorrió todos los correos de la carpeta, los encriptó uno por uno y los subió al bucket seguro.

> **Evidencia:** Script ejecutándose en la terminal (loop de encriptación).
> 
> ![2025-11-28 17.55.02 console.cloud.google.com e8a21edad7b7.png](Fotos/977b2c1614ac64d940d241e0dde2e17002df5842.png)

Resultado Final:

Los archivos en el bucket de Cloud Storage ahora son ilegibles para cualquier persona que no tenga acceso a las llaves de KMS, garantizando la confidencialidad.

> **Evidencia:** Bucket de Cloud Storage con archivos `.encrypted`.
> 
> ![2025-11-28 17.56.07 console.cloud.google.com dcaab5b32406.png](Fotos/ff8e4558b389625ebb2731f39d0b0108a3b9796c.png)

### Paso 6: Auditoría y Cumplimiento

Finalmente, verificamos los **Cloud Audit Logs**. Esto es crucial para la seguridad: permite saber *quién* usó las llaves y *cuándo*.

Vimos los registros de creación del KeyRing y de las CryptoKeys.

> **Evidencia:** Explorador de Logs mostrando la creación de la CryptoKey.
> 
> ![2025-11-28 18.02.29 console.cloud.google.com accc820236d5.png](Fotos/68b2f673af3900047998b4a0670589fddb7ca666.png)

> **Evidencia:** Explorador de Logs mostrando actividad del KeyRing.
> 
> ![2025-11-28 18.04.02 console.cloud.google.com 9e699441d419.png](Fotos/212243c1922cfc1163829fa69499de3e690c3983.png)
> 
> 

## 4. Conclusión

Este laboratorio demostró cómo **Google Cloud KMS** permite desacoplar los datos de las llaves de seguridad. Aunque la interacción manual vía API (`curl`) es compleja y propensa a errores, ilustra el flujo real que seguiría una aplicación backend utilizando las librerías cliente (SDKs) de Google Cloud.

La implementación exitosa de IAM y los registros de auditoría aseguran que el sistema no solo es seguro criptográficamente, sino también robusto en términos de gobernanza y control de acceso.
