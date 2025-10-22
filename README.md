# Marathon Runtime Recorder

## Project Overview
The **Marathon Runtime Recorder** is an IoT-based system designed to accurately record player start and finish times during a marathon or race event using **RFID technology**.  
Each participant carries an **RFID tag** that is scanned at checkpoints to log timing data automatically in real time.

---

## Key Features
- **RFID-Based Timing:** Utilizes an **MFRC522 RFID reader** to detect player tags for precise start and end time recording.  
- **ESP32 Integration:** The RFID reader communicates with the **ESP32 microcontroller via SPI protocol**, enabling reliable and high-speed data capture.  
- **Wi-Fi Connectivity:** The ESP32 connects to the internet over **Wi-Fi (IEEE 802.11)** for cloud-based data transmission.  
- **Real-Time Data Logging:** Captured data is transmitted to the **Arduino IDE serial monitor** and simultaneously uploaded to **Google Sheets** for centralized tracking of player run times.  
- **Cloud-Based Visualization:** Uses **HTTP POST requests** to send player data securely to a **Google Form endpoint**, enabling live monitoring and data visualization through **Google Sheets**.  

---

## Technical Stack
- **Hardware:** ESP32, MFRC522 RFID Reader, RFID Tags  
- **Protocols:** RFID (ISO/IEC 14443A), SPI, Wi-Fi, HTTP/HTTPS  
- **Software:** Arduino IDE, Google Forms/Sheets, MATLAB *(optional for analysis)*  

---

## Communication Protocols Summary

| **Layer** | **Protocol** | **Communication Between** | **Purpose** |
|------------|---------------|----------------------------|--------------|
| **Physical / Data Link** | **RFID (ISO/IEC 14443A)** | RFID Tag ↔ MFRC522 Reader | Tag detection and data exchange |
| **Hardware Interface** | **SPI** | ESP32 ↔ MFRC522 | High-speed serial communication |
| **Network Layer** | **Wi-Fi (IEEE 802.11)** | ESP32 ↔ Router/Internet | Wireless network connectivity |
| **Application Layer** | **HTTP/HTTPS** | ESP32 ↔ Google Forms | Cloud data transfer via POST requests |

 **Protocol Flow:**  
`RFID Tag → MFRC522 (via RFID protocol) → ESP32 (via SPI) → Wi-Fi Network → Google Forms/Sheets (via HTTPS POST)`

---

##
## Setup Instructions

### Install Required Libraries
In **Arduino IDE**, go to  
`Sketch → Include Library → Manage Libraries...`  
and install the following:
- `MFRC522` – for RFID communication  
- `WiFi.h` – for ESP32 Wi-Fi connectivity  
- `GoogleFormPost.h` – for HTTP POST requests to Google Forms  

---

### Configure Wi-Fi Credentials
Update your Wi-Fi details in the code:

const char *ssid = "YourWiFiName";
const char *password = "YourWiFiPassword";

---

###  Setup Google Sheets

- Create Google form with requred input fields like player name, id
- Submit a sample response to automatically generate a linked sheet
- Add the form's public link in the code

#define FORM_ROOT_URL "Form Link"

- Identify form field IDs and map them in the code

---

### Upload and Run

- Connect the ESP32 to your laptop and select the COM port
- Upload the sketch via Arduino IDE
- Open Serial Monitor to view Wi-Fi amd RFID logs.
- When a RFID card is tapped, player data automatically updates in the Google sheet.
