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

## 📊 System Diagrams & Documentation

### 1. Use Case Diagram
Models external actors (sensors, supervisors, warehouse operators) and interactions with the MQTT broker and core system logic.
![Use Case Diagram](diagrams/use-case-diagram.png)

### 2. Class Diagram
Defines the object structure, attributes, data types, and inter-class relationships.
![Class Diagram](diagrams/class-diagram.png)

### 3. Sequence Diagrams
Illustrates the temporal exchange of messages between microcontrollers, sensors, cloud services, and actors:
* **Greenhouse Monitoring & Anomaly Alerting:**
  ![Sequence Diagram - Sensor](diagrams/sequence-diagram-temp.png)
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
