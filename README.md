# DeepSteganography
Ever sent a hidden message in invisible ink to your friends? Are you intrigued by the idea of cryptic message exchange? How about using images for this exchange? Steganography is what you need! It is one of the techniques of encryption and over the years, steganography has been used to encode a lower resolution image into a higher resolution image. But steganography using naive methods, like LSB manipulation, is susceptible to statistical analysis. Our model extends existing deep learning research for encoding multiple secret images onto a single cover by leveraging convolutional neural networks based deep learning architectures. DeepSteg allows senders to embed up to three secret images onto a single cover using an encoder network and then have multiple decoder networks to obtain the embedded secrets.




### Read our paper on [arXiv](https://arxiv.org/pdf/2101.00350.pdf)




## Idea
We aim to perform multi-image steganography, hiding three or more images in a single cover image. The embedded secret images must be retrievable with minimum loss. The encoded cover image must look like the original cover image. To perform this, we combine the idea of Baluja [1] and Kreuk et. al [3]. We take the network implementation idea of having a prep and hiding network as an encoder and a reveal network as a decoder from Baluja [1]. To extend this for multiple images, we pass multiple secret images via the
prep network and then concatenating these resulting data with the carrier image and then finally send this via the Hiding network. We then take the idea of having multiple decoders, one per secret image, from Kreuk et al to retrieve all the secret images from the container image.
To improve the security of our image retrieval model, we extend the idea presented by Baluja [1] of putting secret images with noise in the original cover image instead of putting the secret images at the LSBs of the original cover image.
</br>
</br>

## Architecture

#### ENCODER: 
Consists of multiple prep networks, each corresponding to separate secret image input. Prep network outputs are concatenated together with the cover image and then fed through the Hiding network.  
#### DECODER: 
The decoder network comprises of multiple reveal networks, each of which is trained separately to decode its corresponding message.  


[![Alt text](https://github.com/JapsimarSinghWahi/DeepSteganography/blob/master/Images/model.png)](https://www.youtube.com/watch?v=-lsr638W6KU&feature=youtu.be)`  
Figure 1. The image shows the DeepSteg architecture with multiple CNN based sub-networks. Inside the encoder, the prep networks convert the input secret images into images that can be concatenated to the cover. The concatenation is then passed through the hiding network to generate the encode cover. In the decoder network, separate reveal networks are deployed to generate the decoded secrets out of the encoded cover.

##### Prep Networks:
Each of the prep networks consists of the aggregation of 2 layers. With each of the layers made up of 3 separate Conv2D layers. The number of channels for these 3 Conv2D layers is 50, 10, and 5 respectively with the kernel sizes like 3, 4, and 5 for each
layer. The stride length constantly remains 1 along both the axis. Appropriate padding is added to each Conv2D layer so as to keep output image in the same dimensions. Each
Conv2d layer is followed with a ReLU activation.
##### Hiding Network:
The hiding network is an aggregation of 5 layers. With each of these layers made up of the 3 separate Conv2D layers. The underlying structure of the Conv2D
layers in the hiding network is similar to the Conv2D layers in the Prep Network.
##### Reveal Network:
Each of the reveal networks shares a similar underlying architecture with the hiding network, using 5 layers of similarly formed Conv2D layers.





## Implementation Details
The training details are explained below:
1. Adam optimizer has been used with a custom LR scheduler.
2. Learning rate remains constant with 0.001 till first 200 epochs, decreasing to 0.0003 from 200 epochs to 400 epochs and further decreasing it 0.00003 for remaining iterations.
3. Model has been trained for 750 epochs with a batch size of 256 and an additional 400 epochs with a batch size of 32.
4. To make sure weights are updated only once, reveal network weights are frozen before adding it to the full model.
5. Gaussian noise with 0.01 standard deviation is added to encoder’s output before passing it through the decoder.
6. Mean sum of squared error has been used for calculating decoder’s loss.
7. The loss used is for the full model is represented as:  
![Alt text](https://github.com/JapsimarSinghWahi/DeepSteganography/blob/master/Images/Loss%20Function.PNG)
8. While training the reveal network we only consider the secret image component of the loss.
9. During the full model training, the loss for both cover and secret image is taken into
consideration.



## Results

##### Hiding two secret images within the carrier image-
![Alt text](https://github.com/JapsimarSinghWahi/DeepSteganography/blob/master/Images/Results.png)
Figure 2. Left to Right Columns are: Cover Image, Secret Image1, Secret Image2, Encoded Cover Image, Decoded Secret Image1, Decoded Secret Image2  
</br>
</br>

##### Hiding three secret images within the carrier image-
![Alt text](https://github.com/JapsimarSinghWahi/DeepSteganography/blob/master/Images/Results_3images.png)
Figure 3. Left to Right Columns are: Cover Image, Secret Image1, Secret Image2, Secret Image2, Secret Image3, Encoded Cover Image, Decoded Secret Image1, Decoded Secret Image2, Decoded Secret Image3  
</br>
</br>

##### Loss Plot
![Alt text](https://github.com/JapsimarSinghWahi/DeepSteganography/blob/master/Images/loss.png)
Figure 4. Graph of Overall Training Loss vs Number of Epochs till 750 epochs

## References
[1] Shumeet Baluja. “Hiding Images in Plain Sight: Deep Steganography”. In: Advances in Neural Information Processing Systems 30. Ed. by I. Guyon et al. Curran Associates, Inc., 2017, pp. 2069–2079.   
[2] Francisco Ingham. DeepSteg: Implementation of Hidding Images in Plain Sight: Deep Steganography in Pytorch.   
[3] Felix Kreuk et al. Hide and Speak: Deep Neural Networks for Speech Steganography. 2019. arXiv: 1902.03083 [cs.SD].  
[4] Alexandre Muzio. Deep-Steg: Implementation of Hidding Images in Plain Sight: Deep Steganography in Keras.  
