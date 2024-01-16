# Heartbeat Based Authentication in Wearable Devices
## Introduction
This project focuses on developing a secure, spoof-proof authentication system for wearable devices using heartbeat-based authentication. As wearable technology evolves, there is an increasing need for robust security solutions. This project aims to provide an alternative to traditional methods like passwords and biometrics, which are susceptible to various vulnerabilities.

## Why Heartbeat?
### Heartbeat-based authentication offers several advantages over conventional methods:
- Security: Heartbeats are unique to individuals and do not leave biometric data exposed.
- Reliability: Relies on the biological features of the heart, closely linked to the user's liveliness and emotions.
- Resistance to Forgery: Difficult to replicate or forge compared to fingerprints or facial recognition.

## System Overview
The authentication process is based on the seismocardiogram (SCG) principle, using the accelerometer in a sensorTag to capture chest vibrations in response to heartbeats. The system involves:

- Data Collection and Normalization: To create a unique model for each user.
-User Authentication: Differentiating users based on their unique heartbeat models.

## Project Outline
- Heartbeat Collection: Using UDP over 6LoWPAN for data transmission.
- Segmentation and Feature Extraction: Utilizing Wavelet-based Feature Extraction (DWT algorithm).
- Machine Learning Model: Employing Supervised Machine Learning for user authentication.

## Challenges and Solutions
Addressing issues with the Contiki clock and accelerometer precision.
Implementing
UDP data transmission and handling clock precision issues.
Evaluation and Testing: Conducting tests to measure authentication accuracy and address challenges in data transmission and precision.

## Technologies Used
- Blockchain Platform: Ethereum for secure transactions.
- Off-Chain Components:
  - Oracle: Chain Link for decentralized oracles.
  - Database: Cloud storage for additional data related to heartbeat patterns.
- Machine Learning: Support Vector Machines and Neural Networks for pattern recognition and authentication.

# Connect to Border Router
1) Create modern Ubuntu VM 
2) `git clone https://github.com/contiki-os/contiki.git`
3) run `make tunslip6` (in contiki/tools)
4) install net-tools with `sudo apt-get update -y` and `sudo apt-get install -y net-tools`
5) Install required python dependenices
6) Connect sensortag with USB cable
7) run `sudo ./tunslip6 -B 115200 -s /dev/ttyACM0 aaaa::1/64` (in contiki/tools)
8) run python script

# Heartbeat Authentication

Base files added. 
Currently some of the hearbeat data seems to increase continuously as per the plots. Better samples needed

pip install matplotlib

# Increased Precision of Accelerometer
Too increase the precision from the accelerometer please replace the original contiki driver with the modified driver `mpu-9250-sensor.c`. It returns the raw sensor value. It can be converted to G with the following formula:

(raw_data * 1.0) / (32768 / 2);

You find the file in `contiki-git/platform/srf06-cc26xx/sensortag`

To use that file please make sure to run `make clean` before building the source code. (FYI: The sensor is per default in 2G range configured that has the highest possible precision.)
