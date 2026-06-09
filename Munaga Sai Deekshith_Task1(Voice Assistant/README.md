# 🤖 BASIC VERSION OF AI VOICE ASSISTANT

**Oasis Infobyte Internship -- Python Programming**

Created by: **M. Sai Deekshith**

---

## 📌 PROJECT DESCRIPTION

This is a **beginner-friendly Python project** that creates a simple **AI Voice Assistant**. The assistant listens to your voice commands, understands them, and responds with helpful information or performs simple tasks.

### ✨ KEY FEATURES

1. **Speech Recognition** 🎤
   - Listens to your voice through microphone
   - Converts voice to text using Google Speech Recognition API
   - Handles background noise automatically
   - **DEMO MODE**: Automatically switches to text input if no microphone!

2. **Text-to-Speech** 🔊
   - Responds to you with voice using text-to-speech technology
   - Also prints responses on screen for reference

3. **Smart Commands** 🧠
   - **"Hello"** - Greets you back with your name
   - **"Time"** - Tells you the current time
   - **"Date"** - Tells you today's date
   - **"Search [something]"** - Opens Google and searches for information
   - **"Exit"** or **"Bye"** - Stops the assistant

4. **Error Handling** ⚠️
   - Handles microphone errors gracefully
   - Deals with network issues
   - Catches unexpected errors
   - Shows user-friendly error messages
   - **Works in containers** without audio hardware!

5. **DEMO MODE** 🧪
   - Automatically detects if microphone is unavailable
   - Switches to text input mode
   - All features work perfectly with keyboard input
   - Perfect for testing in containers, SSH, or headless systems

---

## 🚀 HOW TO SET UP AND RUN

### Step 1: Prerequisites
- Python 3.7 or higher installed
- Working microphone on your computer
- Internet connection (for Google search)
- VS Code or any Python IDE

### Step 2: Install Required Libraries

Open your terminal and run:

```bash
pip install -r requirements.txt
```

**This will install:**
- `SpeechRecognition` - For voice-to-text
- `pyttsx3` - For text-to-voice
- `PyAudio` - For microphone support

### Step 3: Run the Program

```bash
python ai_voice_assistant.py
```

### Step 4: Use the Assistant

1. Enter your name when prompted
2. Wait for the assistant to greet you
3. Speak clearly into your microphone
4. The assistant will process your command
5. Say **"exit"** or **"bye"** to stop

---

## 📚 CODE STRUCTURE (For Beginners)

### What Each Function Does:

| Function | Purpose |
|----------|---------|
| `speak(text)` | Makes the assistant talk (text-to-speech) |
| `take_command()` | Listens to user and converts voice to text |
| `tell_time()` | Gets and announces the current time |
| `tell_date()` | Gets and announces today's date |
| `search_google(query)` | Opens Google and searches for information |
| `greet_user(name)` | Welcomes user and explains features |
| `process_command(command, name)` | Understands and responds to commands |

### CODE FLOW:

```
START PROGRAM
    ↓
Get User Name
    ↓
Greet User (with demo mode info if needed)
    ↓
LOOP (Keep repeating):
    1. Try to listen for voice command
    2. If no microphone found:
       → Switch to TEXT INPUT MODE
       → Show info message
    3. Get user input (voice or text)
    4. Convert to text (recognize_google or user typed it)
    5. Recognize what command it is
    6. Execute the command
    7. Respond with voice and text
    8. If "exit", stop loop
    ↓
END PROGRAM
```

---

## 🔊 UNDERSTANDING ALSA WARNINGS (Important!)

### What are These Messages?

When you run the program, you might see messages like:
```
ALSA lib conf.c:5204:(_snd_config_evaluate) function snd_func_refer returned error
ALSA lib pcm.c:2721:(snd_pcm_open_noupdate) Unknown PCM sysdefault
Cannot connect to server socket err = No such file or directory
❌ Unexpected error: No Default Input Device Available
```

### Is This an Error? NO! ✅

**These are just WARNINGS** from the audio system trying to initialize. They happen because:

| Situation | What Happens | What You See |
|-----------|-------------|-------------|
| **Using laptop with microphone** | Audio initializes successfully | Program works normally with voice |
| **In a container (Docker, dev container)** | No audio hardware found | ALSA warnings + switches to TEXT MODE |
| **SSH session (headless)** | No audio available | ALSA warnings + switches to TEXT MODE |
| **Virtual machine** | No audio device | ALSA warnings + switches to TEXT MODE |

### Why Your Program Shows These Warnings

The code tries to initialize audio first. Since this is likely a **container environment**, the audio system can't find devices, so it shows warnings. **But the program continues anyway!** ✅

### How the Program Handles This

1. **Tries to use microphone** → Fails with ALSA warnings
2. **Detects "No Default Input Device"** → Catches the error
3. **Automatically switches to TEXT INPUT MODE** → Prompts for keyboard input instead
4. **Program works perfectly** with text commands!

### ALSA Warning Messages Explained

| Message | Meaning | Is It Bad? |
|---------|---------|-----------|
| `ALSA lib conf.c:...` | Audio config file issue | No, just warnings |
| `Unknown PCM sysdefault` | Can't find default audio device | No, expected in containers |
| `Cannot connect to server socket` | Jack audio server not running | No, not needed for our app |
| `No Default Input Device Available` | **Triggers TEXT MODE** | No, handled gracefully! |

### What You Can Do

**Option 1: Ignore The Warnings (Recommended)**
- They're just console noise
- Program works perfectly
- Everything functions normally

**Option 2: Suppress The Warnings** (Advanced)
The code automatically suppresses ALSA warnings with environment variables:
```python
os.environ['ALSA_CARD'] = 'default'
os.environ['PULSE_PROPAGATE_DOCNAME'] = '0'
```

**Option 3: Use With Real Microphone**
- Connect a USB microphone to your system
- Warnings will go away
- Voice recognition will work

---

### 1. **Libraries/Modules**
- External code that someone else wrote
- We import them using `import` keyword
- Example: `import speech_recognition as sr`

### 2. **Functions**
- Blocks of code that do specific tasks
- We define them with `def` keyword
- Example: `def speak(text):`

### 3. **Error Handling (Try-Except)**
- Code that handles problems gracefully
- `try:` - Code we want to run
- `except:` - What to do if error occurs
- Prevents the program from crashing

### 4. **While Loop**
- Keeps repeating code until condition is false
- Used to keep assistant listening
- `while True:` - Loop forever until we break

### 5. **String Methods**
- `.lower()` - Convert to lowercase
- `.strip()` - Remove spaces
- `.format()` - Put values into text

---

## ❓ TROUBLESHOOTING

### **Issue: ALSA Warnings and Audio Errors in Console**
This is **VERY NORMAL** in container/virtual environments! ALSA (Advanced Linux Sound Architecture) warnings like:
```
ALSA lib conf.c:5204: function snd_func_refer returned error
Unknown PCM cards.pcm.surround
No Default Input Device Available
```

**Why this happens:**
- Running in a container without physical audio hardware
- System is looking for audio devices that don't exist
- These are just warnings, NOT errors

**What to do:**
- ✅ **These warnings don't hurt the program** - it still works!
- The program will automatically switch to **TEXT INPUT MODE**
- You can type commands instead of speaking
- All features work normally in text mode

### **Issue: Program Running in TEXT INPUT MODE**
If you see: `📝 Running in TEXT INPUT MODE (no microphone detected)`

**This is expected!**
- Just type your commands instead of speaking
- Example: type `hello` and press Enter
- Type `time` for current time
- Type `date` for today's date
- Type `exit` to quit

### **Issue: Microphone not working**
- Check if microphone is connected
- Test microphone on other applications
- Run: `python -m pip install --upgrade pyaudio`
- Some systems need: `pip install pipwin && pipwin install pyaudio`

### **Issue: "ModuleNotFoundError"**
- Make sure all libraries are installed
- Run: `pip install -r requirements.txt` again

### **Issue: Google speech recognition not working**
- Check internet connection
- Check microphone permissions
- Some networks might block Google API
- Use TEXT INPUT MODE as fallback

### **Issue: Text-to-speech not speaking**
- Check your system volume
- Check speaker connection
- This won't prevent the assistant from working (text will still display)

---

## 📝 EXAMPLE USAGE

```
🤖 WELCOME TO BASIC AI VOICE ASSISTANT 🤖
================================================
📝 Please enter your name: John
================================================

🤖 Assistant: Hello John! Welcome to the Basic AI Voice Assistant.
🤖 Assistant: This is a beginner-friendly voice assistant created for learning Python.
🤖 Assistant: I can help you with a few basic tasks.
🤖 Assistant: Say 'Hello' to greet me, ask for the 'time' or 'date', search Google, or say 'exit' to stop.

✅ Assistant is ready! Start speaking your commands.

🎤 Listening... (Please speak now)
🔄 Recognizing what you said...
✅ You said: hello

🤖 Assistant: Hello John! How can I help you today?

🎤 Listening... (Please speak now)
```

---

## 🔧 ADVANCED TOPICS (Optional)

To extend this assistant, you could add:

1. **More Commands** - Add support for weather, news, jokes, etc.
2. **Wake Word Detection** - Say a specific word to activate
3. **Machine Learning** - Make it learn from conversations
4. **Database** - Remember user preferences
5. **GUI Interface** - Create a visual interface with buttons

---

## 📖 RESOURCES FOR LEARNING

### Libraries Documentation:
- [SpeechRecognition Documentation](https://github.com/Uberi/speech_recognition)
- [pyttsx3 Documentation](https://pyttsx3.readthedocs.io/)
- [Python datetime Module](https://docs.python.org/3/library/datetime.html)

### Learning Resources:
- [Python Official Tutorial](https://docs.python.org/3/tutorial/)
- [Real Python Tutorials](https://realpython.com/)

---

## ✅ FEATURES IMPLEMENTED

- ✅ Speech Recognition (voice to text)
- ✅ Text-to-Speech (text to voice)
- ✅ Greeting with user's name
- ✅ Time and Date functions
- ✅ Google Search functionality
- ✅ Error handling (Timeout, Network, Audio)
- ✅ User-friendly console output
- ✅ Beginner-friendly comments
- ✅ Graceful exit handling
- ✅ Keyboard interrupt handling (Ctrl+C)

---

## 📄 LICENSE

This project is part of the Oasis Infobyte Internship Program.

---

## 🙏 CREDITS

- **Created by:** M. Sai Deekshith
- **For:** Oasis Infobyte Internship
- **Internship Program:** Python Programming
- **Special thanks to:** All open-source library contributors

---

## 💡 TIPS FOR BEGINNERS

1. **Read the comments** - The code has detailed comments explaining each line
2. **Understand one function at a time** - Don't try to understand everything at once
3. **Experiment** - Try modifying the code and see what happens
4. **Test different commands** - Try various ways of saying commands
5. **Debug slowly** - Read error messages carefully, they help you understand problems

---

## 🎯 NEXT STEPS

1. Run the program and test all features
2. Read through the code and comments carefully
3. Try modifying commands
4. Add new features (weather, jokes, notes, etc.)
5. Share your version with others!

**Happy Learning! 🚀**
