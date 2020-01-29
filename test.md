### Active MQ

Active MQ es un broker de mensajería, utiliza estándar JMS, para la validación y manejo de mensajes y el propósito del broker es recibir los mensajes entrantes desde aplicaciones y distribuirlos a los consumidores suscritos. 

Esto trae ventajas como la comunicación asincronica , disminuye el grado de interdependencia entre los servicios, si bien es un producto hecho en java, puede ser utilizado por varias tecnologias distintas,  etc.



Existen dos maneras de obtener y distribuir un mensaje en MQ, mediante ***colas o tópicos.***

 

![1580273092691](https://i.imgur.com/Awm38TO.png)

  

- Topicos

Son básicamente implementaciones de pub/sub. Cuando se envía un mensaje a un tópico, este se distribuye a la totalidad de los consumidores suscriptos en ese momento a ese tópico, pueden ser cero o n.

  

![1580273405013](https://i.imgur.com/oG2oCJN.png)

- Colas

 Las colas amq usan una semántica de balanceador de carga, cuando un producer deja un mensaje en una cola, aunque esa cola tenga muchos consumidores, el mensaje llegara al primero que lo tome y solo a ese. La relación es 1 a 1. si no hay consumidores de esa cola, el mensaje persistirá en el amq hasta tanto exista 1 suscriptor.

![1580273422530](https://i.imgur.com/qMEp4kl.png)





El producto que utilizamos como broker de mensajeria sobre el PaaS es  activeMQ de redhat. tenemos un template en [este link](https://github.bancogalicia.com.ar/devops-master/pom/blob/master/commons/amq/amq-app-persistent.yml)

para utilizarlo solo basta con copiarlo y pegarlo en la consola del proyecto desde el menu "*import YAML/JSON..*" o desde oc:

```bash
oc create -f amq-app-persistent.yml
```

Este template crea un amq que contiene un volumen persistente de 1gb ( alcanza y sobra para el nivel de mensajes actuales ya que los mismos una vez que son tomados por el consumidor se borran de la persistencia)

La definicion de los nombres de colas o topicos se realiza desde el deploy broker-amq, las mismas se pueden asignar con la siguiente variables de entorno ( en formato separado por comas):

AMQ_TOPICS 

AMQ_QUEUES



