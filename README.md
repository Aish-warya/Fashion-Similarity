# Fashion-Similarity
Initial Project Ideas -  
The initial project Idea was to do something with Fashion images. Why chose this? Because it is interesting to solve and there’s a huge customer base that buys fashion online. Initial idea was to do a Fashion box recommendation, meaning recommending products to buy that go together.
Project Proposal 
Online shopping is a big thing. When you don’t have time to spend in the market, shopping online saves your day. But who wants to spend hours browsing for items when you already have an idea of what you want. Obviously Exploration-exploitation tradeoff. But if you know what you are looking for online, you would be happier if the e-commerce platform could return you similar results. 
Data Wrangling
Downloading, exception handlings, cluster making.
		The dataset used is at http://www.tamaraberg.com/street2shop

In-depth Analysis (Machine Learning) 
The first step is to download the dataset i.e. the pictures. This is done using the urllib package in python. When we are downloading the images we are making sure we are applying a bounding box also, so that the final saved image is the one with our region of interest.
Then we are using Keras pre-trained vgg19 model to extract features from our images. The model is pre-trained on ImageNet dataset as described in the Keras Documentation. We are directly using it for getting features.
After we have our vgg19 vectors calculated, we store them in a pickle file. These are of dimensions (1,4096). 
The next step is that we prepare our training and testing data. Our training data will have the format as -
training pairs, training_y - (Vgg19 vector of img_1, Vgg19 vector of img_2) , ( 1 or 0 - depending whether similar or not) 
Similarly we will have our testing data.
The next step will be to create our siamese network. This network will take two input images and learn how similar they are.

In Siamese networks, we take an input image of a person and find out the encodings of that image, after that we take the same network without performing any updates on weights or biases and input a different image and again predict it’s encodings. Once our siamese network is trained, we have got the final embeddings of the image. We store these embeddings in a dictionary with keys as unique image_ids.

We are now ready to use the model - 
Download a query image and get it’s vgg19 vectors.
Pass the vector to our siamese network and get the embedding for the query image.
Using scipy.spatial.cdist we calculate the distances of this embedding with our final embeddings stored in dictionary.
We return the top 10 closest embeddings and mapping it to their corresponding images we are able to find Top 10 similar dresses to our query image of dress.
Viola! You are done.

