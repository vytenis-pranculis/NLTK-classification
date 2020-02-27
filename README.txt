Answers (in order of narrative):

1. Since these articles are not of any specific nature, I have used Tfidf vectorizer with standart english stopwords and a tokenizer which lowercases the text, removes stop words and punctuation, and uses PorterStemmer to obtain word stems. 

4. Since the task requests to use Keras (or PyTorch) deep learning framework, Neural Network was the only type of clasifier I have tested. From some basic data exploration I have noted that there are 90 categories, thus I used a fixed 90 neuron layer for the output for all architectures. I have started with a simple one-hidden-layer architecture as a baseline. I then expanded the network to see if adding a second hidden layer woulf improve its performance, however that was not the case. I tried to remedy the overfiting of the second architecture by adding dropout layers, but this did not seem to produce the desired effect. I then attempted to expand the initial network laterally, however this did not improve accuracy as well. Thus, instead of exploring deeper architectures, I have ddecided to optimize the initial network (I acknowledge that this migh have been a local maxima and that building a very expansive network could've produced even better results, but the performance of the initial model was surprisingly good and so I decided not to spend too much time looking for a possible minor improvement and focus on the low hanging fruit of parameter optimization) 

3. I have chosen to go over parameter tuning in phases - firstly tuning #epochs and bach_size, then optimization method, learning rate, activation and finally dropout. It could've been done in a one singler grid search, however, that would have taken unreasonably long time. Another approach to the same problem might have been to use Bayesian search over the parameter grid, but as I am not super familiar with the details, the setup of such search would've taken too long. In the end, the step-wise optimisation seemed to produce quite good results.

2.
1st architecture: (input) - (512 + 'relu') - (90 + 'softmax') 
Test accuracy: 0.744

2nd architecture: (input) - (512 + 'relu') - (258 + 'relu') - (90 + 'softmax')
Test accuracy: 0.065

3rd architecture: (input) - (512 + 'relu' + 0.5 dropout) - (258 + 'relu' + 0.5 dropout) - (90 + 'softmax')
Test accuracy: 0.561

4th architecture: (input) - (2048 + 'relu') - (90 + 'softmax') 
Test accuracy: 0.684

Final model:
1st architecture: (input) - (512 + 'relu' + 0.1 dropout) - (90 + 'softmax') 
Test accuracy: 0.996

Micro-average quality numbers:
Precision: 0.9565, Recall: 0.7166, F1-measure: 0.8194
Macro-average quality numbers:
Precision: 0.5819, Recall: 0.3037, F1-measure: 0.3693