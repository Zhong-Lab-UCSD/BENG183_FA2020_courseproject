# Chapter 3: Long Short Term Memory
<!--- A deep dive into something most people will not even remember long or short term besides for the exam... 
-->
____

## Section 3.1: What are Recurrent Neural Networks?

### Introduction
Now that we have covered some of the basic machine learning algorithms, let us dive into one of the more complex and widely used
tools - a Long Short Term Memory Neural Network (LSTM). In this chapter, we will cover the following materials:
1) A brief overview of Recurrent Neural Networks (RNN)
2) What is a Long Short Term Memory Neural Network?
3) How do LSTMs work?
4) LSTM Do-It-Yourself Walkthrough!
5) When do I use LSTMs over other tools?
6) Genomic Applications of LSTMs

### What are Recurrent Neural Networks?
To start with, what is a Recurrent Neural Network? A neural network set of algorithms that function in a way that mimics a collection of neurons inside a human brain. There is an input, some calculations in the middle, and some output. The number of inputs, outputs and type of input/output (whether it is an image or music or text) varies per network, and your specific neural network can be customized to analyze whatever you want it to. The difference between a typical neural network and a *recurrent* neural network is that this structure also contains a way to persist some of the outputs from previous iterations into the input of the next iteration. This allows the neural network to essentially "remember" the past and form conclusions about what is to come based on what it has already seen.

### History and Prior Applications of RNNs
Recurrent Neural Networks were developed in 1986 by David Rumelhart, a mathematical psychologist from Stanford University. You can read more about him here [Link to Personal Page](https://en.wikipedia.org/wiki/David_Rumelhart) and even read the original paper where this application is discussed in great detail here: [Link to paper](https://www.nature.com/articles/323533a0). This novel innnovation sparked a great deal of interest in applying this knowledge to many different fields. Within the turn of the century, scientists were starting to apply this to music composition, handwriting recognition, and even protein homology detection. It wasn't until 1997 that two European scientists created the LSTM as an improved and specialized version of the current RNNs. 

If you are interested in reading more, check out these two articles:
* [Article Here: ](https://ai.googleblog.com/2019/03/rnn-based-handwriting-recognition-in.html) This is an article about how Google is using RNNs to develop handwriting recognition software.
* [Scientific Paper Here: ](https://web.stanford.edu/class/archive/cs/cs224n/cs224n.1174/reports/2762076.pdf) This is another interesting research paper detailing how RNN-assisted computer generated music fooled over 70% of human listeners.

### What is the structure of a Recurrent Neural Network?
Do not feel intimidated by the complex math or the weird structures you might see. They are all simply a collection of inputs, outputs, and arrows that indicate the direction that information is flowing. With that in mind, let us look at a simple RNN set-up.

![A traditional RNN Architecture](./images/TraditionalRNNArchitecture.jpg "This is a traditional RNN Architecture")
###### This is a traditional set up, where at each time step, there is exactly one input and one output. 

There are other forms of neural networks where there are different layouts, from one input-> one output to many inputs -> many outputs and everything in between. The structure and setup you choose will depend on what type of problem you are trying to solve. From the picture above, you can see that there is a basic input, an output, and some calculations that happen in between. 

The calculations are what makes this algorithm ultimately work, and we will be going into detail about what exactly those are later. The algorithm is simulated via nodes which contain the input (in green), output (in red), and calculation (in blue) steps inside. As seen in the picture above, the arrow that leads from one computational node into the next computational node is what allows this recurrent neural network to have persistent memory and maintain information about past events. 

---

## Section 3.2: What is a Long Short Term Memory Neural Network?

### The Problem with RNNs...

![The Vanishing Gradient Problem](./images/VanishingGradient.jpg "The Vanishing Gradient Problem")
###### This illustrates the vanishing gradient problem, where as the node values get closer to the extremes (over time), large changes in input can yield very minimal changes in output.

Now that you have somewhat of an understanding of what Recurrent Neural Networks are, we can dive into looking at the actual topic - Long Short Term Memory Neural Networks. 
All RNNs have feedback loops where some information about the past inputs is retained, but over time, the amount of information retained decays exponentially. This is called the vanishing gradient problem. For some situations, this is desired, as only the most recent information is truly necessary to solve the problem, but not for all problems. Take music for example - if we were to generate music and only have the computer remember the past 5-10 notes, that might not work because a lot of the information regarding the tempo, the general theme of the song, and larger structural patterns are all lost. The same goes for words in a sentence and sentences in a paragraph. Though you might be able to figure out what words go together more often, it would be hard to understand the general theme or context of the paragraph without more than 5 words. For this reason, it can be difficult to train standard RNNs to solve problems that include long-term temporal dependencies. 

### LSTMs save the day!
LSTM Networks are a special type of RNNs. They have a very similar layout, except LSTM computational units contain an additional process called a "cell state" that can maintain information over long periods of time. This cell state includes additional gates which control when information enters its memory, when it should be forgotten, and how it should contribute to determining the output. These gates solve the problem of losing information over time, as it controls exactly what is important and what is not important.

### A Supervised Deep Learning Algorithm
At the end of the day, Long short term memory neural networks are classified as a **Supervised Deep Learning** algorithm that can be used for classification or Regression. I know that was a lot of big words, but let's break it down.

**Supervised** simply means that in the training phase, we are feeding the neural network with data that has already been labeled with the correct answer. This allows for the neural network to correct itself and reconfigure its calculation nodes and memory gates in a way that is most optimized for the task it is trained for. To give an example, if we feed the neural network a bunch of text, letter after letter, it might be able to guess what the next letter is and then use the correct answer (the label) to judge whether it was right or wrong. If it is wrong, it will change its computational methods to be better next time, and if it is right, it will reinforce what it already has. This is opposed to unsupervised learning, where input just comes in without any labelling, allowing the neural net to discover for itself what the patterns are.

![Supervised Learning](./images/supervised.png "Supervised Learning Example")
###### This is an example of Supervised learning, where we tell the computer exactly what each thing is during the training phase. This is in contrast to the following picture, which is unsupervised.  
<br />  
  
![Unsupervised Learning](./images/unsupervised.png "Unsupervised Learning Example")
###### This is Unsupervised learning where input is not labeled upon entry. Only after classification does a human need to come in and find out what each group represents.
<br />

**Deep learning** corresponds to having multiple layers in between the input and the output layers. This is a common tactic to allow for more computation that could find hidden patterns within the code. LSTMs are inherently 'deep', as they always include multiple different layers within the temporal dimensions. This essentially works by chaining several machine learning practices and algorithms together so they can operate off of each other and while one looks at raw data and simplifies, the other can draw meaningful conclusions from a more closed set of input. This allows for higher level abstraction and can be useful in particular situations where data is extremely complex or hidden

---

## Section 3.3 How do Long Short Term Memory Neural Networks actually work?

### Common LSTM Terms
Before jumping in, we have to define some common terms that are used when talking about LSTMs.

* Cell: A term used to describe the current group of calculations taking place.

* Cell State: A collection of all information that has been stored throughout the chain of calculations.

* Gate: A regulator of information. LSTMs possess 3 gates that all carry out similar functions at different steps in a LSTM; Forget, Input, Output.

* Sigmoid Function: A mathematical function shaped like an S curve bounded by y=[0,1]

* Hyperbolic Tangent: Another mathematical function also shaped like an S curve, but bounded by y=[-1,1]

![Common Activation Functions](./images/CommonActivationFunctions_Cropped.jpg "Common Activation Functions")
###### The sigmoid and tanh functions are both used in the activation step during calculation.


### How do LSTMs work?

Unlike standard RNNs that possess only one layer, LSTMs utilize multiple layers as a means to store long term dependencies. LSTMs feature what is called a cell state, or a collection of all information that has been stored throughout the chain.  
<br />

### The Big Picture: 
![LSTM Big Pic](./images/LSTM.png "A typical LSTM computational cell")
###### This is the typical layout of a computational cell within the LSTM. We will look at each specific gate more in detail below.

This cell state acts as a conveyor belt, traveling in a straight path across the different cells, both storing important information for later, forgetting no longer useful information, and assisting the cell with calculations by providing a filtered set of its memory to the main calculation path. How does the cell state update and how does the network know what pieces of information to keep? This is where the previously mentioned gates work their magic.  
<br />

### The Forget Gate: 
![Forget Gate](./images/ForgetGate.png "A focused picture of the forget gate within LSTMs")
###### Forget gates are the method by which LSTMs remove irrelevant information from their calculations.

The first gate is called the “forget gate”. This gate will look through both the previous cell’s output (O<sub>t-1</sub>) and the next input (I<sub>t</sub>) and assign the information within the cell state values to determine which of the specific pieces of information will remain and which ones the state can “forget”. This gate is a sigmoid layer so it will output a value between 0 and 1 for the combined (O<sub>t-1</sub>,I<sub>t</sub>). If the information is assigned a 0, then the state will get rid of it and if the information is assigned a 1 then the information will stay. The forget gate output is multiplied by the cell state to remove all information with an assigned value of 0, or the information that the state no longer needs.  
<br />

### The Input Gate
![Input Gate](./images/InputGate.png "A focused picture of the input gate")
###### Input gates are where cell states get new information based on previous and new input.

The next gate is the “Input gate”, where the cell state will get new information based off of the previous output and new input. First, (O<sub>t-1</sub>,I<sub>t</sub>) is sent through a sigmoid input layer to obtain output with 0s and 1s. At the same time, another copy of (O<sub>t-1</sub>,I<sub>t</sub>) is passed through a tanh layer, which will create a vector of possible new information to add onto the cell state where the different nodes on the vector have values anywhere between -1 and 1. These two outputs are multiplied to filter out information in the vector that the input gate didn’t want and then added onto the cell state. While the cell state will be used in the next step, all of the information in the cell state after the input gate gets passed onto the next cell in the chain.  
<br />

### The Output Gate
![Output Gate](./images/OutputGate.png "A focused picture of the output gate")
###### Output gates are where the information from the previous two gates combine to produce an output.

The final gate is the output gate. While the prior two were manipulating the cell state, this gate uses the information from the cell state along with the previous cell output combined with the new input. First the sigmoid layer determines what information from (O<sub>t-1</sub>,I<sub>t</sub>) will be used in the new output, and this output of 0s and 1s is multiplied by a tanh layer of the cell state itself. This creates the final output for the individual cell, that will get passed onto the next one in the chain along with the cell state.

---

## Section 3.4 Code Walkthrough

LSTMs can be used to generate predictions in text. Below is a simple LSTM using Tensorflow (Keras) to predict sentence endings based off of training data from Dr. Seuss' "The Cat in the Hat". 

You can find the links to the data and the tutoral here:
* [Dr. Seuss Poem Data](https://www.oatridge.co.uk/poems/d/dr-seuss-cat-in-the-hat.php)
* [Tutorial from Harsh Bansal](https://bansalh944.medium.com/text-generation-using-lstm-b6ced8629b03)

The first step is to import the necessary packages. Here is the list:
```
import numpy 
import sys

from nltk.corpus import stopwords
from nltk.tokenize import sent_tokenize, word_tokenize

from keras.models import Sequential
from keras.layers import Dense, Dropout, LSTM
from keras.utils import np_utils
from keras.callbacks import ModelCheckpoint
```

Now, we want to load all the text input from the poem into Python.

```
file = open("cat_in_hat.txt", "r")
lines = file.readlines()
```
Next, we will split each word in the text into a separate object using the tokenize class. Following that, we will use a tool called one-hot-encoding to convert the poem into binary. This changes the English text into a format that the computer can understand.

```
words=word_tokenize(file)
words=" ".join(words)

chars = sorted(list(set(processed_inputs)))
char_to_num = dict((c, i) for i, c in enumerate(chars))
```

Store the number of inputted words, as well as the number of unique vocabulary words from the text.

```
input_len = len(processed_inputs)
vocab_len = len(chars)
```

Define sequence length (number of characters considered) and convert the data to readable form.

```
seq_length = 100
x_data = []
y_data = []

for i in range(0, input_len - seq_length, 1):
    in_seq = words[i:i + seq_length]
    out_seq = words[i + seq_length]
    x.append([char_to_num[char] for char in in_seq])
    y.append(char_to_num[out_seq])
    
n_patterns = len(x_data)
```

Format the input as x, and output as y, and convert the output to binary with one-hot-encoding.

```
X = numpy.reshape(x, (n_patterns, seq_length, 1))
X = X/float(vocab_len)
y = np_utils.to_categorical(y)
```

Create a 3-layer LSTM, the first two will have 256 units of memory and will store sequences of input data. The last will have 128 units of memory, and will generate a prediction for the next character in the sequence. 

```
model = Sequential()
model.add(LSTM(256, input_shape=(X.shape[1], X.shape[2]), return_sequences=True))
model.add(Dropout(0.2))
model.add(LSTM(256, return_sequences=True))
model.add(Dropout(0.2))
model.add(LSTM(128))
model.add(Dropout(0.2))
model.add(Dense(y.shape[1], activation='softmax'))
```

Compile the model using an optimizer.

```
model.compile(loss='categorical_crossentropy', optimizer='adam')
```

Fit the model based on the generated input and output.

```
model.fit(X, y, epochs=4, batch_size=256, callbacks=desired_callbacks)
```

Change the output from binary to readable characters and use the model to generate a sequence of characters. 

```
num_to_char = dict((i, c) for i, c in enumerate(chars))
tart = numpy.random.randint(0, len(x_data) - 1)
pattern = x_data[start]
```

Predict the characters next in your pattern and print it to terminal.

```
for i in range(1000):
    x = numpy.reshape(pattern, (1, len(pattern), 1))
    x = x / float(vocab_len)
    prediction = model.predict(x, verbose=0)
    index = numpy.argmax(prediction)
    result = num_to_char[index]
    seq_in = [num_to_char[value] for value in pattern]
    sys.stdout.write(result)
    pattern.append(index)
    pattern = pattern[1:len(pattern)]
```

Hopefully, this shows you a sneak peek at how LSTMs can be created and used to do very powerful calculations. This was a fairly simple example using a common children's book, but we could easily extend this example from fictional novels to genomic data, where instead of inputting words and letters, we can input genes and entire genomes. In the next few sections, we will explore some of these uses and how LSTMs have impacted what we understand about the human genome.

---

## Section 3.5  Compare and Contrast

### When do I use what algorithm?
Now that you have seen how powerful LSTMs can be with specific data, you might be urging to get up out of your seat and start coding your own! We applaud your excitement, but before you start, you need to make sure you are using the right tool for the right job. LSTMs are one of many different machine learning algorithms out there, and each has its own pros and cons. How do you pick which to use? And after you pick which one to use, how do you choose the factors to customize that to your own data? Well.. there really isn't a clear answer. Many of these tools can be used for multiple different things, but some are definitely better at certain jobs. Often times, scientists will attempt the same problem using multiple different algorithms and pick the one that performs the best for their situation. This even includes stringing different types of ML algorithms together in a chain to find different complex relations in your data.

Take a look at the following chart as a helpful guide to start your journey on the right track when picking which machine learning algorithm to use.

### Comparison Chart

|Machine Learning Algorithm|Description             |Type of Data  |When to use?  |
|--------------------------|------------------------|--------------|--------------|
|Multi-Layer Perceptrons   |A classical neural net  |Image, Text   |any input->output case|
|Convolutional Neural Nets |A neural net designed for images  |Image   |Image identification, feature analysis|
|Recurrent Neural Nets     |A neural net with memory|Speech, Text, Time-series data| Sequence prediction, classification |
|Long Short Term Memory    |An RNN built to identify long-term interactions |Speech, Text, Music, Time-series data  |Sequence Prediction, classification|
|Generative Adversarial Networks | An unsupervised ML tool to generate data|Image, Text  |When you want to generate new data|

---
## Section 3.6 Genomic Applications of Long Short Term Memory

Now that we have an enhanced understanding of LSTM Networks, let’s take a look at both how they can be used right now and how they may be utilized in the future.

### Sequence Alignment:

Due to their ability to hold onto information over many iterations of inputs and calculations, LSTMs have the framework to calculate ideal alignment between sequences. By storing the reference sequence in the cell state and adding on potential alignment vectors each time step, a query sequence input can be analyzed across the entire reference sequence to look for the alignment with the highest score.

LSTM-Alignment has many potential improvements over currently available alignment, multiple sequence alignment, and long alignment softwares. LSTMs can handle much longer sequences due to the cell state, and may even be more accurate with proper algorithm training. 

[Read the scientific paper here!](https://ieeexplore.ieee.org/abstract/document/8754024)

### Sequence Prediction: 

Another example of LSTMs being able to identify long-range correlation between genomic sequences can be seen with identifying neanderthal introgression levels in modern human genes. To do this, the trained LSTM model has the ability to compare k-mers from modern human genes with neanderthal DNA to determine if the gene has ancestry within the Neanderthal reference.

[Read the article here!](https://towardsdatascience.com/lstm-to-detect-neanderthal-dna-843df7e85743)

### Future Directions:

We are just beginning to unlock the powers that LSTMs have, and in the future they may be one of the most important components of genomic research. Bioinformatics is at the cusp of the distinct fields of computer science, biology, natural language processing, and data science. Crossing multidisciplinary boundaries can lead to new and profound discoveries. We are excited to see what you all have to come up with in the near future!
