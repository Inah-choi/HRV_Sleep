# 🛌 Smart_Blind_HRV_module

Real-time Sleep Stage Classification with HRV from MAX30102 Sensor on Raspberry Pi  
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)

This repository enables real-time classification of sleep stages using Heart Rate Variability (HRV) signals measured with the MAX30102 sensor on Raspberry Pi.  
The system uses preprocessing, feature extraction, and deep learning (LSTM-based) classification pipelines from the [`sleep-analysis`](https://github.com/mad-lab-fau/sleep_analysis) framework.

---

## 📡 Components

- **Sensor**: MAX30102 (IR signal for HRV)
- **Hardware**: Raspberry Pi with GPIO button
- **Software**: Python + sleep-analysis framework
- **Classification**: LSTM or other ML/DL models
- **Optionally**: Control smart blinds based on sleep stage

---

## 🔧 1. Raspberry Pi Setup

### ✅ Enable I2C Interface
```bash
sudo raspi-config
# → 5 Interfacing Options → P5 I2C → YES
# → Reboot after enabling
