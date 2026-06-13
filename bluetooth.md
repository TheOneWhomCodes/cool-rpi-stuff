

# Bluetooth stuff!!


## Basics

to enter the bluetooth terminal type:

´´´
bluetoothctl
´´´
ctl stands for control, cool huh

to enable bluetooth, type:

```
power on
```

and to turn it off

```
power off
```

If you want to scan for nearby devices that're using bluetooth, you can use this

```
scan on
```
You will see an output like this

<img width="756" height="102" alt="image" src="https://github.com/user-attachments/assets/6d3b764a-39dd-4450-9b3f-cf152f76ddcb" />

This way you can try to find your device's MAC address

## Pairing

When you want to pair a device, you look for your device's MAC address which looks like this *AA:AA:AA:AA:AA:AA* for example

if you found your MAC address you can pair it like this:

Keep in mind that you need to **turn on scanning** when pairing

```
pair AA:AA:AA:AA:AA:AA
```

After that you can *connect* with your device like this:

```
connect AA:AA:AA:AA:AA:AA
```

You can also *trust* the device, so that your pi can reconnect to it automatically when he finds it!

like this:

```
trust AA:AA:AA:AA:AA:AA
```



## Audio problem

You might encounter a problem, like I did, where you cannot connect to your device, but you can pair with it

The most likely reason for that happening is because your pi does not support the software needed to use the bluetooth device's service, for example a bluetooth speaker

My pi cannot connect to bluetooth speakers due to it not having an audio system installed, therefore I need to install one in order to make it work

If you're suffering from the same problem then you can download this in order to let your pi use bluetooth speakers/headphones

```
sudo apt update
sudo apt install bluez pulseaudio pulseaudio-module-bluetooth
```
- bluez: is bluetooth itself, your pi will most likely already have this, but it doesn't hurt to update it

- pulseaudio: a soundsystem which lets linux play audio

- pulseaudio-module-bluetooth: This is the "bridge" I need, so that my pi knows how to send data over to my bluetooth headphones


Now that it's installed you can use this to check if the audio system is running

```
pulseaudio --check
```
if it doesn't give an output then that means you're good!

now reboot your device like this

```
reboot
```

Now if you allowed your device to be trusted by the rpi, it should automatically connect and work

To see if it's working you can use this command

```
pactl list short sinks
```

- pactl: This stands for PulseAudio Control, this is a tool that lets you inspect audio devices, change them, route sound, and etc it's basically how you control your sound system

- list: this asks the pactl tool to list info

- short: this asks to make the info readable and compact, without it you get alot of text thrown at you

- sinks: this stands for output devices, like speakers, headphones, hdmi audio

an input device device would be called a *source*, like a microphone

after using that command you should see something like this:

<img width="1350" height="49" alt="image" src="https://github.com/user-attachments/assets/0f6228a2-d58a-48b6-9eec-d16fa0b3d71a" />

- the number 3: is the internal id of my device (headphones)

- bluez_sink.41_42_C6_BD_99_64.a2dp_sink:
  - bluez_sink.41_42_C6_BD_99_64 is the MAC address in a different format
  - .a2dp_sink this means that my device supports stereo audio
  
- module-bluez5-device.c : this is the module we installed on our rpi to route bluetooth audio correctly, the *.c* means it's a plugin written in C

- s16le 2ch 48000Hz: this is the audio format my device uses

- SUSPENDED: this means that the device isn't getting sent audio at the moment, so it's idle, when audio does get sent through it'll be changed to RUNNING


if you want to play audio files with a builtin linux command you can use

```
aplay
```

and since it's builtin they even come with builtin .wav files you can try out like this

```
aplay /usr/share/sounds/alsa/Front_Center.wav
```

**BEWARE**: since it's a lightweight builtin command, it can only play .wav files! so no mp3!!

To change get the current volume of your device you can write this:

```
pactl get-sink-volume DEVICE_NAME
```
for me DEVICE_NAME would be *bluez_sink.41_42_C6_BD_99_64.a2dp_sink* You can find out what device name you have by looking at the steps above

to change the volume you can do this

```
pactl set-sink-volume DEVICE_NAME 100%
```
You can even go past a 100% when the device normally doesn't let you, so that's a fun way to bypass that!
