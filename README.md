# SomPi
The objectif of this project is to control your Somfy shaders from a Raspberry Pi.
My current remote is a [Smoove Origin RTS](https://boutique.somfy.fr/smoove-origin-rts.html)
Thanks Nickduino for the support.

Let's play with SomPi!

## Hardware - What do you need?
The first step is to buy the needed hardware.

### Transmitter
- I took this one: [433MHz RF Transmitter Receiver Kit](https://www.ebay.ch/itm/272993898467?ViewItem=&item=272993898467). 
- There is 5 transmitters and receivers in this kit, useful and cheap.
### Crystals
- As Somfy as a particular frequency to avoid noises, I found out that it's needed to change the crystal. 
- I took this one: [433.42M 433.42MHz R433 F433 SAW Resonator Crystals TO-39](https://www.ebay.ch/itm/232574365405?ViewItem=&item=232574365405). 
- There is 5 crystals also in this kit, useful and cheap too.
### Wires
- To easy plugs between the Raspberry Pi and the Transmitter. I had in stock some [Male to Female Solderless Flexible Breadboard Jumper Cable Wire for Raspberry Pi](https://www.amazon.com/Ganvol-Flexible-Breadboard-Raspberry-ordinateur/dp/B01LVVIOUO) but they were Male to Female...so I had to customized them. 
- Otherwise, you can buy directly [Female to Female Solderless Flexible Breadboard Jumper Cable Wire for Raspberry Pi](https://www.amazon.com/Ganvol-Flexible-Breadboard-Raspberry-ordinateur/dp/B01LWAXJJS)


## Preparation
You can now replace carefully your crystal by doing soldering.
Then you have to plug the transmitter to the RaspberryPi

There is three pins on the transmitter: 
1. ATAD (DATA)
2. VCC
3. GND (Ground)

You need to connect all of them to the [Raspberry Pi GPIO.](https://www.raspberrypi.org/documentation/usage/gpio/)
1. Connect the ATAD pin with GPIO 4 (or adapt for your needs)
2. VCC with 5V
3. GND with any GND pin on the Raspberry Pi

## Installation
You can easily install the python controller with the following instructions:
1. Install dependencies
`sudo apt-get update && sudo apt-get install git python pigpio python-pigpio python3-pigpio`
2. Verify that everything is well installed
`git --version && python --version`
3. Then clone this repository
`sudo git clone https://github.com/alxlaxv/SomPi.git`
4. Enter in SomPi
`cd SomPi`
5. Make the controller executable
`sudo chmod +x controller.py`
6. Launch pigpio daemon 
`sudo pigpiod`
7. Launch pigpio daemon automatically on every boot 
`sudo systemctl enable pigpiod.service`

## Configuration
Now you will need to register your emitter as a remote for your shaders.
First you need to do a long press on the Prog button behind your current official Remote.
Your shaders will then briefly move, you can now release the Prog button.

Now we need to pair SomPi as a new remote
`sudo python controller.py livingRoom register`
And then close your shaders to test the pairing
`sudo python controller.py livingRoom close`

That's it! Well done!

## Available commands

* Open: `sudo python controller.py livingRoom open`
* Close: `sudo python controller.py livingRoom close`
* Stop: `sudo python controller.py livingRoom stop`
* Register: `sudo python controller.py livingRoom register`
