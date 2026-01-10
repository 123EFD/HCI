# Emotion Detection Model

This directory should contain a Teachable Machine image classification model trained to detect the following 6 emotions:

1. **Happy** - Joyful, smiling expression
2. **Sad** - Sorrowful, frowning expression
3. **Angry** - Frustrated, upset expression
4. **Surprised** - Wide-eyed, amazed expression
5. **Scared** - Fearful, worried expression
6. **Excited** - Enthusiastic, energetic expression

## How to Create Your Model

1. Go to [Teachable Machine](https://teachablemachine.withgoogle.com/train/image)
2. Create a new Image Project
3. Create 6 classes, one for each emotion listed above
4. Add training images for each emotion (at least 50-100 samples per class recommended)
   - Use webcam to capture samples of children making different facial expressions
   - Ensure good lighting and various angles
5. Train the model
6. Export the model:
   - Click "Export Model"
   - Choose "Tensorflow.js"
   - Download the model files
7. Place the downloaded files in this directory:
   - `model.json` - Model architecture
   - `metadata.json` - Class labels and metadata
   - `weights.bin` - Model weights (may be multiple files)

## Model Files Required

- `model.json`
- `metadata.json`
- `weights.bin` (or multiple weight shard files)

## Demo Mode

If no model files are present, the facial recognition feature will run in demo mode with simulated predictions for testing purposes.

## Tips for Better Accuracy

- Collect diverse training samples with different lighting conditions
- Include samples from children of different ages
- Ensure faces are clearly visible and well-lit
- Train with a balanced number of samples per emotion
- Test and retrain if accuracy is low
