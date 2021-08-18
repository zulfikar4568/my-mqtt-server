# Menjalankan Mosquitto menggunakan Username dan Password

## Setup Environment Variable
Ubah file `example.env` menjadi `.env` dan ganti Password di `.env`
```
MOSQUITTO_USERNAME=mosquitto
MOSQUITTO_PASSWORD=mosquitto
```
Ubah versi mosquitto di `.env` sesuai dengan image yang tersedia di [Docker Hub](https://hub.docker.com/)
```
MOSQUITTO_VERSION=latest
```
## Build Image
```
sudo docker-compose build
```
## Jalankan Container
```
sudo docker-compose up -d
```

## Testing
Gunakan MQTT client lalu hubungkan dengan MQTT Broker. Gunakan official `mosquitto_pub` dan `mosquitto_sub` untuk melakukan publish dan subscribe, dalam hal ini pastikan mosquitto sudah [terinstal](https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-the-mosquitto-mqtt-messaging-broker-on-ubuntu-18-04)

```
# Subscribe to topic.
mosquitto_sub -h <host/ip> -t test -u "mosquitto" -P "mosquitto"

# Publish a message.
mosquitto_pub -h <host/ip> -t test -m "hello." -u "mosquitto" -P "mosquitto"
```

Jika kita ingin langsung mencoba, kita bisa masuk ke dalam container untuk men test mqtt yang sudah kita install
### Masuk ke Container
Sediakan dua buah terminal dan ketikan perintah berikut
```
sudo docker exec -it eclipse-mosquitto sh
```

Jalankan dua buah perintah pada masing - masing container
```
# Pada terminal 1. Digunakan untuk subscribe
mosquitto_sub -h localhost -t test -u "mosquitto" -P "mosquitto"

# Pada terminal 2. Digunakan untuk publish
mosquitto_pub -h localhost-t test -m "hello." -u "mosquitto" -P "mosquitto"
```
Maka seharusnya akan muncul message `hello` pada terminal 1

## Menstop Container
```
sudo docker-compose down
```