# System Architecture – Smart Bottle Plus

## 🏗️ Overview
Smart Bottle Plus is a hybrid physical-digital product.  
The core bottle includes a digital clock and buzzer controlled by an embedded microcontroller.  
In this iteration, Bluetooth Low Energy enables communication with a lightweight mobile app that stores and syncs reminder schedules.

---

## 🔹 Hardware Layer (Bottle)
| Component | Function |
|------------|-----------|
| **Microcontroller (MCU)** | Controls clock display, buzzer, and handles BLE communication |
| **Real-Time Clock (RTC)** | Maintains accurate time for display and reminders |
| **Digital Display** | Shows current time and reminder icons |
| **Piezo Buzzer** | Provides gentle reminder alerts |
| **Buttons** | Allow on-device time and schedule setup |
| **Battery + Power Circuit** | Provides power and manages charging via USB-C |
| **Bluetooth Module (BLE)** | Connects to mobile app for data sync |

**Firmware Responsibilities**
- Timekeeping and alarm scheduling  
- Reading button inputs  
- Activating buzzer  
- BLE communication (send/receive reminder settings)  
- Power-saving sleep modes  

---

## 🔹 Software Layer
| Layer | Technology | Role |
|:------|:------------|:----|
| **Frontend (Mobile App)** | React Native | User interface for setting reminders and viewing hydration logs |
| **Backend (API Server)** | Node.js + Express | Receives/sends data from the app, validates user settings |
| **Database** | MongoDB Atlas | Stores user profiles and reminder schedules |

---

## 🔹 Communication Flow
```text
[ Smart Bottle Hardware ]
        ⇅  Bluetooth LE
[ React Native App ]
        ⇅  HTTPS / REST API
[ Node.js Server ]
        ⇄
[ MongoDB Database ]


🔹 Data Model Example
{
  "userId": "A102",
  "reminderTimes": ["09:00", "11:30", "14:00", "17:00"],
  "bottleSync": true,
  "lastSync": "2025-11-07T09:30:00Z"
}

🔹 Technical Feasibility

All components use readily available embedded modules.

BLE ensures low-energy, offline functionality.

MERN-based stack (React Native, Node.js, MongoDB) supports rapid prototyping.

Firmware and app both operate independently — reliable even when offline.



