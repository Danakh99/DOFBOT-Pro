# DOFBOT-Pro

## ✅ Specs
- Robot: **Yahboom DOFBOT PRO**
- Platform: **Jetson Orin NX SUPER**
- OS: **Ubuntu + ROS2**
- Features: Vision sorting, MoveIt control, gesture control, QR tasks

---

## 📂 References  
**Restore System Image:**  
https://www.yahboom.net/study/Orin-NX-SUPER  

**DOFBOT PRO:**  
https://www.yahboom.net/study/DOFBOT-Pro  

---

## 📦 Requirements

### Hardware
- Jetson Orin NX SUPER
- DOFBOT PRO robot arm
- Orbbec depth camera
- Power supply & USB cables

### Software Packages
- Ubuntu (Yahboom pre-built image)
- ROS2 (included in Yahboom image)
- Python 3.8+
- CUDA (preinstalled on Yahboom image)

### Install Tools
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install python3-colcon-common-extensions python3-pip git ros-${ROS_DISTRO}-desktop

```

### Python Packages
```bash
pip install mediapipe opencv-python numpy
```

## 📥 Download Resources

- DOFBOT PRO system image: https://www.yahboom.net/study/DOFBOT-Pro  
- Jetson Orin NX SUPER system image: https://www.yahboom.net/study/Orin-NX-SUPER  

> Note: Vendor files and VM ZIPs are not uploaded to this repository.  
Please download from the official sources above.

---

## 🔧 Restore System Image
Flash the official Yahboom OS image to Jetson Orin NX SUPER before use.

---

## 🛠 Hardware Setup
- Jetson Orin NX SUPER
- DOFBOT PRO arm
- Orbbec depth camera
- ROS2 workspace

---

## 🚀 Usage Features

### 📱 Mobile App Control
To be documented after testing

---

### 🤖 MoveIt Control

**Result**
[![MoveIt Demo](media/moveit_demo.png)](https://drive.google.com/file/d/12Lj-xKwZIRodAGTPWEMM_14WD6o8gwvn/view?usp=drive_link)

```bash
cd ~/dofbot_pro_ws
colcon build
source install/setup.bash
ros2 run dofbot_pro_driver dofbot_pro_driver
ros2 launch dofbot_pro_moveit demo.launch.py
```

### ♻️ YOLOv11 Garbage Sorting

**Goal:** Sort garbage based on object category using YOLOv11

**Result**
[![Garbage Sorting](media/garbage_sorting.png)](https://drive.google.com/file/d/13vIG55xIh9PMsZIv3Id7WxpjcTBtx2Cl/view?usp=drive_link)

**Steps**
1. Close all terminals related to the app
2. Run:
```bash
ros2 launch orbbec_camera dabai_dcw2.launch.py
ros2 run dofbot_pro_driver arm_driver
ros2 run dofbot_pro_info kinemarics_dofbot
ros2 run dofbot_pro_yolov11 msgToImg
python3 ~/dofbot_pro_ws/src/dofbot_pro_yolov11/dofbot_pro_yolov11/yolov11.py
ros2 run dofbot_pro_yolov11 yolov11_sortation
```
3. Click on the result_image window
4. Press Spacebar to start processing


### 🧾 QR Sorting — Machine Code ID

**Result**
[![QR Sorting](media/qr_sorting.png)](https://drive.google.com/file/d/1wVS-a51UxX95Sapd7qaIn3J6jn5YoZIG/view?usp=drive_link)


```bash
ros2 launch orbbec_camera dabai_dcw2.launch.py
ros2 run dofbot_pro_info kinemarics_dofbot
ros2 run dofbot_pro_driver arm_driver
ros2 run dofbot_pro_driver apriltag_detect
ros2 run dofbot_pro_driver grasp
```
Then click the result image window and press Spacebar.

### 🎨 Color Sorting
[[ IN PROGRESS ]]

### 👋 Gesture Control — Mediapipe

Goal: Gesture-based pick and place

Steps

1. Close all terminals related to app development
2. Run:
```bash
ros2 run dofbot_pro_mediapipe 17_GestureGrasp
```

3. Place the middle-sized object
4. Show 5 fingers → pick
5. Show 1 finger → drop

## ⚡ Shortcut Commands

| Task | Command |
|---|---|
Build workspace | `colcon build` |
Source workspace | `source install/setup.bash` |
Run MoveIt | `ros2 launch dofbot_pro_moveit demo.launch.py` |

---

## 🧠 Under Development / Future Work

- Custom merged ROS2 package combining all previous features

---
