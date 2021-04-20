# BioFaceNet

This file implement BioFaceNet proposed in [Alotaibi, S., & Smith, W. (2019). Biofacenet: Deep biophysical face image interpretation. arXiv preprint arXiv:1908.10578]

# p1&p2
The whole porcess has been implemented and can be run successfully. But there are three differences with the original paper which avoid this network to be poperly trained. 

1. The paper uses celeB data but I cannot find the data with actucal shading and actual mask which are used in the training. (so I just create a placeholder for it).

3. Through I installed MatConvNet correctly (the test file ran successfully) and I forced the server to be true (since I have no access to matlab server), I cannot find setup_autonn, vl_nnillumD. thus the following codes cannot be run and I cannot get the value for illD. (I could achieve all other pre-defined parameters, but in the code I just use random variable in setup block). Since I cannot run matlab code properly, the whole python code are built based just on my unserstanding of the paper and matlab code.

        illumDlayer = Layer.fromFunction(@vl_nnillumD);
        illD   = illumDlayer(CCT,illumDNorm);
        illuminantD = illD.*weightD; 

3. In computeSpecularities: it says %     Specularities    : H x W x 1 x B, but I think it should be  Specularities    : H x W x 3 x B.

# p3

The overall architecuture is great since it utilizes the residual block and re-build the image step-by-step.
Here are some ideas on improvements

1. May be we can add a few layers at the beginning to do some semantic segmentation or masking to remove the backgroung (pre-trained model or a few conv layers can be used).
2. Since there exist seome theoritical based decomposition methods, I thought if it possile to incorporate them in this model to solve the underconstrainted problem. For instance, if we use some methods to get the four output images, we may use a simple conv layer and add them to the layer layer of Decoder so that the network only need to modify on the given images. 
3. If we use theoritical decomposition method or have dataset with all decomposition, we may be able to build a network with two U-nets. Then we can drop the b and lighting parameters and just encodes the image into four biofaces and then decode it. And the loss should be the sum of reconstruction loss + encoding loss.
4. Most of the parameters setting are domain-specific, is it possible to train them simultaneously in the model? For instance, let the model selects the number dimensions of camera model. (weighted sum of different dimension's value).


