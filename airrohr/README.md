# 2019-Nifi
Apache Nifi Scripte for 2019


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

_Example data record_

'''
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

'''

* WeatherObserved

Depending on the design, the spring sensor provides at least the temperature and the relative humidity, the different sensor types are described below.

Each spring sensor is combined to a measuring station via a device reference with an associated fine dust sensor.

_Example data record_


'''
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
'''

### Sensor Types

### Credits
