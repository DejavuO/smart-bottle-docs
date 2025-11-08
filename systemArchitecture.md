# System Architecture – Smart Bottle Plus

## 🏗️ Overview
Smart Bottle Plus is a hybrid physical-digital product.  
The core bottle includes a digital clock and buzzer controlled by an embedded microcontroller.  
Bluetooth Low Energy (BLE) enables communication with a lightweight mobile app, which stores and syncs reminder schedules.  

This architecture ensures that the bottle works **independently for reminders**, while the app can optionally provide **backup, tracking, and remote configuration**.

---

## 🔹 Hardware Layer (Bottle)
| Component | Function |
|-----------|---------|
| **Microcontroller (MCU)** | Controls clock display, buzzer, and handles BLE communication |
| **Real-Time Clock (RTC)** | Maintains accurate time for display and reminders |
| **Digital Display** | Shows current time and reminder icons |
| **Piezo Buzzer** | Provides gentle reminder alerts |
| **Buttons** | Allow on-device time and schedule setup |
| **Battery + Power Circuit** | Supplies power and manages USB-C charging |
| **Bluetooth Module (BLE)** | Connects to mobile app for syncing reminders |

**Firmware Responsibilities:**
- Timekeeping and alarm scheduling  
- Reading button inputs  
- Activating buzzer  
- BLE communication (send/receive reminder settings)  
- Power-saving sleep modes  

---

## 🔹 Software Layer
| Layer | Technology | Role |
|-------|-----------|-----|
| **Frontend (Mobile App)** | React Native | User interface for setting reminders and syncing with bottle |
| **Backend (API Server)** | Node.js + Express | Receives/sends data from app, validates user settings |
| **Database** | MongoDB Atlas | Stores user profiles and reminder schedules |

---

## 🔹 Communication Flow
Smart Bottle communicates with the app via Bluetooth.  
The app can optionally sync data to the server, which stores user information in the database.  

```text
[ Smart Bottle Hardware ]
        ⇅  Bluetooth LE
[ Mobile App (React Native) ]
        ⇅  HTTPS / REST API
[ Node.js Server ]
        ⇄
[ MongoDB Database ]
```

## 🖼️ System Architecture Diagram

        ┌─────────────────────────────┐
        │      Smart Bottle           │
        │  (Digital Clock + Buzzer +  │
        │       Microcontroller)      │
        └─────────────┬──────────────┘
                      │  Bluetooth LE
                      ▼
        ┌─────────────────────────────┐
        │       Mobile App            │
        │      (React Native)         │
        └───────┬─────────┬──────────┘
                │         │ HTTPS / REST API
                │         ▼
                │   ┌───────────────┐
                │   │ Backend Server│
                │   │ (Node.js +    │
                │   │  Express)     │
                │   └───────┬──────┘
                │           │
                ▼           ▼
        ┌─────────────────────────────┐
        │       MongoDB Atlas         │
        │       (Database)            │
        └─────────────────────────────┘


## 🔹 Data Model Example

This example shows how user information and reminder schedules are stored in the database.  
It helps developers understand the structure of the data used by the Smart Bottle Plus app.

```json
{
  "userId": "A102",
  "reminderTimes": ["09:00", "11:30", "14:00", "17:00"],
  "bottleSync": true,
  "lastSync": "2025-11-07T09:30:00Z"
}
```
Explanation of Fields:
- `userId` → unique identifier for each user
- `reminderTimes`→ array of times for hydration reminders
- `bottleSync`→ indicates whether the bottle has synced with the app
- `lastSync`→ timestamp of the last successful sync

## 🔹 Technical Feasibility

### Hardware:
- Uses standard, inexpensive components (microcontroller, digital clock, buzzer, BLE module, battery).
- Components are widely available and proven to work together.

### Software:
- Mobile app is built using mainstream development tools.
- Backend and database use standard technologies for reliable storage and retrieval.

### Summary:
Because all components and frameworks are standard, widely available, and low-cost, Smart Bottle Plus can be prototyped, built, and scaled without relying on experimental or untested technology.

## 🔹 Future Enhancements

These are potential improvements planned for Smart Bottle Plus:
- Add water-level sensor to track actual consumption  
- Integrate with wearable health dashboards for overall wellness tracking  
- Voice-activated reminders for hands-free alerts  
- Analytics dashboard to visualize user hydration trends over time  
- Option to customize reminder sounds or vibration patterns

