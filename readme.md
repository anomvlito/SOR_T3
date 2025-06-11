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

## 2. Describa qué tipos de paquetes se están usando, es decir, indique qué tipo de paquete es, por qué se usan y qué deben contener. (3 puntos)

## 3. Describa de forma ordenada qué rutas toman los paquetes descritos en la pregunta anterior (especificar por dónde pasan y en qué orden). (4 puntos)

## 4. (Desde Casa de Bob) Observe qué paquetes se están usando y qué rutas toman estos paquetes. Luego, describa las diferencias y similitudes entre este proceso y el proceso analizado anteriormente para Alice. (4 puntos)
