# envsensor-observer-py

Python Bluetooth low energy observer example for OMRON Environment Sensor ([2JCIE-BL01](http://www.omron.com/ecb/products/sensor/special/environmentsensor/))([2JCIE-BU01](https://www.components.omron.com/product-detail?partId=73065)).

*   No BLE connections are required
*   Accept advertisements from multiple sensor
*   Collect variety of environmental information from sensor beacon
    *   Temperature
    *   Humidity
    *   Light
    *   UV Index
    *   Absolute pressure
    *   Noise (Sound level)
    *   3-Axis Acceleration
    *   Discomfort Index
    *   Heatstroke risk indicator
    *   Battery voltage
    *   RSSI
*   2JCIE-BU Environment Sensor (USB Type) is now supported (Advertising mode 0x01 & 0x02)
*   Flexible data logging options
    *   Local CSV file (rotate every midnight)
    *   Local / Remote [fluentd](http://www.fluentd.org/) daemon
    *   Local / Remote [InfluxDB](https://www.influxdata.com/time-series-platform/influxdb/)
*   Tested on Raspberry Pi 3 model B (built-in Bluetooth connectivity)


![Diagram](https://github.com/OmronMicroDevices/envsensor-observer-py/wiki/images/diagram_s.png)

## Requirements

*   BlueZ libraries
*   python 2.7
    *   python-bluez
    *   [fluent-logger-python](https://github.com/fluent/fluent-logger-python) (Optional)
    *   [influxdb-python](https://github.com/influxdata/influxdb-python) (Optional)

## Instructions

These instructions apply only to an up-to-date Raspbian Jessie with PIXEL, the official Raspberry PI distro.

### Prerequisite

    $ sudo apt-get install python-bluez

When using fluentd forwarder (Optional)

    $ sudo pip install fluent-logger

When uploading data to influxDB 0.9 or higher (Optional)

    $ sudo pip install influxdb
    $ sudo pip install --upgrade influxdb

#### Device Setup

![Sensor](https://github.com/OmronMicroDevices/envsensor-observer-py/wiki/images/2jcie-bl01_s.png)

Environment Sensor (2JCIE-BL01) must be configured as a beacon broadcaster (IM/EP).

In this mode of operation, sensor data is included in the advertisement packet to be transmitted.

Please refer to [communication interface manual](https://omronmicrodevices.github.io/products/2jcie-bl01/communication_if_manual.html) for more details.


### Configuration

Open `conf.py` and edit your configuration.

 > CSV is saved under _**./log/**_ directory in the script path by default.
 >
 > You can specify a different log location in your configuration.

### Run

*   Normal mode

Only sensor status information is sent to _stdout_ in a set interval.

    $ sudo ./envsensor_observer.py

 > You need to make `envsensor_observer.py` executable.
 >
 > You can use **Supervisor** to start the script running in the background when system boot.

*   Debug mode

Full Bluetooth messages are sent to _stdout_ in addition to the sensor status.


    $ sudo ./envsensor_observer.py --debug

 or

    $ sudo ./envsensor_observer.py -d


## Visualization

With [Grafana](http://grafana.org/), you can easily visualize any of data stored in [InfluxDB](https://www.influxdata.com/time-series-platform/influxdb/) through this script.

![Dashboard](https://github.com/OmronMicroDevices/envsensor-observer-py/wiki/images/grafana_dashboard.png)

## Note :

It should be noted that this example code is for demonstration purposes only, it is not intended for use in a production environment, is not guaranteed fit for any purpose.

## Reference :
*   [OMRON Corporation](http://www.omron.com/)
*   [OMRON Micro Devices - Github](https://github.com/OmronMicroDevices/)
*   [OMRON Micro Devices - Resources & Samples](https://OmronMicroDevices.github.io/)
*   [Environment Sensor : 2JCIE-BL01 Product Page](http://www.omron.com/ecb/products/sensor/special/environmentsensor/)
*   [環境センサ : 2JCIE-BL01 製品紹介](http://www.omron.co.jp/ecb/products/sensor/special/environmentsensor/)
*   [Environment Sensor : 2JCIE-BL01 Communication Interface Manual](https://omronmicrodevices.github.io/products/2jcie-bl01/communication_if_manual.html)
