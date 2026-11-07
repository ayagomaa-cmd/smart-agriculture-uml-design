# 🌾 Smart Climate Agriculture & Warehouse Management System (UML & System Architecture)

A complete system analysis and object-oriented architectural design for an IoT and cloud-integrated agriculture and inventory tracking platform.

---

## 📌 Project Overview
A smart agriculture enterprise operates connected greenhouses and automated wheat storage warehouses. The platform integrates **IoT sensors, PlantEye multispectral cameras, RFID tags, Raspberry Pi microcontrollers, and AWS cloud analytics** to eliminate manual delays, automate disease detection, and enforce FIFO inventory dispatch.

---

## ⚙️ Core System Architecture
* **Greenhouse Layer:** Real-time monitoring of temperature, humidity, and solar radiation with automated anomaly detection.
* **Crop Analytics:** Automated plant disease detection and growth assessment using multispectral image processing.
* **Warehouse Management:** Automated grain bag tracking via RFID scanners and strict FIFO stock rotation.
* **Communication & Cloud:** MQTT brokers connecting microcontrollers with AWS cloud storage and operational dashboards.

---
---

## 📋 System Requirements

### Environmental Monitoring Requirements
* **FR1:** The system allows the temperature sensor to continuously monitor greenhouse temperature.
* **FR2:** The system allows the humidity sensor to continuously monitor greenhouse humidity.
* **FR3:** The system allows the solar radiation sensor to measure shortwave radiation levels.
* **FR4:** The system allows the solar radiation sensor to measure light and heat intensity.
* **FR5:** The system allows the PlantEye camera to capture images of wheat crops for health analysis.

### Data Processing & Alerting Requirements
* **FR6:** The system allows the PI microcontroller to gather readings from all sensors and cameras.
* **FR7:** The system analyzes collected environmental and crop data in real time.
* **FR8:** The system detects environmental anomalies based on predefined thresholds.
* **FR9:** The system detects crop diseases and pest indications using image analysis.
* **FR10:** The system evaluates plant growth status and determines cultivation needs.
* **FR11:** The system sends automated alerts to the supervisor when abnormal conditions are detected.

### RFID & Warehouse Management Requirements
* **FR12:** The system allows the supervisor to notify warehouse inventory about incoming wheat stock.
* **FR13:** The system allows RFID readers to scan wheat bag tags during storage.
* **FR14:** The system allows the warehouse manager to add incoming stock and track storage dates.
* **FR15:** The system identifies older wheat batches and guides release according to the FIFO method.
* **FR16:** The system generates automated warehouse and inventory reports.
## 📊 System Diagrams & Documentation

### 1. Use Case Diagram
Models external actors (sensors, supervisors, warehouse operators) and interactions with the MQTT broker and core system logic.
<img width="1430" height="1034" alt="Picture1" src="https://github.com/user-attachments/assets/c6505e4d-d421-4851-a289-c30b5746fb40" />


### 2. Class Diagram
Defines the object structure, attributes, data types, and inter-class relationships.

```mermaid
classDiagram
    class TemperatureSensor {
        -int temperatureSensorID
        -int temperatureValue
        -varchar sensorModel
        -int measurementTime
        +initiateSensing()
        +monitorTemperature()
    }

    class HumiditySensor {
        -int humiditySensorID
        -int humidityValue
        -varchar sensorModel
        -int measurementTime
        +initiateSensing()
        +testHumidity()
    }

    class SolarRadiationSensor {
        -int solarRadiationSensorID
        -int shortWaveRadiationValue
        -int heatIntensityValue
        -varchar sensorModel
        -int measurementTime
        +initiateSensing()
        +measureShortWaveRadiation()
        +measureLightAndHeatIntensity()
    }

    class PlantEyeCamera {
        -int cameraID
        -varchar diseaseType
        -varchar plantGrowthLevel
        +startCapturingPlantImages()
        +requestPlantImages()
    }

    class PiMicrocontroller {
        -int microcontrollerID
        -varchar model
        -int batteryLevel
        +gatherSensorReadings()
        +getDataInsights()
        +detectAnomaly()
        +generateReport()
        +requestReport()
        +sendPlantImages()
        +detectCropDiseases()
        +checkPlantGrowth()
    }

    class Supervisor {
        -int supervisorID
        -varchar name
        -varchar email
        +sendAlert()
        +sendReport()
        +plantsNeedCultivation()
    }

    class WarehouseManager {
        -int managerID
        -varchar name
        -varchar email
        +monitorIncomingStock()
        +getReadings()
        +receiveWheatQuantities()
        +sendWarehouseReport()
    }

    class WarehouseEmployee {
        -int employeeID
        -varchar name
        -varchar email
        -varchar address
        +receiveWheatBagDates()
    }

    class WarehouseInventory {
        -int tagID
        -date dateOfCultivation
        -int quantity
        -varchar wheatBagLocation
        +notifyWarehouseAboutIncomingStock()
        +noIncomingStock()
        +addToStock()
        +releaseOldWheat()
    }

    class RfidReader {
        -int readerID
        -int readerRange
        +readRfidTag()
        +requestWheatBagDates()
    }

    class WarehouseReport {
        -varchar spaceEfficiency
        -int wheatBagReleases
        -int inputsAndOutputs
        -varchar rfidTracking
        +requestWarehouseReport()
    }

    TemperatureSensor --> PiMicrocontroller : send readings
    HumiditySensor --> PiMicrocontroller : send readings
    SolarRadiationSensor --> PiMicrocontroller : send readings
    PlantEyeCamera --> PiMicrocontroller : send readings
    PiMicrocontroller --> Supervisor : send alert
    Supervisor --> WarehouseManager : notify about incoming stock
    WarehouseManager --> WarehouseInventory : add to stock
    WarehouseEmployee --> WarehouseInventory : release wheat
    WarehouseEmployee --> RfidReader : track wheat bags through
    WarehouseInventory --> WarehouseReport : contributes in
    RfidReader --> WarehouseReport : contributes in
    WarehouseManager --> WarehouseReport : request
```


### 3. Sequence Diagrams
Illustrates the temporal exchange of messages between microcontrollers, sensors, cloud services, and actors:
* **Greenhouse Monitoring & Anomaly Alerting:**
  <img width="522" height="432" alt="Picture4" src="https://github.com/user-attachments/assets/8991ffba-7f00-4c68-a654-76b070c7e725" />
<img width="610" height="465" alt="Picture3" src="https://github.com/user-attachments/assets/b883240c-4e0e-408a-805b-d606aec6f914" />

* **Plant Health Analysis & Cultivation Notification:**
  ![Sequence Diagram - Crop](diagrams/sequence-diagram-crop.png)
* **RFID Warehouse Ingestion & FIFO Stock Release:**
  ![Sequence Diagram - Warehouse](diagrams/sequence-diagram-warehouse.png)

### 4. Activity Diagrams
Step-by-step business workflows covering anomaly branches, alerting thresholds, and inventory updates.
* **Crop Image Capture & Analysis Flow:**
  ![Activity Diagram - PlantEye](diagrams/activity-diagram-planteye.png)
* **FIFO Warehouse Release Workflow:**
  ![Activity Diagram - Warehouse](diagrams/activity-diagram-warehouse.png)

---

## 🛠️ Tools & Standards
* **Modeling Tool:** Visual Paradigm
* **Standard:** UML 2.0 (Use Case, Class, Sequence, Activity)
* **Target Architecture:** IoT Sensors, MQTT Broker, AWS Cloud Platform, RFID Tracking
