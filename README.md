# node-red-contrib-siemens-sentron
Node-RED nodes to read electrical measures from [Siemens SENTRON](https://new.siemens.com/global/en/products/energy/low-voltage/components/sentron-measuring-devices-and-power-monitoring.html) series over Modbus TCP/IP.
## Table of Contents
* [Install](#install)
* [How to use](#how-to-use)
* [Supported devices](#supported-devices)
* [Usage](#usage)
* [Meters data](#meters-data)
* [Equipment compatibility](#equipment-compatibility)
---

## Install
You can install these nodes directly from the **Manage Palette** menu in the [Node-RED](https://nodered.org/) interface.

Alternatively, run the following command in your Node-RED user directory - typically `~/.node-red` on Linux or `%HOMEPATH%\.nodered` on Windows

        npm install node-red-contrib-siemens-sentron
        
You must also install `node-red-contrib-modbus` directly from the **Manage Palette** menu in the Node-RED interface or run the following command in your Node-RED user directory
       
        npm install node-red-contrib-modbus
                 
## How to use

### measure node
Use the `measure` node to configure which information you want to request from the device.

Wire the output of the `measure` to the input of the `Modbus Flex Getter` from 'node-red-contrib-modbus' modules.

Enable check box `Keep Msg Properties` in the `Modbus Flex Getter` properties.

### getter node
Use the `getter` node to convert the values from the modbus response into human readable numbers.

Wire the second output of the `Modbus Flex Getter` to the input of the `getter`.

## Supported devices

### Measuring devices
+ PAC1200
+ PAC1600
+ PAC2200
+ PAC3100
+ PAC3120
+ PAC3200
+ PAC3220
+ PAC3200T
+ PAC4200
+ PAC5200
+ SEM3

### Transfer controller
+ ATC6300

### Molded case circuit breakers
+ 3VA

### Dataserver
+ 7KN Powercenter 1000

### RF devices
+ 5SL6 COM
+ 5SV6 COM
+ 5ST3 COM
+ 3NA COM

## Usage
### Example flow
```json
[{"id":"ac42dc3cfc737a41","type":"tab","label":"Siemens SENTRON","disabled":false,"info":"","env":[]},{"id":"ba83206eb52d59f2","type":"inject","z":"ac42dc3cfc737a41","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"10","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":190,"y":180,"wires":[["9edbc9242d918b94","209122aaf081e90d"]]},{"id":"9edbc9242d918b94","type":"measure","z":"ac42dc3cfc737a41","name":"","unitId":"1","device":"pac2200","deviceProtection":"5st3com","data":"voltageLL-avg","x":400,"y":140,"wires":[["0a2ba7e6c1721f97"]]},{"id":"56cf05bc9733a65f","type":"getter","z":"ac42dc3cfc737a41","name":"","unitId":"","data":"","x":790,"y":140,"wires":[["be3da888d87fa30f"]]},{"id":"0a2ba7e6c1721f97","type":"modbus-flex-getter","z":"ac42dc3cfc737a41","name":"","showStatusActivities":false,"showErrors":false,"logIOActivities":false,"server":"50fc5c2a64d40a1e","useIOFile":false,"ioFile":"","useIOForPayload":false,"emptyMsgOnFail":false,"keepMsgProperties":true,"x":590,"y":140,"wires":[[],["56cf05bc9733a65f"]]},{"id":"be3da888d87fa30f","type":"debug","z":"ac42dc3cfc737a41","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"true","targetType":"full","statusVal":"","statusType":"auto","x":950,"y":140,"wires":[]},{"id":"209122aaf081e90d","type":"measure","z":"ac42dc3cfc737a41","name":"","unitId":"1","device":"pac2200","deviceProtection":"5st3com","data":"current-avg","x":400,"y":220,"wires":[["e1621552b6017614"]]},{"id":"b1dcc45732697c41","type":"getter","z":"ac42dc3cfc737a41","name":"","unitId":"","data":"","x":790,"y":220,"wires":[["3ece6051729284e5"]]},{"id":"e1621552b6017614","type":"modbus-flex-getter","z":"ac42dc3cfc737a41","name":"","showStatusActivities":false,"showErrors":false,"logIOActivities":false,"server":"50fc5c2a64d40a1e","useIOFile":false,"ioFile":"","useIOForPayload":false,"emptyMsgOnFail":false,"keepMsgProperties":true,"x":590,"y":220,"wires":[[],["b1dcc45732697c41"]]},{"id":"3ece6051729284e5","type":"debug","z":"ac42dc3cfc737a41","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"true","targetType":"full","statusVal":"","statusType":"auto","x":950,"y":220,"wires":[]},{"id":"358e4fca54d8b667","type":"comment","z":"ac42dc3cfc737a41","name":"PAC2200","info":"","x":400,"y":100,"wires":[]},{"id":"50fc5c2a64d40a1e","type":"modbus-client","name":"","clienttype":"tcp","bufferCommands":true,"stateLogEnabled":false,"queueLogEnabled":false,"tcpHost":"192.168.1.113","tcpPort":"502","tcpType":"DEFAULT","serialPort":"/dev/ttyUSB","serialType":"RTU-BUFFERD","serialBaudrate":"9600","serialDatabits":"8","serialStopbits":"1","serialParity":"none","serialConnectionDelay":"100","serialAsciiResponseStartDelimiter":"0x3A","unit_id":"1","commandDelay":"1","clientTimeout":"1000","reconnectOnTimeout":true,"reconnectTimeout":"2000","parallelUnitIdsAllowed":true}]
```
### Device type
![device-config](docs/device-config-a.png)

### Meter data 
![data-config](docs/data-config-a.png)

### Circuit protection device
![circuit-protection-device](docs/circuit-protection.png)

### Circuit protection data
![circuit-protection-device](docs/data-config-protection.png)

### Message object 
![message-format](docs/message-format.png)

### Sample flow
![sample-flow](docs/sample-flow.png)

### Application examples
[SENTRON 7KN Powercenter 1000 push messages with Node-RED](https://support.industry.siemens.com/cs/document/109808556/sentron-7kn-powercenter-1000-push-messages-with-node-red?dti=0&lc=en-AE)


## Meters data
List of **PAC2200** meter data:

| Measure                            | Units                 | Type            | 
| ---------------------------------- | --------------------- | --------------- | 
|  Voltage L1-N                      | V                     | Float 32        | 
|  Voltage L2-N                      | V                     | Float 32        |
|  Voltage L3-N                      | V                     | Float 32        |
|  Voltage L1-L2                     | V                     | Float 32        |
|  Voltage L2-L3                     | V                     | Float 32        |
|  Voltage L3-L1                     | V                     | Float 32        |
|  Current L1                        | A                     | Float 32        |
|  Current L2                        | A                     | Float 32        |
|  Current L3                        | A                     | Float 32        |
|  Apparent power L1                 | VA                    | Float 32        |
|  Apparent power L2                 | VA                    | Float 32        |
|  Apparent power L3                 | VA                    | Float 32        |
|  Active power L1                   | W                     | Float 32        |
|  Active power L2                   | W                     | Float 32        |
|  Active power L3                   | W                     | Float 32        |
|  Reactive power L1                 | var                   | Float 32        |
|  Reactive power L2                 | var                   | Float 32        |
|  Reactive power L3                 | var                   | Float 32        |
|  Power factor L1                   | -                     | Float 32        |
|  Power factor L2                   | -                     | Float 32        |
|  Power factor L3                   | -                     | Float 32        |
|  Frequency                         | Hz                    | Float 32        |
|  Average voltage L-N               | V                     | Float 32        |
|  Average voltage L-L               | V                     | Float 32        |
|  Average current                   | A                     | Float 32        |
|  Total apparent power              | VA                    | Float 32        |
|  Total active power                | W                     | Float 32        |
|  Total reactive power              | var                   | Float 32        |
|  Total power factor                | -                     | Float 32        |
|  Neutral current                   | A                     | Float 32        |
|  Active energy import              | Wh                    | Float 32        |
|  Reactive energy import            | varh                  | Float 32        |
|  Active energy export              | Wh                    | Float 32        |
|  Reactive energy export            | varh                  | Float 32        |
|  Active energy import tariff 1     | kWh                   | Double          |
|  Active energy import tariff 2     | kWh                   | Double          |
|  Active energy export tariff 1     | kWh                   | Double          |
|  Active energy export tariff 2     | kWh                   | Double          |
|  Reactive energy import tariff 1   | kvarh                 | Double          |
|  Reactive energy import tariff 2   | kvarh                 | Double          |
|  Reactive energy export tariff 1   | kvarh                 | Double          |
|  Reactive energy export tariff 2   | kvarh                 | Double          |
|  Apparent energy tariff 1          | kVAh                  | Double          |
|  Apparent energy tariff 2          | kVAh                  | Double          |


List of **7KN Powercenter 1000** meter data:

| Measure                            | Units                 | Type            | 
| ---------------------------------- | --------------------- | --------------- | 
|  Current temperature               | °C                    | Float 32        |   
|  Average temperature               | °C                    | Float 32        |
|  Actual current L                  | A                     | Float 32        |
|  Average current L                 | A                     | Float 32        |
|  Maximum current L                 | A                     | Float 32        |
|  L-N voltage                       | V                     | Float 32        |
|  Line frequency                    | Hz                    | Float 32        |
|  Active power L                    | W                     | Float 32        |
|  Apparent power L                  | VA                    | Float 32        |
|  Reactive power L                  | var                   | Float 32        |
|  Power factor L                    | -                     | Float 32        |
|  Imported active energy            | kWh                   | Float 64        |
|  Exported actie energy             | kWh                   | Float 64        |
|  Imported reactive energy          | kvarh                 | Float 64        |
|  Exported reactive energy          | kvarh                 | Float 64        |
|  Protection device status          | -                     | Unsigned int 16 |
|  Alarms status                     | -                     | Unsigned int 32 |
|  Mechanical operating cycles       | -                     | Float 32        |
|  Tripping operations               | -                     | Float 32        |
|  Short-circuit trips               | -                     | Float 32        |

Set unit IDs (1 .. 24) for paired circuit protection devices. 

## Equipment compatibility

Compare the values obtained with the measures on the installed device and report any bugs such as:
+ measured value error
+ measured value format
+ unit of measure

These modules have been developed and tested on:
+ SENTRON PAC2200
+ 7KN Powercenter 1000 with 5SL6 COM

