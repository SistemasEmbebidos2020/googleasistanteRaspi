# GoogleasistanteRaspi
- Configurar altavoz y micrófono usb para la raspberry
- con el comando aplay -l verificar el número de tarjeta y número de dispositivo del parlante
- con el comando arecord -l verificar el número de tarjeta y número de dispositivo del micrófono
- ambos datos editarlos en el siguiente archivo
- editar el archivo /home/pi/.asoundrc y colocar lo siguiente
 ```
 pcm.!default {
  type asym
  capture.pcm "mic"
  playback.pcm "speaker"
}
pcm.mic {
  type plug
  slave {
    pcm "hw:[card number],[device number]"
  }
}
pcm.speaker {
  type plug
  slave {
    pcm "hw:[card number],[device number]"
  }
}
```
- con el comando speaker-test -t wav, se confirma que esté correctamente funcionando el parlante
- con el comando arecord --format=S16_LE --duration=5 --rate=16000 --file-type=raw out.raw nos permite grabar un audio para comprobar el micrófono
- con el comando aplay --format=S16_LE --rate=16000 out.raw verificamos que se grabó correctamente nuestro audio
- realizar un apt-get update y apt-get upgrade
- instalar un entorno virtual en la raspberry, habilitarlo y entrar en el modo virtual 
 ```
sudo apt-get install python3-dev python3-venv
python3 -m venv env 
source env/bin/activate
```
- Ahora instalar los paquetes requeridos dentro del entorno virtual
```
python -m pip install --upgrade pip setuptools wheel
```
- Instalar paquetes de audio
```
sudo apt-get install portaudio19-dev libffi-dev libssl-dev
```
- Instalar el paquete de google assitant
```
python -m pip install --upgrade google-assistant-sdk[samples]
```
- Subir json de configuracion de google y ejecutar el siguiente comando y acceder al enlace que les asomará para permitir la app
```
python -m pip install --upgrade google-auth-oauthlib[tool]
google-oauthlib-tool --scope https://www.googleapis.com/auth/assistant-sdk-prototype --save --headless --client-secrets /home/pi/<credentials-file-name>.json
```
- Para ejecutar el asistente de google:
```
googlesamples-assistant-pushtotalk --project-id raspi-9959a --device-model-id raspi-9959a-raspi3-2rj8mo
```
