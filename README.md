# EcoSnap


https://user-images.githubusercontent.com/7581348/208559445-a449cef6-0ae1-4c08-b9a5-c591062c3a3e.mp4


Recycle your plastic better with Artificial Intelligence ♻️

EcoSnap tells you how and where to recycle your items from a simple picture, with advice tailored to your location. 


> 

## Table of contents

- [Features](#features)
- [Installation](#installation)
- [The AI model](#the-ai-model)
	- [Dataset](#data)
	- [Training your own model](#training)
	- [Prediction](#prediction)
    - [The feedback loop](#feedback)
- [Credit](#credit)
- [Libraries used](#libraries-used)

## Features

📸 Snap or upload a picture of a plastic code<br>
📱 Install the PWA on your phone for easy access<br>
🔍 Search for specific item to know how to dispose of it<br>
♻️ Learn how to recycle effectively using AI<br>
🥤 Keep track of how many plastic items you've recycled<br>
🌍 Change your location for specific advice<br>
✨...and much more to come - all for free & no sign in needed!



## The AI Model

### Data

The model was trained on image examples of the 7 different resin codes, the data for this can be found in `ml/seven_plastics`. It is a combination of the following [Kaggle Dataset](https://www.kaggle.com/datasets/piaoya/plastic-recycling-codes) and images collected by the authors and contributors.

### Training

The final model was trained using [TensorFlow's EfficientNet](https://www.tensorflow.org/api_docs/python/tf/keras/applications/efficientnet_v2/EfficientNetV2B0) implementation, the model weights were frozen for transfer learning, so the model could learn the resin codes faster! The model was trained in `Python` on a GPU-powered machine, for faster training! You can find the training script in `ml/train.py` and try it for yourself, there you will see that different meta architectures and parameters were experimented with before arriving at the final model.

### Prediction

To predict the plastic resin code, the model had to be integrated with the front end app for real-time results, to do this we had to convert the model in a way that was compatible with [TensorFlow.js](https://www.tensorflow.org/js).

The app passes the image Tensor onto the model that then gives a probability for each of the plastic resin codes, the one with the highest probability gets shown to the user, *along with bespoke advice*!

### Feedback

Training a specific model is hard, the model always gets things wrong. So if it does, we give the user an opportunity to tell us what the right code was! This benefits in several ways:

1. The user gets the information they need on how to recycle their item
2. We can see how the model is performing in production
3. We get new data (if the user lets us) to train the model with and improve it for everyone

While we implemented the front end for the feedback loop, we ended up not connecting it to the backend as it added complexity and cost, and we wanted the app to be very lightweight and running entirely on the client. We'd also have to communicate clearly to the user how exactly their images would be used, and set up either an opt-in or opt-out system, which felt a bit cumbersome.

## Credit
- [Kaggle Dataset](https://www.kaggle.com/datasets/piaoya/plastic-recycling-codes) - for the plastic codes
- [Collletttivo](http://collletttivo.it/) - for the Mattone font
- [Stubborn](https://stubborn.fun/) - for some of the illustrations
- [Unsplash](https://unsplash.com/) - for the images

## Libraries used
- [Tensorflow](https://www.tensorflow.org/) - for training the model and doing the prediction
- [React Camera Pro](https://github.com/purple-technology/react-camera-pro) - for the camera



