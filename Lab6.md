# Lab 6

**Hand in your solution in Canvas before midnight tomorrow (28 September). A single `fullName_lab6.py` file containing the solution.**

__Note: Neither Tensorflow nor the library Keras that Tensorflow uses works with Python 3.7. So those that have installed version 3.7 have to downgrade to version 3.6.6 or lower. ;(. See bottom of page for some help with doing that. An alternative is to use the [Collab page for the tutorial](https://colab.research.google.com/github/tensorflow/docs/blob/master/site/en/tutorials/keras/basic_text_classification.ipynb).__

## Text classification using a Neural Network

Follow the [Text classification with movie reviews](https://www.tensorflow.org/tutorials/keras/basic_text_classification) tutorial on the Tensorflow homepage. It is not neccessary to create the plot at the end.

You have to begin by installing the Tensorflow library.

```python
$ pip3 install tensorflow
```

Then follow the tutorial making sure you understand what is going on at each step.

```python
import tensorflow as tf
from tensorflow import keras
import numpy as np

[...]
```

Feel free to play around with the model when you are done, e.g. changing the training data, the layers in the model and the number of epocs to see what effect that has.

**TODO handin the code and results in comments**

## Answer the following question in comments

* How is the movie review data preprocessed and why was that neccessary?
* What is the format and type of the training and validation data that the `model.fit` method accepts?
* At what point (epoch) does the model start to overfit to the training data?
* Describe how the model's graph is structured.

## Appendix: Downgrading Python from 3.7 to 3.6.6

MacOS:
* Delete Python 3.7 from the Applications folder.
* Delete the folder "3.7" from Library/Frameworks/Python.Framework/Versions/
* Install 3.6.6 from Python.org, Downloads > MacOSX  and select "macOS 64-bit installer"
* Open a new terminal window and make sure you have the correct version, `python --version`

Windows:
* Control Panel, uninstall Python
* Install 3.6.6 from Python.org, Downloads > Windows and download and run an installer
* Open Command Prompt (`cmd`) and make sure you have the correct version, `python --version`

Visual Studio Code:
* If you are using Code and the Python extension from Microsoft, you have to uninstall the extension and install it again and reload, then run "Python: Select Interpreter" in the Command Pallete (⌘+Shift+P) and select "Python 3.6.6 64-bit".

Reinstall Python Libraries:
* `pip3 install nltk`
* `nltk.download('movie_reviews')` (the some goes for other corpora you want to use)
