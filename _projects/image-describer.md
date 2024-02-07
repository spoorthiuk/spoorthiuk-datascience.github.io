---
layout: project
title: Image Describer using CNN and LSTM
image: 
  path: /assets/img/blog/image-describer/main.png
  width: 400
  height: 300
description: >
  The goal for the project is to build a convolutional neural network (CNN) that would extract features from an image, generate a caption describing the image and convert the generated text into audio using GTTS.
tags: [Computer Vision, Python, Deep Learning, Neural Networks, CNN]
sitemap: true
hide_last_modified: true
---

[![](https://img.shields.io/badge/Jupyter-Open_Notebook-blue?logo=Jupyter)](https://github.com/spoorthiuk/Image-Describer/blob/main/image-describer.ipynb)
[![](https://img.shields.io/badge/GitHub-View_in_GitHub-blue?logo=GitHub)](https://github.com/spoorthiuk/Image-Describer/tree/main)

* toc
{:toc}

## Project Overview and Results
### Context 
This project combines the power of Convolutional Neural Networks (CNNs) and Long Short-Term Memory (LSTM) networks using Python to create an image description model. CNNs extract image features, while LSTMs generate descriptive captions. The project uses the Flickr8k dataset, and key steps include data cleaning, feature extraction, tokenizing vocabulary, and creating a data generator. The model architecture involves a feature extractor, sequence processor, and decoder. The provided Python script and GUI allow users to upload images, generate descriptions, and convert them into audio using Google’s Text To Speech API, making images accessible through sound.

### Convolution Neural Network

**Convolution Neural Networks (Convents or CNNs)** are those neural networks that are able to take an image as the input and learn its various features by applying filters. It is different from a typical Machine Learning model as it does not require any preprocessing and uses principles from linear algebra, specifically matrix multiplication to identify patterns within an image.

They consist of three main layers:

* Convolution layer
* Pooling layer
* Fully-connected layer

As the input image progresses through the different layers, the complexity of the CNN increases and a greater portion of the image is identified.

#### Convolution Layer

The convolution layer requires the following three things:

* Input data
* Filter
* Feature Map
<br>
We will be feeding colored images to generate captions and a colored image is made up of a matrix of pixels in 3D. Therefore, an input image will have a length, breadth and height. A feature detector, also known as a kernel or a filter, is moved across the respective fields of the image checking if the feature is present and this process is known as convolution.

The feature detector is a 2-D array of weights which represents part of the image. When we say that we are applying the filter to a part of the image, it means that a dot product is calculated between the input pixels and the filter. The filter then shifts by a stride and the process is repeated until the kernel has been swept across the entire image. The final dot product output is known as feature map.

After each convolution operation, the CNN applies a **Rectified Linear Unit** transformation to the feature map thereby introducing nonlinearity to the model.

#### Pooling Layer

The pooling layers perform downsampling or dimensionality reduction. In this layer the kernel sweeps across the entire input and applies an aggregation function to the values within the receptive field.

Pooling is mainly of two types:

* **Max pooling**: The pixel with the maximum value is sent to the output array.
* **Average pooling**: The average value of the pixels within the kernel field in sent to the output
This layer reduces complexity, improves efficiency and reduces the risk of overfitting.
#### Fully-Connected Layer

This layer performs classification based on the features extracted through the previous layers by usually applying the softmax activation function to classify inputs by producing a probability from 0 to 1.

### Long Short-Term Memory
Long Short-Term Memory (LSTM) Networks are sequential and Recurrent Neural Networks(RNNs) that allow information to persist. RNNs remember the previous information fed to them but one of their shortcomings is that they cannot remember long-term dependencies due to vanishing gradient. This shortcoming is avoided due to the long-term dependency of LSTMs

#### LSTM Architecture

The LSTM architecture can be divided into three gates:

* **Forget Gate**: This gate decides if the information coming from the previous timestamp is relevant. It is given by the following equation.
![](/assets/img/blog/image-describer/f1.png)
<br>
A step function is applied to the result to limit the values to 0 and 1. The transformed is then multiplied with the cell state and the following decisions are made.
![](/assets/img/blog/image-describer/f2.png)
* **Input Gate**: This gate decides if we want the current incoming information to be retained by the model for future computation.<br>
![](/assets/img/blog/image-describer/f3.png)
* **New Information**: The new information that needs to be passed to the cell state is a function of the hidden state at the previous timestamp and the input at the current timestamp t. It is given by the following equation:
![](/assets/img/blog/image-describer/f4.png)<br>
The cell updation will happen with the following equation:
![](/assets/img/blog/image-describer/f5.png)
* **Output gate**: This gate completes the information based on the cell state. The equation of the output gate is given by:<br>
![](/assets/img/blog/image-describer/f6.png)<br>
The current hidden state is computed using the following equation:<br>
![](/assets/img/blog/image-describer/f7.png)<br>
The output is given by the following equation:<br>
![](/assets/img/blog/image-describer/f8.png)<br>
![](/assets/img/blog/image-describer/f9.png)
### Image Describer Model
In our model, we are using:

* CNNs to extract features from the images.
* LSTM will use the information from the CNN to generate a description.
#### Dataset

* Flicker8k_Dataset — Dataset folder with 8091 images.
* Flickr_8k_Text — Dataset folder containing text files and captions of images.
#### Project files and folders

* Models — This folder stores the trained models.
* description.txt — Contains the image captions after pre-processing.
* features.p — Pickel object containing the features extracted from the pre-trained Xception CNN model.
* tokenizer.p — Contains tokes mapped with index values.
* main.py — Python file for generating descriptions for any given image
* image-describer.ipynb — Jupyter notebook used in creating the model and training it with the training images.
#### image-describer.ipynb

* Data Cleaning:
Flickr8k.token.txt file contains the image file names with their respective captions.

Each image contains 5 different captions. We will define a function, img_captions, which will generate a dictionary with the file names as the key and the captions in a list as the values.

In order to clean the captions, we will define another function called data_cleaning to remove punctuation, and words containing numbers and to turn all alphabets into lowercase.

The get_vocabulary function will create a set containing all the words used in the captions. The store_description function will map each caption to the text file name and store it in a text file.
```python
class FileHandling:
    def __init__(self):
        pass
    def load_file(self, file):
        file = open(file,"r")
        text = file.read()
        file.close()
        return text
    def img_captions(self, file_contents):
        img_captions = dict()
        for file_name_raw in file_contents.split('\n'):
            file_name = file_name_raw.split('\t')[0].split('#')[0]
            if file_name not in img_captions.keys():
                img_captions[file_name] = []
            img_captions[file_name].append(file_name_raw.split('\t')[-1])
        return img_captions
    def data_cleaning(self, captions):
        #create a dictionary of ascii values of all punctuation mapped to none values
        img_edited_captions = {}
        punctuation_none_map = str.maketrans('','',string.punctuation)
        for img_name,all_captions in captions.items():
            if img_name not in img_edited_captions.values():
                img_edited_captions[img_name] = []
            for caption in all_captions:
                #remove punctuation
                caption = caption.translate(punctuation_none_map)
                all_words = caption.split()
                #convert to lower case
                all_words = [word.lower() for word in all_words]
                #remove hanging 's and a'
                all_words = [word for word in all_words if len(word) > 1]
                #remove words containing numbers
                all_words = [word for word in all_words if word.isalpha()]
                caption_edited = ' '.join(all_words)
                img_edited_captions[img_name].append(caption_edited)
        return img_edited_captions
    def get_vocabulary(self, captions):
        vocab = set()
        for img in captions.keys():
            for caption in captions[img]:
                vocab.update(caption.split())
        return vocab
            
    def store_description(self, all_captions, file_name):
        export_text = []
        for img,captions in all_captions.items():
            for caption in captions:
                export_text.append("{}\t{}".format(img,caption))
        file = open(file_name,"w")
        file.write('\n'.join(export_text))
        file.close()
```

* Extract Features:
We will define a function extract_features that will extract the features from all the images stored in a given directory. We use a pre-trained model called Xception to extract the features from the images. We will resize the given image to [299x299] and normalize the pixel values by first dividing them by 127.5 and subtracting the resulting value with 1.0 to get a value between -1 and 1. After feature extraction, we will store these features in a pickle file called features.p.
```python
#extract_feature: Given a directory, this function extracts all the features using Xception model
def extract_features(directory):
    model = Xception(include_top = False, pooling = 'avg')
    features = {}
    for img in tqdm(os.listdir(directory)):
        file_name = directory+'/'+img
        image = Image.open(file_name)
        image = image.resize((299,299))
        image = np.expand_dims(image,axis=0)
        image = image / 127.5
        image = image - 1.0
        feature = model.predict(image)
        features[img] = feature
    return features
    ```
* Preparing data for training:
We will define a function called clean_description that will create a dictionary mapping the image file names to their captions after appending <start> and <end> to the captions. load_features will return a dictionary with the mapping of the image names to their respective features extracted from the Xception model.

```python
class TrainModel:
    def __init__(self):
        pass
    
    def load_photos(self,file_name):
        File = FileHandling()
        file = File.load_file(file_name)
        img_list = file.split('\n')[:-1]
        return img_list
    
    def clean_description(self,file_name,photos):
        File = FileHandling()
        file = File.load_file(file_name)
        descriptions = file.split('\n')
        clean_desc = {}
        for img_desc in descriptions:
            img = img_desc.split('\t')[0]
            if len(img_desc.split('\t')[-1].split()) < 1:
                continue
            if img in photos:
                if img not in clean_desc.keys():
                    clean_desc[img] = []
                clean_desc[img].append("<start> {} <end>".format(img_desc.split('\t')[-1]))
        return clean_desc
        
    def load_features(self,photos):
        all_features = load(open("features.p","rb"))
        features = {}
        for img in photos:
            features[img] = all_features[img]
        return features
```
* Tokenizing vocabulary:
We will define a function called create_tokens that will create word embeddings for all the words used in the captions so that the computer can understand words using Keras Tokenizer() and store these tokens in a pickle file called tokenizer.p
```python
def dict_list(descriptions):
    all_desc = []
    for img in descriptions.keys():
        [all_desc.append(desc) for desc in descriptions[img]]
    return all_desc
def create_tokens(descriptions):
    desc_list = dict_list(descriptions)
    tokenizer = Tokenizer()
    tokenizer.fit_on_texts(desc_list)
    return tokenizer
```

* Data Generator:
We need to now define a function called the data_generator which will create the input and output sequence for our model.

This generator will yield the input and output sequences for a particular image and caption pair as follows

![](/assets/img/blog/image-describer/f10.png)

```python 
def create_sequence(tokenizer, max_length, desc_list, feature):
    X1=list()
    X2=list()
    y=list()
    for desc in desc_list:
        #sequnce encodng
        seq = tokenizer.texts_to_sequences([desc])[0]
        for i in range(0,len(seq)):
            in_seq, out_seq = seq[:i], seq[i]
            #pad input sequence
            in_seq = pad_sequences([in_seq], maxlen = max_length)[0]
            #encode output sequence
            out_seq = to_categorical([out_seq],num_classes=vocab_size)[0]
            X1.append(feature)
            X2.append(in_seq)
            y.append(out_seq)
    return np.array(X1), np.array(X2), np.array(y)

def data_generator(descriptions, features, tokenizer, max_length):
    while 1:
        for key, desc_list in descriptions.items():
            feature = features[key][0]
            input_image, input_seq, output_word = create_sequence(tokenizer, max_length, desc_list, feature)
            yield [[input_image, input_seq], output_word]
            
[a,b],c = next(data_generator(train_descriptions, features,tokens, vocab_size))
print(a.shape,b.shape,c.shape)
```
* CNN and RNN model:
The entire model can be divided into three parts:

1) Feature Extractor:
Here we are using the features extracted for each image earlier and converting a vector of size 2048 to 256 nodes using a dense layer. We set the dropout rate to 0.5 in order to prevent overfitting of the model as half (50%) of the neurons in the specified layer will be randomly deactivated (set to zero) at each forward and backward pass.

2) Sequence Processor:

Here we have an embedding layer where it learns a mapping from discrete categorical values (e.g., words) to continuous vector representations followed by a dropout layer to prevent overfitting and an LSTM model.

3) Decoder:

Here we’re gonna merge the outputs of the above two layers by adding them and a dense to arrive at the final prediction

Once we are done designing our model we train it and store the models in the models folder.

```python
def define_model(vocab_size, max_length):
    #Features changed from CNN model 
    inputs1 = Input(shape=(2048,))
    fel = Dropout(0.5)(inputs1)
    fe2 = Dense(256, activation = 'relu')(fel)
    
    # LSTM sequence model
    inputs2 = Input(shape=(max_length,))
    se1 = Embedding(vocab_size,256,mask_zero=True)(inputs2)
    se2 = Dropout(0.5)(se1)
    se3 = LSTM(256)(se2)
    
    #Merging models
    decoder1 = add([fe2, se3])
    decoder2 = Dense(256, activation='relu')(decoder1)
    outputs = Dense(vocab_size, activation='softmax')(decoder2)
    
    model = Model(inputs = [inputs1,inputs2], outputs = outputs)
    model.compile(loss = 'categorical_crossentropy', optimizer = 'adam')
    
    #summarize
    print(model.summary())
    plot_model(model, to_file='model.png', show_shapes = True)
    return model
```
#### main.py

This Python script contains the code to test our models. We have designed a GUI using Tkinter that will enable us to upload images, predict the image description and convert it into audio using Google’s Text To Speech API.

### Final Result
The total training loss : 2.65
![](/assets/img/blog/image-describer/f11.png)