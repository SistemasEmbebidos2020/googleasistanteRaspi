# GoogleasistanteRaspi
- Configurar altavoz y micrófono usb para la raspberry
- con el comando aplay -l verificar el número de tarjeta y número de dispositivo del parlante
- con el comando arecord -l verificar el número de tarjeta y número de dispositivo del micrófono
- ambos datos editarlos en el siguiente archivo
- editar el archivo /home/pi/.asoundrc y colocar lo siguiente
-- pcm.!default {
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

- con el comando speaker-test -t wav, se confirma que esté correctamente funcionando el parlante
