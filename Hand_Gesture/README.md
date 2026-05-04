# Hand Gesture Detection & LED Control

A real-time hand gesture detection system that recognizes finger positions using a webcam and controls Arduino-connected LEDs based on the detected finger count.

## Project Overview

This project combines computer vision with embedded systems to create an interactive gesture-controlled LED display. It uses your webcam to detect hand gestures and translates them into LED lighting patterns on an Arduino board.

**Features:**
- Real-time hand detection and finger tracking
- Displays finger count on video feed (0-5 fingers)
- Controls 5 LEDs on an Arduino board based on detected fingers
- Support for single hand detection
- Live video preview with gesture recognition

## Project Structure

```
Hand/
├── main.py          # Main application with webcam capture and hand detection
├── controller.py    # Arduino LED control module
└── README.md        # This file
```

## Requirements

### Hardware
- Computer with webcam
- Arduino board (e.g., Arduino Uno)
- 5 LEDs with appropriate resistors
- USB cable for Arduino connection
- Jumper wires

### Software
- Python 3.6+
- OpenCV (`cv2`)
- cvzone with HandTrackingModule
- PyFirmata
- Arduino IDE (for uploading StandardFirmata to your Arduino)

## Installation

### 1. Install Python Dependencies

```bash
pip install opencv-python cvzone pyfirmata
```

### 2. Arduino Setup

1. Download and install [Arduino IDE](https://www.arduino.cc/en/software)
2. Connect your Arduino to your computer via USB
3. Open Arduino IDE → File → Examples → Firmata → StandardFirmata
4. Upload the sketch to your Arduino board

### 3. Hardware Wiring

Connect LEDs to your Arduino as follows:
- LED 1 → Pin 8
- LED 2 → Pin 9
- LED 3 → Pin 10
- LED 4 → Pin 11
- LED 5 → Pin 12

Each LED should have a current-limiting resistor (typically 220Ω) in series.

## Configuration

Before running the application, update the COM port in `controller.py`:

```python
comport='COM9'  # Change to your Arduino's COM port
```

**To find your COM port:**
- **Windows:** Arduino IDE → Tools → Port
- **Linux/Mac:** Run `ls /dev/tty.*` in terminal

## Usage

### Basic Usage

```bash
python main.py
```

**Controls:**
- Press `k` to quit the application

### How It Works

1. The application captures video from your default webcam
2. Hand Detector identifies your hand and tracks finger positions
3. The system determines how many fingers are raised (0-5)
4. LEDs light up sequentially based on finger count:
   - 0 fingers: All LEDs off
   - 1 finger: LED 1 on
   - 2 fingers: LED 1-2 on
   - 3 fingers: LED 1-3 on
   - 4 fingers: LED 1-4 on
   - 5 fingers: All LEDs on

## File Details

### main.py
- Captures video from webcam
- Detects hands and tracks finger positions
- Displays finger count overlay on video
- Calls LED control functions based on detected gestures

### controller.py
- Connects to Arduino via PyFirmata
- Maps finger detection to LED control
- Controls individual LED pins (8-12) on the Arduino

## Troubleshooting

| Issue | Solution |
|-------|----------|
| `pyfirmata.util.serial.SerialException` | Check COM port in `controller.py` matches Arduino's port |
| Hand not detected | Ensure good lighting, adjust `detectionCon=0.8` parameter |
| LEDs not responding | Verify Arduino wiring and that StandardFirmata is uploaded |
| Webcam not working | Check if another app is using the camera, or use `cv2.VideoCapture(1)` for secondary camera |

## Dependencies Reference

- **OpenCV (cv2)** - Video capture and image processing
- **cvzone** - Hand tracking and gesture recognition
- **PyFirmata** - Arduino communication protocol

## Future Enhancements

- [ ] Support for two-hand detection
- [ ] Additional gesture recognition (swipe, pinch, etc.)
- [ ] Configurable LED patterns
- [ ] Multiple LED boards support
- [ ] Web interface for remote control
- [ ] Hand gesture recording and playback

## License

MIT License

## Author

Hand Gesture Detection System

## Support

For issues or questions, please check the troubleshooting section above or verify your Arduino connections and Python dependencies.
