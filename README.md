# Práctica MQTT con ESP32 y Mosquitto

## Descripción

López Ramos Marcos Isaid - 2023630251

En esta práctica se realizó la implementación de una comunicación usando el protocolo MQTT dentro de una arquitectura IoT. Se utilizó una ESP32 como dispositivo publisher para enviar mensajes y una computadora con Mosquitto funcionando como broker. También se utilizó la misma computadora como subscriber para verificar la recepción de los mensajes debido a la falta de una RaspBerry pi como se solicitó en la práctica.

## Arquitectura

ESP32 (Publisher) → Mosquitto (Broker en laptop) → Subscriber (Laptop)

## Instalación

### Mosquitto (Broker)

1. Se instaló Mosquitto en la computadora.
2. Se creó un archivo de configuración llamado **mosquitto.conf** con el siguiente contenido:

listener 1883
allow_anonymous true

3. Se ejecutó Mosquitto con el siguiente comando:

mosquitto -c mosquitto.conf -v

**Nota:** En algunos casos es necesario agregar Mosquitto al PATH del sistema para poder ejecutar el comando desde cualquier terminal.

### ESP32

1. Se instaló Arduino IDE.
2. Se agregó el soporte para ESP32 desde el Boards Manager.
3. Se instaló la librería **PubSubClient**.
4. Se configuró la red WiFi (nombre y contraseña).
5. Se colocó la dirección IP de la computadora como broker MQTT.

**Nota:** La red WiFi utilizada debe ser de 2.4 GHz, ya que la ESP32 no es compatible con redes de 5 GHz.

## Ejecución

1. Ejecutar Mosquitto en una terminal:

mosquitto -c mosquitto.conf -v

2. Abrir otra terminal y ejecutar el subscriber:

mosquitto_sub -h 192.168.X.X -t iot/mensaje

(donde 192.168.X.X es la IP de la computadora que actúa como broker)

3. Subir el código a la ESP32 desde Arduino IDE y abrir el Monitor Serial.
4. Reiniciar la ESP32 y verificar en el Monitor Serial:

Conectando a WiFi...
WiFi conectado
Conectando MQTT...Conectado
Mensaje enviado

5. Observar en la terminal del subscriber la recepción de mensajes:

Hola desde ESP32
Hola desde ESP32

**Nota:** La ejecución del publisher se observa en el monitor serial de la ESP32, donde se muestra el envío periódico de mensajes hacia el broker MQTT.

## Resultados

Se logró establecer la comunicación correctamente utilizando MQTT. La ESP32 envía mensajes de forma periódica al broker y estos son recibidos sin problema en el subscriber. Esto demuestra que la conexión entre los dispositivos funciona correctamente.

## Evidencia

Las capturas de pantalla del funcionamiento se encuentran en la carpeta **evidencia**, donde se muestra:

* Ejecución de Mosquitto (Instalación correcta de mosquitto)
* Monitor serial de la ESP32 (Ejecución de Publisher en ESP32)
* Recepción de mensajes (Recepción de mensajes en el bróker como Subscriber)
