# Virtual Assistant From Scratch

[![Python](https://img.shields.io/badge/Python-3.12-blue?style=for-the-badge&logo=python&logoColor=white)]()
[![GitHub](https://img.shields.io/badge/GitHub-000000?style=for-the-badge&logo=github&logoColor=white)]()

A simple **voice-controlled virtual assistant** built from scratch in Python.  
It can recognize speech from audio files or a microphone and execute commands like opening YouTube, Google, Firefox, or WhatsApp.

---

## 🚀 Features

- Convert text to speech using **Google Text-to-Speech (`gTTS`)**  
- Recognize audio commands with **`speech_recognition`**  
- Automate keyboard input and open applications using **`pyautogui`**  
- Open websites using **`webbrowser`**  
- Compatible with commands like:
  - `"YouTube"` → Opens YouTube in your browser  
  - `"Google"` → Opens Google  
  - `"Firefox"` → Opens Firefox  
  - `"WhatsApp"` → Opens WhatsApp Web  

---

## 💻 Installation

## 1. Clone the repository:

```bash
git clone https://github.com/YourUsername/virtual_assistant_from_scratch.git
cd virtual_assistant_from_scratch
```
## 2. Install the required Python packages:
```
pip install gTTS SpeechRecognition pydub pyautogui
Note: For microphone input, PyAudio is required.

Windows:
pip install pipwin
pipwin install pyaudio

Linux / Mac:
sudo apt-get install portaudio19-dev
pip install pyaudio
```
## 3. Install ffmpeg for audio conversion (mp4 → wav):

Windows: download from FFmpeg

Linux (Ubuntu/Debian):
```
sudo apt-get install ffmpeg
```
## 🎯 Usage
## 1. Using pre-recorded audio files
```
from gtts import gTTS
from pydub import AudioSegment
import speech_recognition as sr

# Generate speech
tts = gTTS(text="open YouTube", lang='en')
tts.save("youtube.mp4")

# Convert mp4 to wav
sound = AudioSegment.from_file("youtube.mp4", format="mp4")
sound.export("youtube.wav", format="wav")

# Recognize speech
r = sr.Recognizer()
with sr.AudioFile("youtube.wav") as source:
    r.adjust_for_ambient_noise(source)
    audio = r.record(source)

text = r.recognize_google(audio, language="en-US")
print("Detected command:", text)
```
## 2. Using real-time microphone input (PC only)
```
import speech_recognition as sr
import webbrowser

r = sr.Recognizer()

with sr.Microphone() as source:
    print("Speak something...")
    r.adjust_for_ambient_noise(source)
    audio = r.listen(source)

text = r.recognize_google(audio, language="en-US")
print("You said:", text)

if "youtube" in text.lower():
    webbrowser.open("https://www.youtube.com")
elif "google" in text.lower():
    webbrowser.open("https://www.google.com")
elif "firefox" in text.lower():
    webbrowser.open("https://www.mozilla.org/firefox/")
elif "whatsapp" in text.lower():
    webbrowser.open("https://web.whatsapp.com")
else:
    print("Command not recognized.")
```
### ⚠ Note: Microphone input requires a PC with a working microphone. Cloud environments like Colab cannot use PyAudio.
✨ Contributing

Feel free to submit issues or pull requests to improve the assistant.
Suggestions for new commands, features, or optimizations are welcome!
