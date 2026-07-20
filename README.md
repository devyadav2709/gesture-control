# 🖐️ Gesture Control Presenter

Control Google Slides (or any keyboard-driven presentation tool) hands-free — using just your webcam and hand gestures.

Built with **OpenCV**, **MediaPipe**, and **PyAutoGUI**, this app tracks your hand in real time, counts how many fingers are up, and translates that into keyboard shortcuts like *next slide*, *previous slide*, *start*, and *exit*.

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![MediaPipe](https://img.shields.io/badge/MediaPipe-0.10.35-green)
![OpenCV](https://img.shields.io/badge/OpenCV-4.8%2B-orange)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

---

## ✨ Features

- 🎥 Real-time hand tracking directly from your laptop webcam
- 🖐️ Finger-counting gesture recognition (no extra hardware needed)
- ⌨️ Maps gestures to keyboard shortcuts via PyAutoGUI
- 🧠 Powered by Google's MediaPipe Hand Landmarker model
- ⏱️ Built-in cooldown to prevent repeated/accidental key presses
- 🪞 Mirrored camera view for a natural, intuitive feel

---

## 🧠 Gesture Controls

| Gesture | Fingers Up | Action |
|---|---|---|
| ✋ Open Palm | 4 | Next Slide |
| 🤟 Three Fingers | 3 | Previous Slide |
| ✌️ Two Fingers | 2 | Start Slideshow |
| ✊ Fist | 0 | Exit Slideshow |

> Gestures are recognized once per `cooldown` window (default: **1.5 seconds**) to avoid firing the same action multiple times while your hand is held in position.

---

## 🛠️ Tech Stack

| Library | Purpose |
|---|---|
| [OpenCV](https://opencv.org/) | Webcam capture, image processing, on-screen drawing |
| [MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/guide) | Hand landmark detection (21 keypoints per hand) |
| [PyAutoGUI](https://pyautogui.readthedocs.io/) | Simulating keyboard presses to control slides |

---

## 📦 Installation

### Step 0 — Make sure Python is installed

> On Linux/macOS use `python3` instead of `python` in the commands below.

```bash
python -V
```

### Step 1 — Get the code

```bash
git clone https://github.com/shivam-kotwalia/gesture-control.git
cd gesture-control
```

Or download the ZIP directly:

```
https://github.com/shivam-kotwalia/gesture-control/archive/refs/heads/main.zip
```

### Step 2 — Install dependencies

```bash
python -m pip install --break-system-packages -r requirements.txt
```

### Step 3 — Download the hand landmark model

The app needs a MediaPipe `hand_landmarker.task` model file, which isn't checked into the repo. Download it with:

```bash
python setup_models.py
```

This saves the model to `models/hand_landmarker.task`, trying multiple sources automatically if one fails.

---

## ▶️ Usage

1. Open **Google Slides** (or any app you control with arrow keys / Esc / Enter) in your browser.
2. Run the app:

   ```bash
   python main.py
   ```
3. A window titled **"Google Slides Gesture Control"** will open showing your webcam feed with hand landmarks drawn on top.
4. Hold up the corresponding gesture in front of your camera to trigger an action.
5. Press **`q`** in the preview window to quit the app (or `Ctrl+C` in the terminal).

---

## 💻 macOS Permission Setup

Simulated keyboard input requires extra permissions on macOS. Without these, gestures will be detected but slides won't actually change.

Go to **System Settings → Privacy & Security**, and grant the following to your terminal (Terminal, VS Code, or PyCharm — whichever you run the script from):

- ✅ Accessibility
- ✅ Input Monitoring

---

## 📂 Project Structure

```
gesture-control/
│
├── main.py            # Main application: capture, detection, gesture mapping
├── setup_models.py     # Downloads the MediaPipe hand_landmarker model
├── requirements.txt    # Python dependencies
├── .gitignore
├── README.md
└── models/
    └── hand_landmarker.task   # Downloaded, not tracked in git
```

---

## ⚙️ How It Works

1. **Capture** — OpenCV reads frames from the webcam and mirrors them for natural interaction.
2. **Detect** — Each frame is converted to RGB and passed to MediaPipe's `HandLandmarker`, which returns 21 3D landmarks per detected hand.
3. **Interpret** — `fingers_up()` compares each fingertip's height to its corresponding knuckle (PIP joint) to decide if that finger is extended.
4. **Map** — The total number of extended fingers is matched against the gesture table above.
5. **Act** — `pyautogui` fires the matching key press (`right`, `left`, `esc`, or `cmd+enter`), respecting the cooldown so a held gesture doesn't spam the same action.
6. **Display** — The current gesture label and hand skeleton are drawn on the live preview window.

---

## 🔧 Configuration

A few values in `main.py` you may want to tune:

| Variable | Default | Description |
|---|---|---|
| `min_hand_detection_confidence` | `0.7` | Minimum confidence to detect a hand |
| `min_hand_presence_confidence` | `0.7` | Minimum confidence that a hand is present |
| `min_tracking_confidence` | `0.7` | Minimum confidence to keep tracking a hand |
| `cooldown` | `1.5` (seconds) | Delay between accepted gesture actions |
| `num_hands` | `1` | Number of hands tracked at once |

---

## ⚠️ Tips for Best Results

- Ensure good, even lighting on your hand
- Keep your hand fully visible within the camera frame
- Avoid cluttered or busy backgrounds
- Stay at a moderate distance from the camera — not too close, not too far

---

## 🔮 Roadmap / Future Improvements

- [ ] Swipe-based gesture recognition
- [ ] Gesture-based laser pointer
- [ ] Volume control gestures
- [ ] Pinch-to-zoom gestures
- [ ] Custom, trainable gesture sets
- [ ] Multi-hand support

---

## 🎓 Why This Project Is Useful

Great as a learning project or live demo for:

- Computer Vision fundamentals
- Human-Computer Interaction (HCI)
- Real-time webcam/video processing
- Automating desktop actions with Python

Also a fun showcase for AI workshops, hackathons, and classroom demos.

---

## 📜 Requirements

```txt
mediapipe==0.10.35
opencv-python>=4.8.0
pyautogui>=0.9.54
```

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

## 🙌 Acknowledgements

- [Google MediaPipe](https://ai.google.dev/edge/mediapipe/solutions/guide) for the Hand Landmarker model
- [OpenCV](https://opencv.org/) community
- [PyAutoGUI](https://pyautogui.readthedocs.io/) for cross-platform input automation

---

## 👤 Author

**Shivam Kotwalia**

- 📧 Email: your-email@example.com
- 🔗 LinkedIn: [linkedin.com/in/your-profile](https://linkedin.com/in/your-profile)
- 🐙 GitHub: [github.com/shivam-kotwalia](https://github.com/shivam-kotwalia)

---

## ⭐ Support

If you found this project useful:

- ⭐ Star this repository
- 🍴 Fork it
- 📢 Share it with others

---

<p align="center">Made with ❤️ using Python, OpenCV, MediaPipe & PyAutoGUI</p>
