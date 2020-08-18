# DeepSteganography
Ever sent a hidden message in invisible ink to your friends? Are you intrigued by the idea of cryptic message exchange? How about using images for this exchange? Steganography is what you need! It is one of the techniques of encryption and over the years, steganography has been used to encode a lower resolution image into a higher resolution image. But steganography using naive methods, like LSB manipulation, is susceptible to statistical analysis. Our model extends existing deep learning research for encoding multiple secret images onto a single cover by leveraging convolutional neural networks based deep learning architectures. DeepSteg allows senders to embed up to three secret images onto a single cover using an encoder network and then have multiple decoder networks to obtain the embedded secrets.


## Architectuure
[![Alt text](https://github.com/JapsimarSinghWahi/DeepSteganography/blob/master/Images/model.png)](https://www.youtube.com/watch?v=-lsr638W6KU&feature=youtu.be)`  
Figure 1. The image shows the DeepSteg architecture with multiple CNN based sub-networks. Inside the encoder, the prep networks convert the input secret images into images that can be concatenated to the cover. The concatenation is then passed through the hiding network to generate the encode cover. In the decoder network, separate reveal networks are deployed to generate the decoded secrets out of the encoded cover.


## Results

![Alt text](https://github.com/JapsimarSinghWahi/DeepSteganography/blob/master/Images/Results.png)
Figure 2. Result of hiding two secret images. Left to Right Columns are: Cover Image, Secret Image1, Secret Image2, Encoded Cover Image, Decoded Secret Image1, Decoded Secret Image2  </br>

![Alt text](https://github.com/JapsimarSinghWahi/DeepSteganography/blob/master/Images/Results_3images.png)
Figure 3. Result of hiding three secret images. Left to Right Columns are: Cover Image, Secret Image1, Secret Image2, Secret Image2, Secret Image3, Encoded Cover Image, Decoded Secret Image1, Decoded Secret Image2, Decoded Secret Image3  </br>

## References
[1] Shumeet Baluja. “Hiding Images in Plain Sight: Deep Steganography”. In: Advances in Neural Information Processing Systems 30. Ed. by I. Guyon et al. Curran Associates, Inc., 2017, pp. 2069–2079.   
[2] Francisco Ingham. DeepSteg: Implementation of Hidding Images in Plain Sight: Deep Steganography in Pytorch.   
[3] Felix Kreuk et al. Hide and Speak: Deep Neural Networks for Speech Steganography. 2019. arXiv: 1902.03083 [cs.SD].  
[4] Alexandre Muzio. Deep-Steg: Implementation of Hidding Images in Plain Sight: Deep Steganography in Keras.  
