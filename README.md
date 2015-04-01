# Sumobot Workshop Setup with Sparkcore
This is a cliff notes version from the [original](http://bocoup.com/weblog/assembling-preparing-robotsconf-sumobot-with-johnny-five/) of how to setup a sumobot to run the sparkcore using johnny five.

## Env setup (Ubuntu only)

Open the terminal application and install node but first make sure to remove other versions as they will not work with the ```spark-cli```. 

````
  sudo apt-get remove nodejs npm
  sudo apt-get purge nodejs npm
  sudo apt-get autoremove
````

Install nodejs from the Chris Lea repository. You'll need g++

````
  sudo apt-get install python-software-properties python g++ make
  sudo add-apt-repository ppa:chris-lea/node.js
  sudo apt-get update
  sudo apt-get install nodejs
````

Do NOT explicitly install npm. If you do so the incompatible npm from the standard Ubuntu repositories will be installed. The nodejs package in the Chris Lea repository contains a later version of npm. Now you can

```sudo npm -g install spark-cli```

## Spark Setup
- Connect spark and run ```sudo spark setup```
- Follow prompts, enter SSID, choose 2 for WPA security and then wifi password.
- Name your core, if it breathes cyan you are good. If not repeat ```spark setup```
- ```spark flash REPLACE_WITH_DEVICE_ID voodoo``` once it breathes cyan you are good.

## Servo calibration
- Install git ```sudo apt-get install git```
- Clone this repo. ```git clone sumobot-sparkcore```
- Then ```cd sumobot-sparkcore && npm install```
- Wire up one servo at a time as shown below
![alt tag](http://bocoup.com/img/weblog/continuous-calibration-spark.png)
- Open up ```calibrate.js```and replace ```process.env.SPARK_TOKEN``` with your ```ACCESS_TOKEN``` and ```process.env.SPARK_DEVICE_2``` with your ```DEVICE_ID```. Now run ```node calibrate.js``` and adjust the potentiometer until servo comes to a complet stop. You can find your ```ACCESS_TOKEN``` and ```DEVICE_ID``` in the [spark web ide](https://www.spark.io/build/)
- Hook up all wires as shown in the schematics below and then open up ```app.js```, add your ```ACCESS_TOKEN``` and  ```DEVICE_ID``` and then run ```node app.js```. Now you should control your sumobot with your arrow keys from the terminal. 
![alt tag](http://bocoup.com/img/weblog/sumo-spark-circuit.png)

For more info on what any of the colors of your spark mean or help troubleshooting, checkout their excellent [docs](http://docs.spark.io/connect/).
