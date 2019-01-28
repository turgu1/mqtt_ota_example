# MQTT OTA Example

This is a simple example of using MQTT as a mean to update a piece of software running on a ESP8266 through OTA. It is a demonstration of a small change requested to the PubSubClient that allows for the transmission of large messages and injection of the received code through a stream normally hooked to the PubSubClient class.

The patched version of the PubSubClient can be find here: https://github.com/turgu1/pubsubclient.git

To use the code, do the following:

1. Edit the parameters for your WiFi and MQTT broker connexions, at the beginning of the src/main.cpp file.

2. Compile and upload the code (PlatformIO).

3. Reset the chip. This is required to not get any complaints about Error 11 (bootstarp needed...)

4. Send a first message to the topic "test/ota" containing a string "SIZE=xxxx"  where xxxx is the size in bytes of the binary firmware to follow:

```
mosquitto_pub -p 1883 -t "test/ota" -h "your_broker_addr" -m "SIZE=423456"
```

5. Send a second message with the content of the firmware to send:

```
mosquitto_pub -p 1883 -t "test/ota" -h "your_broker_addr" -f firmware.bin
```


2019-01-28, GuyTurcotte
