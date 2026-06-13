

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
