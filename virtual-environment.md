

## installing  a virtual environment!

**ATTENTION:** If you don't already have python3 installed, make sure to do that!
but if you're also using the raspberry pi zero 2w it should be preinstalled!

### Process

- **step 1** run an update on your package manager, just in case

```
sudo apt update
```

- **step 2** install the ability to make virtual environments.

```
sudo apt install python3-venv
```
- **step 3** now create your virtual environment! **NOTE:** change "example" to the name you want for your env!

```
python3 -m venv example
```

- **step 4** entering your virtual environment! 
  

```
source example/bin/activate
```

- **step 5** now you're done! yay!



If you still have doubts you're in a virtual environment, you should see something like this in your terminal.

<img width="575" height="33" alt="image" src="https://github.com/user-attachments/assets/3e096e6c-65e7-4b15-aa7f-b63d7a04c5db" />

The grey text at the most left should be your virtual environment name!


If you want **to leave** the virtual environment then you must **type:**

```
deactivate
```

Typing that should remove the grey text on the left, and let you exit the env!
