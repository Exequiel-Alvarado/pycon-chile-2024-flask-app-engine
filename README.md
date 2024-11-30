# Pycon Chile App Engine

**link url video demo**
https://drive.google.com/file/d/19r-9ZJXQ9SqrQaNW4TbvjeGAaoPVR7N3/view?usp=sharing

**Configuración en GCP**:

- Instala el Google Cloud SDK desde [https://cloud.google.com/sdk/docs/install](https://cloud.google.com/sdk/docs/install)
- Abre una terminal y ejecuta:
    
    ```bash
    gcloud init
    ```
    
- Selecciona o crea un proyecto nuevo
- Habilita App Engine para tu proyecto:
    
    ```bash
    gcloud app create
    ```
    
    - Selecciona la región donde quieres desplegar tu aplicación

**Despliegue de la aplicación**:

- Navega hasta el directorio de tu proyecto
- Ejecuta el comando de despliegue:
    
    ```bash
    gcloud app deploy
    ```
    

Este error es común y ocurre porque el servicio no tiene los permisos necesarios para crear y acceder al bucket de almacenamiento que App Engine.

```jsx
ERROR: (gcloud.app.deploy) Error Response: [13] Failed to create cloud build: com.google.net.rpc3.client.RpcClientException: <eye3 title='/ArgoAdminNoCloudAudit.CreateBuild, FAILED_PRECONDITION'/> APPLICATION_ERROR;google.devtools.cloudbuild.v1/ArgoAdminNoCloudAudit.CreateBuild;invalid bucket "staging.windy-elevator-435314-j4.appspot.com"; service account windy-elevator-435314-j4@appspot.gserviceaccount.com does not have access to the bucket;AppErrorCode=9;StartTimeMs=1732975249839;unknown;ResFormat=uncompressed;ServerTimeSec=0.666853241;LogBytes=256;Non-FailFast;EndUserCredsRequested;EffSecLevel=privacy_and_integrity;ReqFormat=uncompressed;ReqID=dc5d0bfb2cc657f;GlobalID=0;Server=[2002:a05:6132:131e:b0:401:15c5:fed3]:4001.
```

Necesitas habilitar las APIs necesarias:

```bash
gcloud services enable cloudbuild.googleapis.com
gcloud services enable cloudresourcemanager.googleapis.com
gcloud services enable compute.googleapis.com
```

Espera unos minutos para que los permisos se propaguen y luego intenta el despliegue nuevamente:

```bash
gcloud app deploy
```

Para ver tu aplicación corriendo en el navegador web

```bash
gcloud app browse
```

(otra terminal) Para ver los logs desde la linea de comando:

```bash
gcloud app logs tail -s default
```
