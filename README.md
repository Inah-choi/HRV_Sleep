# 🛌 Smart_Blind_HRV

Real-time Sleep Stage Classification with HRV from the MAX30102 Sensor on Raspberry Pi  

This repository enables real-time classification of sleep stages using Heart Rate Variability (HRV) signals collected from the MAX30102 sensor on a Raspberry Pi.  
It utilizes preprocessing, feature extraction, and deep learning (LSTM-based) classification pipelines based on the [`sleep-analysis`](https://github.com/mad-lab-fau/sleep_analysis) framework.

---

## 📡 Components

- **Sensor**: MAX30102 (IR signal for HRV)
- **Hardware**: Raspberry Pi with GPIO button
- **Software**: Python + sleep-analysis framework
- **Classification**: LSTM or other ML/DL models
- **Optional**: Control smart blinds based on sleep stage

---

## 🔧 1. Raspberry Pi Setup

---

## 🔌 Driver Installation (for Raspberry Pi)

To use the MAX30102 sensor with this project, please follow these setup steps:

### ✅ 1. Enable I2C Interface

Open the terminal and run:

```bash
sudo raspi-config
```

- Navigate to: `5 Interfacing Options`
- Select: `P5 I2C` → Press Enter
- Confirm with `YES` and reboot the Raspberry Pi

---

### ✅ 2. Install Required System Packages

Make sure your Raspberry Pi is connected to the Internet, then run:

```bash
sudo apt-get update
sudo apt-get install -y build-essential python-dev python-smbus git
```

---

### ✅ 3. Download the Blood Oxygen Driver Library

Clone the official MAX30102 driver provided by DFRobot:

```bash
cd ~/Desktop/
git clone https://github.com/DFRobot/DFRobot_BloodOxygen_S
```

After cloning, your Python scripts should import the driver from this location:
```
DFRobot_BloodOxygen_S/python/DFRobot_BloodOxygen_S.py
```

---

> ⚠️ If you move the folder, make sure to update the `sys.path.append(...)` line in `max30102_reader.py` accordingly.

## 📦 2. Python Environment Setup

### Using Poetry (recommended)
```bash
poetry install
```

### Or with pip
```bash
pip install -r requirements.txt
```

---

## 🩺 3. HRV Data Collection

Collect data from the MAX30102 sensor:

```bash
python hrv_input/max30102_reader.py
```

→ Data will be saved to `hrv_input/data_buffer.csv`.

---

## 🧠 4. Real-Time Sleep Stage Classification

This script listens for a physical button press and performs repeated HRV analysis:

```bash
python run_real_time_pipeline.py
```

Each cycle performs:

✅ Collects HRV from MAX30102  
✅ Preprocesses the IR signal (ECG-like)  
✅ Extracts HRV features  
✅ Runs the classification model (e.g., LSTM)  
✅ Predicts and prints the sleep stage

---
## 📁 Project Structure

```
Smart_Blind_HRV_module/
├── DFRobot_BloodOxygen_S/         # ✅ MAX30102 공식 Python 드라이버 (GitHub에서 clone)
│   └── python/
│       └── DFRobot_BloodOxygen_S.py
│
├── hrv_input/                     # HRV 수집 모듈
│   └── max30102_reader.py         # MAX30102에서 HR 데이터 수집 (SpO2 제외)
│
├── models/                        # 사전 학습된 수면 분류 모델
│   └── lstm_model.h5
│
├── sleep-analysis/               # 수면 분석 프레임워크 (전처리/분류/특징 추출 등)
│   └── ...
│
├── run_real_time_pipeline.py     # 메인 실행 스크립트 (버튼 누르면 반복 측정 및 추론)
├── pyproject.toml                # Poetry 기반 Python 의존성 설정
├── poetry.lock                   # 고정된 의존성 버전 정보
└── README.md                     # 📝 프로젝트 설명서
