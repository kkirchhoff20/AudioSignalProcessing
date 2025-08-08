The following directories chronicle a story: I wanted to know if I could train a ML model to detect what I was typing based on the sounds of my keyboard alone.
The early work focused on data exploration and feature engineering. I found that the Fast Fourier Transform (FFT) and Wavelet Transform could be used on my raw audio data to create acoustic fingerprints of each individual key and potentially serve as training features 
for my model. I thought perhaps it would make more sense to set the bar lower initially - so instead of attempting to train a model to discern the rapid, far less perceptible chatter of different keys, I would first try to train one to classify the sound of a keypress 
vs me tapping on my desk. Despite my enthusiasm, my efforts were not successful. So I lowered the bar further. I thought, if my model can't parse the subtleties of these real-world recorded sounds, then I'll try with controlled, synthetic sounds. 
So I next created a dataset composed of audio waves defined at two different frequencies (with a measured amount of noise added to provide variety). Still no luck. The fact my models couldn't even discern between sounds engineered distinct at the mathematical level 
indicated there was likely a problem upstream in my code. As it turns out, there was. The mistake lay in how I was slicing arrays - subtle enough so as to not throw an error, but nevertheless pernicious enough to throw off my models entirely. After remedying this, I was
able to create models that could easily distinguish the two different synthetic signals. With renewed confidence I downloaded a host of noises from Kaggle, and practiced building models to classify those, all the while refining my pipeline and tools. I felt I was now
ready to take on the more nuanced challenge of typing sounds. I quickly realized that to create a dataset robust enough to train a model on the full set of keys, I would need a more rapid and streamlined way of generating and cataloging data. So I put my programming 
chops to the test and created a Java application from scratch to do that (more info below). After generating several hours of typing data it was time to process, clean and annotate it. With the power of Python and its robust libraries I was eventually able to set up
a system that, while not achieving full automation, greatly streamlined the acquisition, cleaning, processing, modeling, and testing. Through cycles of troubleshooting, error detection, and model improvement, the project moved from foundational exploration to the 
successful classification of distinct acoustic events—showcasing an end-to-end workflow from data capture to predictive modeling.

Repository Structure

1. Data Exploration and Proof of Concept

Early notebooks focus on understanding the raw audio data, visualizing spectrograms, and applying FFT-based feature engineering techniques. This phase helped characterize the acoustic signatures of different sound events and validate the feasibility of machine learning classification.

Notebooks:

Exploring Audio Data.ipynb

Exploring Spectrograms and Feature Engineering.ipynb

2. Building Tools and Preprocessing Pipelines

Once foundational insights were gained, the focus shifted to building reusable tools and preprocessing pipelines. 

Notebooks:

Create Synthetic Signals.ipynb

Desk Tap and Key Press.ipynb

Kaggle Sounds.ipynb

Press Tap Classification.ipynb

Wavelet pipeline component.ipynb

3. EFX – Java-Based Data Capture System
Used to generate and automate the storage of raw audio data and keypress transcripts to be processed and ingested for model training. 
EFX is a multi-threaded GUI system that retrieves and displays a random Wikipedia article for the user to type, all the while synchronizing audio and keystroke data capture and storage. Files include:

AudioRecorder.java: Captures and stores raw audio streams

KeyLogger.java: Tracks keyboard input events with timestamps

LogEntry.java: Data model for storing synchronized logs

Main.java & SampleController.java: Application logic and UI controllers

Sample.fxml & application.css: UI layout and styling

4. Key Classification
With labeled datasets in hand, the final phase encompassed cleaning, feature engineering, model training, and evaluation. Key notebooks focus on:

Data cleaning and transformation of typing logs and audio features

Building and testing classification models for keypress detection

Specialized analysis for identifying specific keys like the spacebar

Notable notebooks:

Cleaning Typing Data.ipynb

Key Classification1.ipynb

Key Classification2.ipynb

Model from Typing Data.ipynb

Spacebar Identifier.ipynb



Ended up creating a model that could discern between the sounds of my keyboard's spacebar key vs any other key with over 90% accuracy.
