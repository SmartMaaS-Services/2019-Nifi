# 2019-Nifi
Apache Nifi Scripte for 2019

[![MIT license](https://img.shields.io/badge/license-MIT-blue.svg)](https://spdx.org/licenses/MIT.html)
[![SOF support badge](https://nexus.lab.fiware.org/repository/raw/public/badges/stackoverflow/orion.svg)](http://stackoverflow.com/questions/tagged/fiware-orion)
[![NGSI v2](https://nexus.lab.fiware.org/repository/raw/public/badges/specifications/ngsiv2.svg)](http://fiware-ges.github.io/orion/api/v2/stable/)


## Airrohr

Fine dust data from the Sensor.community platform in NGSI V2 format

### Context Broker and API endpoint

The used Context Broker is located in the FIWARE platform https://2019.smartmaas.services and is accessed via API at https://context.2019.smartmaas.services.

The fiware service used is smartmaas001 and the fiware service path /

A Bearer Token must be registered at https://apis.2019.smartmaas.services.

The transfer of the data is carried out via the following endpoint https://context.2019.smartmaas.services/v2/op/update/


### Entenitiy Types

3 Entitiy Tpyes are generated:

* Device

Device combines the particulate matter sensors and the corresponding weather sensor to a measuring station which forms a location using the location data.

_Datamodell_

[WeatherObserved]

_Example data record_

```
{
  "actionType" : "append",
  "entities" : [ {
    "type" : "Device",
    "category" : {
      "value" : "sensor"
    },
    "dateObserved" : {
      "type" : "DateTime",
      "value" : "2020-02-27T10:36:59"
    },
    "location" : {
      "type" : "geo:json",
      "value" : {
        "type" : "Point",
        "coordinates" : [ 8.684, 51.686 ]
      }
    },
    "id" : "Device_16399",
    "name" : {
      "value" : "Device_16399"
    }
}

```

* WeatherObserved

Depending on the design, the spring sensor provides at least the temperature and the relative humidity, the different sensor types are described below.

Each spring sensor is combined to a measuring station via a device reference with an associated fine dust sensor.

_Datamodell_

[AirQualityObserved]

_Example data record_

```
{
  "actionType" : "append",
  "entities" : [ {
    "refDevice" : {
      "type" : "Relationship",
      "value" : "Device_15077"
    },
    "type" : "WeatherObserved",
    "dateObserved" : {
      "type" : "DateTime",
      "value" : "2020-02-27T10:39:56"
    },
    "location" : {
      "type" : "geo:json",
      "value" : {
        "type" : "Point",
        "coordinates" : [ 9.908, 49.704 ]
      }
    },
    "id" : "BMP280_27826",
    "stationName" : {
      "value" : "BMP280_27826"
    },
    "temperature" : {
      "value" : 8.87
    },
    "atmosphericPressure" : {
      "value" : 969.3380999999999
    }
  }

```

* AirQualityObserved

Depending on the type, the particulate matter sensor provides at least the PM 2.5 and PM 10 data. Some types can provide further measured values, but are not considered here at this time. The different sensor types are described below. 

Each particulate matter sensor is linked via a device reference with a corresponding weather sensor.

_Example data record_

```
{
    "stationCode" : {
      "type" : "Text",
      "value" : "SDS011_13683"
    },
    "refDevice" : {
      "type" : "Relationship",
      "value" : "Device_6914"
    },
    "PM25" : {
      "metadata" : {
        "unitCode" : {
          "value" : "GP"
        }
      },
      "value" : 20.03
    },
    "PM2.5" : {
      "metadata" : {
        "unitCode" : {
          "value" : "GP"
        }
      },
      "value" : 20.03
    },
    "PM10" : {
      "metadata" : {
        "unitCode" : {
          "value" : "GP"
        }
      },
      "value" : 10.5
    },
    "type" : "AirQualityObserved",
    "source" : {
      "value" : "https://sensor.community/"
    },
    "dateObserved" : {
      "type" : "DateTime",
      "value" : "2020-02-27T13:18:58"
    },
    "location" : {
      "type" : "geo:json",
      "value" : {
        "type" : "Point",
        "coordinates" : [ 9.908, 53.552 ]
      }
    },
    "id" : "SDS011_13683"
  }

```

### Sensor Types

* BMP180

Datasheet
- https://www.alldatasheet.com/datasheet-pdf/pdf/1132068/BOSCH/BMP180.html

Phenomena
- Temperature
- Air pressure 

Measurement ranges
- Temperature  -40 - 85°C 
- pressure     300 - 1100 hPa

* BMP280

Datasheet
- https://eu.mouser.com/datasheet/2/783/BST-BMP280-DS001-1509562.pdf

Phenomena
- Temperature
- Air pressure

Measurement ranges
- Temperature  -40 - 85°C
- pressure     300 - 1100 hPa

* BME280

Datasheet
- https://pdf1.alldatasheet.com/datasheet-pdf/view/1132060/BOSCH/BME280.html

Phenomena
- Temperature
- relative air humidity
- Air pressure

Measurement ranges
- Temperature  -40 - 85°C    
- pressure     300 - 1100 hPa
- humidity       0 - 100%

* DHT22

Datasheet
- https://pdf1.alldatasheet.com/datasheet-pdf/view/1132459/ETC2/DHT22.html

Phenomena
- Temperature
- relative air humidity

Measurement ranges
- Temperature  -40 - 80°C
- humidity       0 - 100%

* SHT31

Datasheet
- https://pdf1.alldatasheet.com/datasheet-pdf/view/897975/ETC2/SHT31.html

Phenomena
- Temperature
- relative air humidity

Measurement ranges
- Temperature  -40 - 90°C
- humidity       0 - 100%


* SDS011

Datasheet
- https://cdn-reichelt.de/documents/datenblatt/X200/SDS011-DATASHEET.pdf

Phenomena
- dust particles PM2.5
- dust particles PM10

Measurement ranges
- PM2.5/PM10 0.0-999.9 μg/m3

* PMS1003

Datasheet
- http://www.aqmd.gov/docs/default-source/aq-spec/resources-page/plantower-pms1003-manual_v2-5.pdf

Phenomena
- dust particles PM1
- dust particles PM2.5
- dust particles PM10

Measurement ranges
- PM1/PM2.5/PM10 ca.0 - 500 μg/m3


* PMS7003

Datasheet
- https://www.pdf-archive.com/2017/04/12/plantower-pms-7003-sensor-data-sheet/plantower-pms-7003-sensor-data-sheet.pdf

Phenomena
- dust particles PM1
- dust particles PM2.5
- dust particles PM10

Measurement ranges
- PM1/PM2.5/PM10 ca.0 - 500 μg/m3

* PPD42NS

Datasheet
- https://www.mouser.com/datasheet/2/744/Seeed_101020012-1217636.pdf

Phenomena
- dust particles PM1
- dust particles PM2.5
- dust particles PM10

Measurement ranges
- PM1/PM2.5/PM10 0 ~ 8000 μg/m3

### Credits

Credits to opendata-stuttgart
http://codefor.de/stuttgart/

and

Open Knowledge Foundation Deutschland e.V.
https://okfn.de/

and all the 10 thousands people who operate an "AirRohr Sensors

[WeatherObserved]: https://fiware-datamodels.readthedocs.io/en/latest/Weather/WeatherObserved/doc/spec/index.html
[AirQualityObserved]: https://fiware-datamodels.readthedocs.io/en/latest/Environment/AirQualityObserved/doc/spec/index.html
