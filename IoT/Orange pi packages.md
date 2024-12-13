### software packages
- Python3
	`sudo apt install python3
- pip3
	`sudo apt install python3-pip
- python3-venv (tool for creating virtual environments)
	`sudo apt install python3-venv`
	
- git
```
sudo apt install git
```
- wiringOP
```
git clone https://github.com/orangepi-xunlong/wiringOP.git
cd wiringOP
./build clean
./build 
```
- install the needed packages for gpio 
```
sudo apt install swig python3-dev python3-setuptools
```

### Python libraries:
WiringOP
```
git clone --recursive https://github.com/orangepi-xunlong/wiringOP-Python.git
cd wiringOP-Python
sudo apt-get install swig python3-dev python3-setuptools
```

### Build & install with

```
python3 generate-bindings.py > bindings.i`
sudo python3 setup.py install
```


### Usage
```
gpio readall
gpio mode 2 out -> set the pin 2 in output
gpio write 2 1 -> set pin 2 to value = 1
gpio write 2 0 -> set pin 2 to value = 1
```




### for i2c
```
sudo pip install smbus

edit 
add line to the file:  /boot/orangepiEnv.txt
-> overlays=i2c0
```


### install mqtt

```
sudo apt-get update
sudo apt-get install mosquitto mosquitto-clients -y
sudo systemctl start mosquitto
sudo systemctl enable mosquitto
```

#### Install MQTT Python library
```
sudo apt-get install python3-pip -y
sudo pip install paho-mqtt
```
How to use this library in your Python programs, see  
[https://pypi.org/project/paho-mqtt/](https://pypi.org/project/paho-mqtt/)
