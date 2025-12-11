# WhatsApp Activity Tracker - Full Stack Analytics

> ⚠️ **DISCLAIMER**: Proof-of-concept for educational and security research purposes only. Demonstrates privacy vulnerabilities in WhatsApp and Signal.

## Overview

This project implements the research from the paper **"Careless Whisper: Exploiting Silent Delivery Receipts to Monitor Users on Mobile Instant Messengers"** by Gabriel K. Gegenhuber, et al.

**What it does:** By measuring Round-Trip Time (RTT) of WhatsApp message delivery receipts, this tool can detect:
- When a user is actively using their device (low RTT)
- When the device is in standby/idle mode (higher RTT)
- Activity patterns over time (Sleep/Wake cycles)

**Security implications:** This demonstrates a significant privacy vulnerability in messaging apps that can be exploited for surveillance.

## Features

- **Real-time Tracking:** Live RTT gauge and status updates via Socket.IO.
- **Persistent History:** MongoDB storage for long-term data analysis.
- **Analytics Dashboard:**
    - **24h Timeline:** Visual history of Online/Standby states.
    - **Activity Heatmap:** Hourly intensity charts.
    - **Sleep Estimation:** Automated detection of longest inactivity periods.
- **Multi-Device Support:** Track multiple contacts simultaneously.
- **Modern UI:** React + Vite + TailwindCSS + Recharts.

## Tech Stack

- **Backend:** Node.js, Express, Socket.IO, `@whiskeysockets/baileys`
- **Database:** MongoDB (Mongoose)
- **Frontend:** React, Vite, TailwindCSS, Recharts

## Installation

### Prerequisites
- Node.js 16+
- MongoDB (running locally or via Atlas URI)
- WhatsApp Account (for the tracking session)

### Setup

1. **Clone repository**
   ```bash
   git clone https://github.com/gommzystudio/device-activity-tracker.git
   cd device-activity-tracker
   ```

2. **Install dependencies**
   ```bash
   npm install
   cd client && npm install && cd ..
   ```

3. **Database Configuration**
   By default, the app connects to `mongodb://localhost:27017/whatsapp-tracker`.
   To use a different URI, set the `MONGODB_URI` environment variable.

## Usage

### Web Dashboard (Recommended)

1. **Start the Backend Server**
   ```bash
   npm run start:server
   ```
   *The server runs on port 3001.*

2. **Start the Frontend Client**
   ```bash
   npm run start:client
   ```
   *The client runs on http://localhost:5173.*

3. **Authenticate**
   - Open the client URL.
   - Scan the QR code with your WhatsApp (Linked Devices).

4. **Start Tracking**
   - Enter a target phone number (with country code, e.g., `491701234567`) in the sidebar.
   - View real-time metrics and historical analytics.

### CLI Interface

```bash
npm start
```
Follow prompts to authenticate and enter target number. Note: CLI does not support the visual dashboard or persistent history features.

## Project Structure

```
device-activity-tracker/
├── src/
│   ├── database.ts     # MongoDB connection & Schema
│   ├── tracker.ts      # Core RTT analysis & DB saving
│   ├── server.ts       # Express API & Socket.IO
│   └── index.ts        # CLI entry point
├── client/             # Vite + React Frontend
│   ├── src/
│   │   ├── components/ # Dashboard Widgets (Gauge, Graph, etc.)
│   │   └── App.tsx     # Main Layout
└── package.json
```

## Ethical & Legal Considerations

⚠️ **For research and educational purposes only.**
Never track people without explicit consent - this may violate privacy laws (e.g., GDPR, stalking laws). Authentication data is stored locally (`auth_info_baileys/`) and must never be shared.

## License

MIT License - See LICENSE file.

Built with [@whiskeysockets/baileys](https://github.com/WhiskeySockets/Baileys)
