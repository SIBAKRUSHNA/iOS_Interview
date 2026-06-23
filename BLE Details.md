
# 📶 BLE (Bluetooth Low Energy) in iOS

<img width="1024" height="1536" alt="ChatGPT Image Jun 23, 2026, 12_21_30 PM" src="https://github.com/user-attachments/assets/b683f9cc-578c-44f1-a736-3510296df33a" />


## What is BLE?

**Bluetooth Low Energy (BLE)** is a wireless communication technology designed for low power consumption and short-range communication between devices.

### Common BLE Devices
- ⌚ Smart Watches
- 💓 Heart Rate Monitors
- 🏃 Fitness Bands
- 🏠 Smart Home Devices
- 🔒 Smart Locks
- 🌡️ IoT Sensors

---

# BLE vs Classic Bluetooth

| BLE | Classic Bluetooth |
|------|------|
| Low Power Consumption | Higher Power Consumption |
| Small Data Transfer | Large Data Transfer |
| Fast Connection | Slower Connection |
| Battery Efficient | More Battery Usage |
| IoT Devices | Audio Streaming |

---

# CoreBluetooth Framework

Apple provides the **CoreBluetooth** framework for BLE communication.

```swift
import CoreBluetooth
```

---

# BLE Architecture

```text
Central (iPhone)
      │
      ▼
Peripheral (BLE Device)
      │
      ▼
Service
      │
      ▼
Characteristic
```

### Example

```text
Heart Rate Monitor
    └── Heart Rate Service
            └── Heart Rate Characteristic
```

---

# Main BLE Components

## 1. CBCentralManager

Responsible for:

- Scanning devices
- Connecting devices
- Managing Bluetooth state

```swift
let centralManager = CBCentralManager(
    delegate: self,
    queue: nil
)
```

---

## 2. CBPeripheral

Represents a BLE device.

Examples:

- Smart Watch
- Fitness Tracker
- BLE Sensor

```swift
var peripheral: CBPeripheral?
```

---

## 3. Service

A logical grouping of related data.

Examples:

- Heart Rate Service
- Battery Service
- Device Information Service

```text
Peripheral
    └── Service
```

---

## 4. Characteristic

Contains actual data inside a service.

Examples:

- Heart Rate Value
- Battery Percentage
- Temperature Value

```text
Service
    └── Characteristic
```

---

# BLE Connection Flow

## Step 1: Create Central Manager

```swift
centralManager = CBCentralManager(
    delegate: self,
    queue: nil
)
```

---

## Step 2: Check Bluetooth State

```swift
func centralManagerDidUpdateState(
    _ central: CBCentralManager
) {
    if central.state == .poweredOn {
        print("Bluetooth ON")
    }
}
```

---

## Step 3: Scan Devices

```swift
centralManager.scanForPeripherals(
    withServices: nil,
    options: nil
)
```

---

## Step 4: Discover Device

```swift
func centralManager(
    _ central: CBCentralManager,
    didDiscover peripheral: CBPeripheral,
    advertisementData: [String : Any],
    rssi RSSI: NSNumber
) {
    print(peripheral.name ?? "")
}
```

---

## Step 5: Connect Device

```swift
centralManager.connect(peripheral)
```

---

## Step 6: Discover Services

```swift
peripheral.discoverServices(nil)
```

---

## Step 7: Discover Characteristics

```swift
peripheral.discoverCharacteristics(
    nil,
    for: service
)
```

---

## Step 8: Read Data

```swift
peripheral.readValue(
    for: characteristic
)
```

---

## Step 9: Write Data

```swift
let data = "Hello".data(using: .utf8)!

peripheral.writeValue(
    data,
    for: characteristic,
    type: .withResponse
)
```

---

# Characteristic Properties

| Property | Description |
|-----------|------------|
| Read | Read Data |
| Write | Write Data |
| Notify | Receive Updates |
| Indicate | Reliable Notification |
| Broadcast | Broadcast Data |

Example:

```swift
if characteristic.properties.contains(.read) {
    print("Readable")
}
```

---

# Read vs Notify

## Read

Fetches the value once.

```swift
peripheral.readValue(for: characteristic)
```

### Use Cases
- Battery Percentage
- Device Name
- Firmware Version

---

## Notify

Receives continuous updates.

```swift
peripheral.setNotifyValue(
    true,
    for: characteristic
)
```

### Use Cases
- Heart Rate Monitor
- Temperature Sensor
- Live Sensor Data

---

# BLE Delegate Methods

## Device Discovered

```swift
didDiscover
```

## Device Connected

```swift
didConnect
```

## Device Disconnected

```swift
didDisconnectPeripheral
```

## Services Discovered

```swift
didDiscoverServices
```

## Characteristics Discovered

```swift
didDiscoverCharacteristicsFor
```

## Characteristic Value Updated

```swift
didUpdateValueFor
```

---

# Bluetooth States

```swift
.poweredOn
.poweredOff
.resetting
.unauthorized
.unsupported
.unknown
```

---

# RSSI (Signal Strength)

RSSI = **Received Signal Strength Indicator**

| RSSI Value | Signal Strength |
|------------|---------------|
| -30 dBm | Excellent |
| -50 dBm | Strong |
| -60 dBm | Good |
| -70 dBm | Fair |
| -90 dBm | Weak |

---

# MTU (Maximum Transmission Unit)

**MTU** defines the maximum amount of data that can be sent in a single BLE packet.

### Benefits of Larger MTU

- Faster data transfer
- Fewer packets
- Better performance

---

# BLE Interview Questions

## 1. What is BLE?

Bluetooth Low Energy is a low-power wireless communication protocol used for IoT and wearable devices.

---

## 2. What is CoreBluetooth?

Apple's framework used to communicate with BLE devices.

---

## 3. What is CBCentralManager?

Used to scan and connect BLE devices.

---

## 4. What is CBPeripheral?

Represents a remote BLE device.

---

## 5. What is a Service?

A collection of related characteristics.

---

## 6. What is a Characteristic?

A container that stores actual data.

---

## 7. Difference Between Read and Notify?

| Read | Notify |
|--------|--------|
| One-time Data Fetch | Continuous Updates |
| Manual Request | Automatic Updates |

---

## 8. What is RSSI?

Signal strength measurement between central and peripheral.

---

## 9. What is MTU?

Maximum packet size transferred over BLE.

---

## 10. Difference Between BLE and Classic Bluetooth?

BLE is optimized for low power and small data transfer, whereas Classic Bluetooth is designed for continuous high-bandwidth communication.

---

# Real-World Example

## Heart Rate Monitor

```text
iPhone (Central)
        │
        ▼
Heart Rate Sensor (Peripheral)
        │
        ▼
Heart Rate Service
        │
        ▼
Heart Rate Characteristic
        │
        ▼
72 BPM
```

The iPhone subscribes to notifications and receives heart-rate updates continuously.

---

# Quick Revision

```text
BLE
├── CBCentralManager
├── CBPeripheral
├── Service
├── Characteristic
├── Read
├── Write
├── Notify
├── RSSI
├── MTU
└── CoreBluetooth
```

## Key Points

✅ Low Power Communication  
✅ Uses CoreBluetooth Framework  
✅ Central ↔ Peripheral Architecture  
✅ Service → Characteristic Hierarchy  
✅ Read, Write, Notify Operations  
✅ Widely Used in IoT & Wearable Devices
