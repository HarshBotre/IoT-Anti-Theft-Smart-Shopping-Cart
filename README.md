# 🛒 IoT Anti-Theft Smart Shopping Cart

An IoT-enabled **Smart Shopping Cart** designed to automate the retail shopping and checkout experience using **barcode scanning, real-time weight verification, anti-theft validation, automated billing, and QR-based UPI payment**.

---

## 📌 Overview

Traditional shopping requires customers to manually carry products and wait at checkout counters for each item to be scanned and billed. This can result in long queues, manual billing errors, and difficulties in monitoring whether all products placed in a cart have been properly billed.

The **IoT Anti-Theft Smart Shopping Cart** addresses these challenges by integrating an **ESP32-based embedded system** with a barcode scanner, load cell, HX711 module, display, buttons, and QR-based payment functionality.

When a product is scanned, its product information and expected weight are registered by the system. The product is then placed in the cart, where the **load cell measures its actual weight**. The ESP32 compares the expected weight with the measured weight to verify the item.

If the weight matches the expected value within the defined tolerance, the item is accepted and added to the bill. A mismatch can indicate that an incorrect or unregistered item has been placed in the cart, providing an additional **anti-theft validation mechanism**.

At checkout, the system calculates the final bill and generates a **QR code for UPI payment**, enabling a convenient and contactless checkout experience.

---

## ✨ Key Features

* 🏷️ **Barcode-based Product Identification**
* ⚖️ **Real-Time Weight Measurement**
* 🛡️ **Weight-Based Anti-Theft Detection**
* 🧾 **Automatic Bill Generation**
* ❌ **Item Cancellation**
* 📺 **On-Device Bill Display**
* 📱 **QR-Based UPI Payment**
* 🔋 **Portable Battery-Powered System**
* 📡 **ESP32-Based IoT Architecture**
* 🛒 **Smart Shopping Cart Design**

---

## 🏗️ System Architecture

```text
                     ┌─────────────────────┐
                     │      PRODUCT        │
                     │      BARCODE        │
                     └──────────┬──────────┘
                                │
                                ▼
                     ┌─────────────────────┐
                     │   BARCODE SCANNER   │
                     │      DE2120         │
                     └──────────┬──────────┘
                                │
                                ▼
                     ┌─────────────────────┐
                     │       ESP32         │
                     │  MAIN CONTROLLER    │
                     └──────┬───────┬──────┘
                            │       │
              ┌─────────────┘       └─────────────┐
              ▼                                   ▼
     ┌─────────────────┐                 ┌─────────────────┐
     │  LOAD CELL +    │                 │     DISPLAY     │
     │     HX711       │                 │                 │
     └────────┬────────┘                 └─────────────────┘
              │
              ▼
     ┌─────────────────┐
     │ WEIGHT          │
     │ VERIFICATION    │
     └────────┬────────┘
              │
              ▼
     ┌─────────────────┐
     │ ANTI-THEFT      │
     │ VALIDATION      │
     └────────┬────────┘
              │
              ▼
     ┌─────────────────┐
     │ BILL GENERATION │
     └────────┬────────┘
              │
              ▼
     ┌─────────────────┐
     │ QR / UPI        │
     │ PAYMENT         │
     └─────────────────┘
```

---

## ⚙️ How It Works

### 1. Product Scanning

The customer scans the product barcode using the integrated **DE2120 barcode scanner**.

The ESP32 receives the barcode information and identifies the corresponding product.

```text
Product
   ↓
Barcode Scanner
   ↓
ESP32
   ↓
Product Information
```

The product information can include:

* Product name
* Price
* Expected weight

---

### 2. Weight Measurement

After scanning, the product is placed inside the shopping cart.

The **load cell** measures the actual weight of the product, while the **HX711 module** amplifies and converts the load-cell signal so that it can be processed by the ESP32.

```text
Product
   ↓
Load Cell
   ↓
HX711
   ↓
ESP32
```

---

### 3. Anti-Theft Validation

The ESP32 compares the product's expected weight with its measured weight.

```text
             Expected Weight
                    │
                    ▼
               ┌─────────┐
               │ COMPARE │
               └────┬────┘
                    ▲
                    │
              Actual Weight
```

### If the weight is valid:

```text
Weight Match
     ↓
Product Accepted
     ↓
Added to Bill
```

### If the weight is invalid:

```text
Weight Mismatch
      ↓
Validation Failed
      ↓
Item Not Accepted /
Alert Condition
```

This weight-verification mechanism provides the project's primary **anti-theft validation layer**.

---

## 🧾 Automatic Billing

After successful product validation, the item is added to the shopping cart's bill.

The system maintains a running total:

```text
Product 1 ──┐
Product 2 ──┤
Product 3 ──┼──► ESP32 ──► Total Bill
Product 4 ──┘
```

The display provides the user with information about the scanned products and current bill.

---

## ❌ Item Cancellation

A dedicated button allows the user to cancel/remove an item from the bill.

```text
Select Item
     ↓
Cancel
     ↓
Remove from Bill
     ↓
Update Total
     ↓
Update Display
```

---

## 💳 QR-Based UPI Payment

Once shopping is complete, the user selects the checkout option.

The system:

1. Calculates the final bill.
2. Generates a payment QR code.
3. Displays the QR code.
4. Allows the customer to make a UPI payment.

```text
Checkout
   ↓
Final Bill
   ↓
Generate QR
   ↓
Scan with UPI App
   ↓
Payment
```

---

## 🔧 Hardware Components

| Component                           | Purpose                                      |
| ----------------------------------- | -------------------------------------------- |
| **ESP32 Dev Board**                 | Main processing and communication controller |
| **SparkFun DE2120 Barcode Scanner** | Product identification                       |
| **Load Cell**                       | Measures product weight                      |
| **HX711**                           | Load-cell interface and signal amplification |
| **OLED/TFT Display**                | Displays product and billing information     |
| **Push Buttons**                    | User interaction and item cancellation       |
| **TP4056**                          | Battery charging                             |
| **Li-ion Batteries**                | Portable power source                        |
| **XL6009 Boost Converter**          | Voltage boosting                             |
| **3.3V Regulator**                  | Provides regulated 3.3V supply               |

---

## 💻 Software & Technologies

* **Arduino IDE**
* **C/C++**
* **ESP32**
* **Wi-Fi**
* **HX711 Library**
* **Display Libraries**
* **QR Code Generation**
* **Arduino IoT Cloud** *(where applicable)*

---

## 🔋 Power System

The project uses a rechargeable battery-based power system.

```text
       Li-ion Batteries
              │
              ▼
        ┌───────────┐
        │  TP4056   │
        │  Charger  │
        └─────┬─────┘
              │
              ▼
        ┌───────────┐
        │  XL6009   │
        │   Boost   │
        └─────┬─────┘
              │
              ▼
             5V
              │
        ┌─────┴──────┐
        │            │
        ▼            ▼
      ESP32     3.3V Regulator
                     │
                     ▼
              Peripheral Devices
```

The documented project uses three lithium-ion batteries connected in parallel with a TP4056 charging module and a boost-converter-based power arrangement.

---

## 📂 Repository Structure

```text
iot-anti-theft-smart-shopping-cart/
│
├── README.md
│
├── docs/
│   └── project-report.pdf
└── 
```

---

## 🎯 Applications

The system can be adapted for:

* 🛒 Smart supermarket shopping carts
* 🏪 Retail stores
* 🤖 Self-service checkout systems
* 🏬 Unmanned retail stores
* 📦 Inventory management
* 🛍️ Automated shopping systems
* 🎓 IoT and embedded-systems demonstrations

---

## ✅ Advantages

* Reduces checkout time
* Minimizes manual billing
* Provides weight-based item verification
* Adds an anti-theft validation mechanism
* Provides self-service shopping
* Supports contactless QR-based payment
* Portable and modular design
* Can be extended with additional IoT features

---

## ⚠️ Limitations

* Product information must be maintained in the system
* Load cell requires calibration
* Weight tolerance must be configured appropriately
* Compact displays provide limited information at one time
* Payment functionality requires appropriate implementation and testing
* Additional hardware may increase the size and weight of the cart

---

## 🔮 Future Enhancements

Potential improvements include:

* 📡 RFID-based product identification
* ☁️ Cloud-based inventory synchronization
* 📱 Dedicated Android/iOS application
* 🤖 AI-based fraud detection
* 👤 Biometric authentication
* 📊 Real-time inventory monitoring
* 🔔 Improved theft alerts
* 📈 Shopping and inventory analytics

---

## 📚 Documentation

Detailed project documentation is available in the `docs/` directory.

It includes:

* System architecture
* Hardware components
* Circuit design
* Power supply
* Program flow
* Implementation details
* Applications
* Future enhancements

---

## 🧑‍💻 Author

**Harsh Rajesh Botre**

Computer Science Engineering
IoT & Cyber Security Including Blockchain Technology
A. C. Patil College of Engineering

---

## 📌 Project Status

```text
🟢 Completed
```

---

## 📄 License

This project is intended for educational and personal project purposes.

See the `LICENSE` file for details.
