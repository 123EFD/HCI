# Emotion Learning Game

An interactive web-based game designed to help children learn and recognize emotions through various engaging activities.

## Project Summary

This project is an **Emotion Learning Game** that teaches children to identify and understand six basic emotions: Happy, Sad, Angry, Surprised, Scared, and Excited. The application uses multi-modal learning approaches including visual flashcards, interactive games, audio feedback, and facial recognition technology.

## Features

- 🎴 **Flashcards** - Interactive flip cards showing emotion faces with names
- 🎯 **Matching Game** - Drag-and-drop game matching facial expressions to emotion names
- 🧠 **Expression Quiz** - Multiple choice quiz testing emotion recognition
- 🎤 **Voice Soundboard** - Audio samples representing each emotion
- 📷 **Facial Recognition** - Real-time emotion detection using webcam and Teachable Machine

## Technology Stack

- **HTML5/CSS3** - Responsive UI with gradient designs and animations
- **JavaScript (Vanilla)** - Game logic and interactivity
- **TensorFlow.js** - Machine learning runtime for facial recognition
- **Teachable Machine** - Pre-trained emotion classification model
- **Web Speech API** - Text-to-speech for emotion pronunciation
- **Web Audio API** - Sound effect playback

## Multi-language Support

The application supports three languages:
- English
- Bahasa Melayu
- 中文 (Chinese)

---

## Prompts and Concepts Used

### 1. Emotion Data Structure
The core emotion data is structured as an array of objects containing emotion properties:

```javascript
const emotions = [
    {
        name: "Happy",
        description: "A feeling of joy and contentment...",
        soundDescription: "Laughing and cheerful voice",
        color: "#FFD93D"
    },
    // ... other emotions
];
```

### 2. Multi-language Translation System
Translations are organized in a structured object with language codes as keys:

```javascript
const translations = {
    en: {
        'game-title': 'Emotion Learning Game',
        'Happy': 'Happy',
        // ... more translations
    },
    ms: {
        'game-title': 'Permainan Pembelajaran Emosi',
        'Happy': 'Gembira',
        // ...
    },
    zh: {
        'game-title': '情绪学习游戏',
        'Happy': '快乐',
        // ...
    }
};
```

---

## Important Code Highlights

### 1. Drawing Emotion Faces (SVG)
Function to dynamically draw emotion faces using SVG images:

```javascript
function drawHumanFace(svgElement, emotionName) {
    const emotion = emotions.find(e => e.name === emotionName);
    const color = emotion ? emotion.color : "#FFD93D";
    
    svgElement.innerHTML = '';
    
    // Create face circle background
    const face = document.createElementNS("http://www.w3.org/2000/svg", "circle");
    face.setAttribute("cx", "100");
    face.setAttribute("cy", "100");
    face.setAttribute("r", "90");
    face.setAttribute("fill", color);
    svgElement.appendChild(face);
    
    // Load emotion image overlay
    const img = document.createElementNS("http://www.w3.org/2000/svg", "image");
    img.setAttribute("href", `assets/${emotionName.toLowerCase()}.png`);
    img.setAttribute("width", "180");
    img.setAttribute("height", "180");
    svgElement.appendChild(img);
}
```

### 2. Drag and Drop Implementation
Touch and mouse event handling for the matching game:

```javascript
// Desktop drag events
emojiElement.addEventListener('dragstart', handleDragStart);
emojiElement.addEventListener('dragend', handleDragEnd);

// Mobile touch events
emojiElement.addEventListener('touchstart', handleTouchStart, { passive: false });
emojiElement.addEventListener('touchmove', handleTouchMove, { passive: false });
emojiElement.addEventListener('touchend', handleTouchEnd, { passive: false });
```

### 3. Facial Recognition with Teachable Machine
Loading and using the Teachable Machine model:

```javascript
async function initFacialRecognition() {
    const modelURL = "./emotion_model/model.json";
    const metadataURL = "./emotion_model/metadata.json";
    
    // Load model
    facialModel = await tmImage.load(modelURL, metadataURL);
    facialMaxPredictions = facialModel.getTotalClasses();
    
    // Setup webcam
    facialWebcam = new tmImage.Webcam(300, 300, true);
    await facialWebcam.setup();
    await facialWebcam.play();
    
    // Start prediction loop
    facialLoop();
}

async function facialPredict() {
    const predictions = await facialModel.predict(facialWebcam.canvas);
    // Update UI with predictions
}
```

### 4. Text-to-Speech for Emotion Names
Speaking emotion names in the selected language:

```javascript
function speakEmotionName(emotionName, buttonElement) {
    const emotion = emotions.find(e => e.name === emotionName);
    const textToSpeak = emotion ? emotion.translatedName : emotionName;
    
    const utterance = new SpeechSynthesisUtterance(textToSpeak);
    utterance.lang = languageVoiceConfig[currentLanguage].lang;
    
    speechSynthesis.speak(utterance);
}
```

### 5. Sound Effect Playback
Playing emotion-specific audio files:

```javascript
const soundFiles = {
    "Happy": "soundeffect/happy-noisesmp3-14568.mp3",
    "Sad": "soundeffect/baby-crying-64996.mp3",
    "Angry": "soundeffect/angry-grunt-103204.mp3",
    "Surprised": "soundeffect/wow1-83641.mp3",
    "Scared": "soundeffect/Kid Screaming.mp3",
    "Excited": "soundeffect/children-saying-yay-praise-and-worship-jesus-299607.mp3"
};

function playHumanVoice(emotionName, callback) {
    const audio = new Audio(soundFiles[emotionName]);
    audio.onended = callback;
    audio.play();
}
```

### 6. Quiz Question Generation
Creating randomized quiz questions:

```javascript
function initQuiz() {
    quizQuestions = [];
    let emotionPool = shuffleArray([...emotions]);
    
    for (let i = 0; i < 10; i++) {
        quizQuestions.push({
            emotion: emotionPool[i % emotions.length].name,
            correct: "Yes",
            options: ["Yes", "No"]
        });
    }
    showQuestion();
}
```

---

## File Structure

```
HC1/
├── index.html          # Main application file
├── README.md           # This file
├── vercel.json         # Vercel deployment config
├── assets/             # Emotion face images
│   ├── happy.png
│   ├── sad.png
│   ├── angry.png
│   ├── surprised.png
│   ├── scared.png
│   └── excited.png
├── soundeffect/        # Audio files for emotions
│   └── *.mp3
└── emotion_model/      # Teachable Machine model
    ├── README.md
    ├── model.json
    ├── metadata.json
    └── weights.bin
```

## Deployment

The application is configured for deployment on **Vercel**. The `vercel.json` file includes rewrite rules for single-page application routing.

## Getting Started

1. Clone the repository
2. Open `index.html` in a web browser
3. For facial recognition, add your Teachable Machine model to the `emotion_model/` folder
4. (Optional) Deploy to Vercel for online access

## License

This project is for educational purposes.
