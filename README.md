# Image-Captioning
An image captioning model by combining a pre-trained VGG-16 image encoder with LSTM-based language decoder.
 
 
Here I build an image captioning model by combining a pre-trained VGG-16 image encoder from with LSTM-based language decoder from. 

This is an implementation of the following paper:

Show and tell: A neural image caption generator, O. Vinyals, A. Toshev, S. Bengio, D. Erhan, CVPR,
2015.

which requires the steps detailed below.

1. Setup Image Encoder:

Here I load pre-trained VGG-16 model with the weights trained on ImageNet. I also get rid of softmax, so I will
end up with fc2 layer producing 4096 feature encoding for a given image i.

<!---
2. Setup Language Decoder. Here you will start with the language decoder model that you used as part
of the end-to-end network in Part 6 of Assignment 3. You will need to pass image encoding xi as the
hidden state input into the rst LSTM cell (i.e., h0 = xi). However, this would only work if the hidden
state is dimension of the 4; 096, which is way too high dimensional. In order to get a more reasonably
dimensional representation you will need to insert a linear layer to project from R4;096 ! R300 (note
that Vinyals paper used 512-dimensional hidden state and image feature projection, so you could also
use 512 instead of 300, which will likely be a bit better). The remainder of the language decoder,
including the CrossEntropy loss should remain identical to Assignment 3.
3. Training Captioning Encoder-Decoder Architecture. For training the model you can follow the
training procedure in Assignment 3, by training on (imagei; sentencei) pairs. However, you will want to
freeze the Image encoder (not back-propagate through it). You can relax this and optimize/ne-tune
end-to-end once the language decoder is at, or close to, convergence. You are not required to ne-tine
the model end-to-end, though this will likely improve the results a little.
4. MAP and Sampling Inference. We will reuse the decoder inference functions from Assignment 3.
The only minor change that is needed is providing the rst hidden state from VGG-16 as opposed to
getting it from the language encoder.
5. Measuring Performance. For validation images compute the average BLEU score. Since for each
image there are 5 ground truth sentences, you will need to supply the same MAP inference for each of
5 ground truth sentences when computing the BLEU score.
