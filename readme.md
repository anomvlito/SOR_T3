# Parte 1

## 1. ¿Cuál es el largo en bits de la dirección IP de destino?

DST IP: 136.155.0.2, toda dirección IPv4 se representa con 32 bits (4 bytes).

## 2. ¿Cuál es la dirección IP de origen cuando el paquete se encuentra en el router central derecho y el último dispositivo visitado es el router gateway de la red Casa de Alice?

La dirección IP de origen es SRC IP: 190.190.1.2, la cual es al ip asignada anteriormente al Router Gateway, asi que si proviene de ahí.

## 3. ¿Cuál es la dirección IP de origen cuando el paquete se encuentra en el router central izquierdo y el último dispositivo visitado es el router gateway de la red DNS?

SRC IP: 190.190.1.2

La dirección IP de origen es 190.190.1.2, ya que el paquete aún mantiene como dirección ip de origen la del Router Gateway Casa Alice. Aunque el paquete viene de pasar por el Router Gateway DNS, eso no modifica el campo “SRC IP” del paquete.

## 4. Describa, en orden y separado por capas de entrada y salida, todo lo que ocurre con el paquete cuando este se encuentra en el servidor de la red DNS y el último dispositivo visitado es el router gateway de la red DNS.

En la entrada, el paquete llega al servidor DNS desde el router gateway de la red DNS. En la capa de enlace de datos (Ethernet II), la dirección MAC de origen es 0010.11C6.D1AA (router) y la de destino es 0060.5C2E.2E95 (servidor). En la capa de red (IP), la dirección IP de origen es 190.190.1.2 (PC de Alice) y la de destino es 136.155.0.2 (DNS). El TTL es 251, el protocolo es 0x01 (ICMP) y se trata de un paquete tipo 0x08 (Echo Request).

En la salida, el servidor DNS genera la respuesta. En la capa de enlace de datos, la dirección MAC de origen pasa a ser 0060.5C2E.2E95 (servidor) y la de destino es 0010.11C6.D1AA (router). En la capa de red, la IP de origen ahora es 136.155.0.2 (DNS) y la de destino es 190.190.1.2 (PC de Alice). El TTL se reinicia en 128, el protocolo se mantiene como ICMP (0x01) y el tipo de paquete ahora es 0x00 (Echo Reply).

# Parte 2: Ahora active todos los paquetes IPv4, ademas del HTTP y TCP, y desde el escritorio de la red de Casa de Alice conectese a la pagina de DCClubPenguin, luego responda las siguientes preguntas:

## 1. ¿Cuál es el largo en bytes del HTTP Request del paquete HTTP? (1 punto)

HTTP Request = 130 - 20 (IP) - 20 (TCP) = 90 bytes

## 2. Describa qué tipos de paquetes se están usando, es decir, indique qué tipo de paquete es, por qué se usan y qué deben contener. (3 puntos)

Los paquetes usados son:

ICMP se usa inicialmente para verificar conectividad entre dispositivos mediante mensajes tipo ping. Estos paquetes contienen información mínima, como tipo, código, identificador, número de secuencia y datos opcionales, y permiten confirmar que el destino está disponible.

TCP se utiliza para establecer una conexión confiable entre el cliente, en este caso, el PC Casa Alice y el servidor web DCClubPenguin. Incluye campos como puerto origen y destino, número de secuencia, número de confirmación, banderas , ventana, etc. Este tipo de paquete garantiza que los datos lleguen completos y en orden.

HTTP es el protocolo de aplicación que permite la comunicación entre el navegador del cliente y el servidor web. Se encapsula dentro de TCP y contiene la solicitud HTTP , incluyendo headers, el recurso solicitado, el host, tipo de contenido aceptado y otros campos necesarios para recuperar la página web.

## 3. Describa de forma ordenada qué rutas toman los paquetes descritos en la pregunta anterior (especificar por dónde pasan y en qué orden). (4 puntos)

La ruta seguida por los paquetes TCP y HTTP desde la PC de la red Casa Alice hasta el servidor Club Penguin es la siguiente: PC Casa Alice, Switch Casa Alice, Router Gateway Casa Alice, Router Rama Derecha, Router Rama Izquierda, Router Gateway DNS, Router Rama Izquierda, Router Gateway Club Penguin, Switch Club Penguin, Server Club Penguin. Esta ruta es utilizada tanto para los paquetes TCP, encargados de establecer la conexión fiable entre cliente y servidor, como para los paquetes HTTP, que transportan la solicitud GET del navegador y la respuesta del servidor.

## 4. (Desde Casa de Bob) Observe qué paquetes se están usando y qué rutas toman estos paquetes. Luego, describa las diferencias y similitudes entre este proceso y el proceso analizado anteriormente para Alice. (4 puntos)

Durante el intento de conexión del PC de Bob al servidor DCClubPenguin se observa que se utilizan los siguientes tipos de paquetes: DNS, TCP, ICMP y HTTP. La secuencia comienza con solicitudes DNS, necesarias para resolver el nombre del servidor DCClubPenguin a una dirección IP. Luego, se establece la conexión mediante TCP, específicamente con el protocolo de control de transmisión para garantizar la entrega ordenada de los datos. Se utiliza también ICMP, que puede aparecer como respuesta de error o de diagnóstico. Finalmente, se intenta establecer comunicación con HTTP, pero esta es rechazada por una lista de control de acceso configurada.

En cuanto a la ruta de los paquetes, siguen el mismo camino que en el caso de Alice: desde el PC de Bob, pasando por el switch y el router gateway de la red Casa Bob, luego a través del router central derecho, router central izquierdo, y hacia la red Club Penguin. Sin embargo, en este caso, al llegar al router gateway de Club Penguin, los paquetes HTTP provenientes de Bob son denegados por una ACL (lista de control de acceso), tal como estaba especificado en la configuración del router. Esto impide que el servidor procese la solicitud de Bob.

La principal similitud con el proceso de Alice es que ambos recorren la misma infraestructura de red, utilizan los mismos protocolos y siguen el mismo flujo de paquetes. La diferencia clave es que Alice logra completar la comunicación HTTP y recibir respuesta del servidor, mientras que Bob es bloqueado al llegar a Club Penguin, cumpliéndose así el requisito de que solo en esa subred se le restrinja el acceso HTTP.
