# Text and Object Detenction with Subsequent Explanation

This project is designed to recognize and interpret various elements within an image, such as faces, numbers, objects, and text, and provides an interactive Q&A chatbot that leverages context from images. Below is an overview of each module and the technologies applied.

## Project Modules
### Face Detection
This module detects human faces in an image and identifies the primary facial components, such as eyes, nose, and mouth. We use the Haar Cascade Classifier for face detection, an effective method for identifying objects in real-time. Although other XML files for different detectors are available, this project specifically uses the face detector only.

Technology: **OpenCV’s Haar Cascade Classifier**
Purpose: Basic facial recognition and feature detection for interactive systems.

### Number Recognition
The Number Recognition module identifies numbers within an image, if present. A Convolutional Neural Network (CNN) is used for both training and recognizing digits in images. This model is optimized to detect and classify numbers, especially beneficial for image-based data analysis.

Technology: **Convolutional Neural Network (CNN) implemented in TensorFlow**
Purpose: Enables automated number detection for images containing digit-based data.

### Object Recognition
This module is trained to recognize objects from a specific set of 10 classes: ['airplane', 'automobile', 'bird', 'cat', 'deer', 'dog', 'frog', 'horse', 'ship', 'truck']. Given an image, the module identifies if it contains objects from these classes. A CNN is used to train the model on these categories.

Technology: **CNN implemented with TensorFlow**
Purpose: Broadens the recognition capabilities to include general objects, useful for multi-object detection tasks.

### Text Extraction
The Text Extraction module uses Optical Character Recognition (OCR) to extract text from an image. This feature allows the system to interpret written content, expanding the range of recognized data from the image.

Technology: **Keras OCR**
Purpose: Extracts and interprets textual data, enabling textual content analysis.

### Generative Q&A Chatbot
The Q&A Generative Chatbot combines textual and visual context to answer questions related to images. The chatbot initially learns phrases associated with images through an LSTM model, and then learns question-answer patterns with additional context through a CRNN (ResNet) model. This structure allows the chatbot to respond accurately by considering both textual and visual elements.

Technology: **LSTM for phrase learning, CRNN (ResNet) for context-based Q&A**
Purpose: Provides a conversational interface that considers visual and textual data, enhancing interaction by adapting responses based on image context.

**NOTE: The Q&A Generative Chatbot in this project is primarily demonstrated for educational and illustrative purposes**. It has been trained with limited resources, so while the construction, implementation, and usage of the chatbot are showcased here, its responses may not reflect the high accuracy of a fully-trained model. This module is intended to serve as a learning tool for understanding how image-based question-answering models can be developed and integrated.
