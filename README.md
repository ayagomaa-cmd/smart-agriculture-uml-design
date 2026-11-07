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
```mermaid
flowchart LR
    %% Actors
    subgraph Sensors ["Greenhouse Sensors"]
        T_Sensor((Temperature Sensor))
        H_Sensor((Humidity Sensor))
        R_Sensor((Solar Radiation Sensor))
        Cam((PlantEye Camera))
    end

    subgraph Devices ["Field Devices"]
        RFID_Dev((RFID Reader))
        Pi((PI Microcontroller))
    end

    subgraph Users ["Actors & Supervisors"]
        Sup((Supervisor))
        WM((Warehouse Manager))
        WE((Warehouse Employee))
    end

    %% MQTT Broker Boundary
    subgraph MQTT ["MQTT Broker"]
        B1[Message Ingestion]
    end

    %% System Boundary
    subgraph CoreSystem ["Smart Climate Agriculture & Warehouse System"]
        UC1([Monitor Temperature])
        UC2([Test Humidity])
        UC3([Measure Solar Radiation])
        UC4([Capture Plant Images])
        UC5([Gather Sensor & Camera Readings])
        UC6([Get Data Insights])
        UC7([Detect Anomaly])
        UC8([Detect Crop Disease])
        UC9([Check Plant Growth])
        UC10([Send Alert to Supervisor])
        UC11([Generate & Receive Sensors Report])
        UC12([Notify Warehouse About Incoming Stock])
        UC13([Read Tags & Quantities])
        UC14([Add New Stock to Inventory])
        UC15([Release Old Wheat - FIFO])
        UC16([Request & Receive Warehouse Report])
    end

    %% Sensor Connections
    T_Sensor --> B1 --> UC1 --> UC5
    H_Sensor --> B1 --> UC2 --> UC5
    R_Sensor --> B1 --> UC3 --> UC5
    Cam --> B1 --> UC4 --> UC5

    %% Processing & Pi Microcontroller
    UC5 <--> Pi
    UC5 --> UC6
    UC6 -.->|extend| UC7
    UC6 -.->|extend| UC8
    UC6 -.->|extend| UC9

    %% Alerts & Reports
    UC7 -.->|include| UC10
    UC8 -.->|include| UC10
    UC10 --> Sup
    Sup --> UC11
    UC9 -.->|extend| UC12
    UC12 --> Sup

    %% Warehouse Operations
    Sup --> UC12 --> WM
    RFID_Dev --> UC13
    WM --> UC14
    UC13 --> UC14
    WE --> UC15
    UC13 --> UC15
    WM --> UC16
```
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
 ```mermaid
sequenceDiagram
    autonumber
    actor Supervisor
    participant Microcontroller as PI Microcontroller
    participant Sensor as Solar Radiation Sensor

    Microcontroller->>Sensor: Initiate sensing
    Sensor-->>Microcontroller: Measure short-wave radiation

    loop Continuous Sensing
        Sensor->>Microcontroller: Gather sensor data (wavelength data)
        Note over Microcontroller: Get data insights
    end

    opt Wavelength exceeds range
        Note over Microcontroller: Detect anomaly
        Microcontroller->>Supervisor: Send alert (wavelength exceeds)
        Supervisor-->>Microcontroller: Confirmed
    end

    Supervisor->>Microcontroller: Request report
    Note over Microcontroller: Generate report
    Microcontroller-->>Supervisor: Send report
```
* **Plant Health Analysis & Cultivation Notification:**
```mermaid
sequenceDiagram
    autonumber
    actor Supervisor
    participant Microcontroller as PI Microcontroller
    participant Camera as PlantEye Multispectral Camera
    participant Warehouse as Warehouse Inventory

    Microcontroller->>Camera: Start capturing plant images
    Microcontroller->>Camera: Request plant images

    loop Continuous Capture
        Camera->>Microcontroller: Send plant images
        Note over Microcontroller: Get data insights (image data)
    end

    opt Disease Detected
        Note over Microcontroller: Detect crop disease
        Microcontroller->>Supervisor: Send alert (crop disease detected)
        Supervisor-->>Microcontroller: Confirmed
    end

    opt Cultivation Ready
        Note over Microcontroller: Check plant growth
        Microcontroller->>Supervisor: Send alert (plants need cultivation)
        Supervisor-->>Microcontroller: Confirmed
    end

    alt Wheat Growth Adequate
        Supervisor->>Warehouse: Notify warehouse about incoming stock
        Warehouse-->>Supervisor: Confirmed
    else Growth Inadequate
        Supervisor->>Warehouse: No incoming stock
        Warehouse-->>Supervisor: Confirmed
    end

    Supervisor->>Microcontroller: Request sensor report
    Note over Microcontroller: Generate report
    Microcontroller-->>Supervisor: Send report
```
  
* **RFID Warehouse Ingestion & FIFO Stock Release:**
```mermaid
sequenceDiagram
    autonumber
    actor Manager as Warehouse Manager
    participant RFID as RFID Reader
    actor Employee as Warehouse Employee
    participant Inventory as Warehouse Inventory
    participant Reports as Warehouse Reports

    Manager->>RFID: Read tag (Quantity)
    RFID-->>Manager: Return quantity ()
    Manager->>Inventory: Add to stock
    Inventory-->>Manager: Added

    Employee->>RFID: Request wheat bag dates
    RFID-->>Employee: Return (dates)
    Employee->>Inventory: Release old wheat (FIFO)
    Inventory-->>Employee: Removed from stock

    Manager->>Reports: Request warehouse report
    Reports-->>Manager: Send report
```
  
### 4. Activity Diagrams
Step-by-step business workflows covering anomaly branches, alerting thresholds, and inventory updates.
* **Crop Image Capture & Analysis Flow:**
```mermaid
flowchart TD
    Start([Start]) --> A1[Initiate sensing]
    A1 --> A2[Test humidity]
    A2 --> A3[Gather sensor data - humidity]
    A3 --> A4[Get data insights]
    A4 --> D1{Anomaly detected?}
    
    D1 -- No --> A4
    D1 -- Yes --> A5[Send alert]
    A5 --> A6[Receive alert - Supervisor]
    A6 --> A7[Request sensor report]
    A7 --> A8[Generate sensor report]
    A8 --> A9[Receive sensor report]
    A9 --> EndNode([End])
```
```mermaid
flowchart TD
    Start([Start]) --> B1[Start capturing plant images]
    B1 --> B2[Request plant images]
    B2 --> B3[Send plant images]
    B3 --> B4[Get data insights - image data]
    
    B4 --> D_Dis{Crop diseases detected?}
    D_Dis -- Yes --> B5[Send alert]
    B5 --> B6[Receive alert - Supervisor]
    B6 --> B7[Request report]
    B7 --> B8[Generate report]
    B8 --> B9[Receive report]
    B9 --> EndNode([End])
    
    D_Dis -- No --> D_Grow{Plant growth adequate?}
    D_Grow -- Yes --> D_Cult{Plants need cultivation?}
    
    D_Cult -- Yes --> B10[Notify warehouse manager]
    B10 --> B11[Receive notification]
    
    D_Cult -- No --> B12[No incoming stock]
    B12 --> B13[Receive status]
```

* **FIFO Warehouse Release Workflow:**
 ```mermaid
flowchart TD
    Start([Start]) --> C1[Read RFID Tag]
    C1 --> C2[Return quantity]
    C2 --> C3[Add new stock to inventory]
    
    C3 --> C4[Request wheat dates]
    C4 --> C5[Return dates]
    C5 --> C6[Release old wheat by date - FIFO]
    C6 --> C7[Remove stock from inventory]
    
    C7 --> C8[Request warehouse report]
    C8 --> C9[Send report]
    C9 --> EndNode([End])
```
---

## 🛠️ Tools & Standards
* **Modeling Tool:** Visual Paradigm
* **Standard:** UML 2.0 (Use Case, Class, Sequence, Activity)
* **Target Architecture:** IoT Sensors, MQTT Broker, AWS Cloud Platform, RFID Tracking
