# PROTEINS dataset classification
Here I have a little bit of research on how to classify enzymes in PROTEINS benchmark dataset. The feature of this dataset is that it is small, contains very tiny graphs sometimes, and does not have edge features. Therefore, it has the one of the lowest benchmark accuracy among other benchmark datasets

There are a little bit of exploration, and implementation of some models.
First is the baseline model -  neural network with linear layers with global average pooling in the beginning. 70% of accuracy achieved

Second one is the following network:
- Graph Convolution (4 dim -> 64 dim, dropout=0.5) + Relu
- Graph Convolution with attention (64 dim -> 64 dim, 16 heads, dropout rate = 0.6) + Relu
- Graph Convolution (64*16 dim-> 64*2 dim, dropout = 0.5) + Relu
- Linear (64*2 dim-> 64 dim) + Relu
- Linear (64 -> 2 dim) + Softmax

~73% of accuracy achieved.
More hidden dimensionality in convolution leads to overfitting. Less heads or hidden dimensionality leads to more poor performance. After many tries, this parameters in the structure seem to be the best

The third and best one is the Graph U-Net that follow the structure GCN -> U-Net (for embeddings) -> aggregation to get graph embeddings -> classification by linear models. This model showed ~77% of accuracy
More info can be found in the code, paper or the report 3 in the root

Also, here is the colab that allows to learn about graph u-net interactively:
https://colab.research.google.com/drive/1a8h990BHr-xZcSHJmQa3bu6VF2nWVVmt
