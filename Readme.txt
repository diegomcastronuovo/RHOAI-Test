Este Pipeline ejecuta lo siguiente:

1.- Toma un archivo "credidcard.csv"
https://drive.google.com/file/d/1wyuP1YYijvvk8R5ibpi7zy0ujbndnBqy/view?usp=sharing


2.- Prepara los datos
3.- Entrena un modelo
4.- Pone el modelo en una carpeta para ser desplegado


Usa los siguientes buckets en AWS:
Region: us-east-1
Bucket: semper-pipelines
Carpeta destino del modelo: /data
Nombre del modelo para desplegar model-final.onnx

---------------------------------------------------------------------

Armar los siguientes S3 en AWS:

semper-wb
semper-pipelines

poner credit-card.csv en la raíz del S3 semper-pipelines
Dentro de semper-pipelines armar una carpeta llamada "data"

---------------------------------------------------------------------

Armar las conexiones a ambos S3

Para WB:
http://s3.amazonaws.com/semper-wb

Para Pipelines:
Endpoint: s3://semper-pipelines.s3.us-east-1.amazonaws.com
Bucket: semper-pipelines

Armar una tercer conexión para el Model Server, en el Endpoint poner:
https://s3.amazonaws.com/
bucket: semper-pipelines en su propio campo

----------------------------------------------------------------------

Para el Deploy Model:
Armar un Model Server  
Framework: onnx-1
Existing Data Connection: la que armamos arriba para el Model Server
Path: data/model-final.onnx

----------------------------------------------------------------------

Armar el Workbench:

Small con Tensorflow y conectarlo a semper-wb

Agregar una variable de entorno (config map --> Key/Value)

PIPELINES_SSL_SA_CERTS
/var/run/secrets/kubernetes.io/serviceaccount/ca.crt


