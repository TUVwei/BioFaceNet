# BioFaceNet

This file implement BioFaceNet proposed in [Alotaibi, S., & Smith, W. (2019). Biofacenet: Deep biophysical face image interpretation. arXiv preprint arXiv:1908.10578]

# p1&p2
The whole porcess has been implemnted and can be run successfully.

but there are three differences which avoid this network to be poperly trained. 

1. The paper said it used celeB data but I cannot find the data with actucal shading and actual mask which were used in training. (so I just create a placeholder for it).

3. Through I installed MatConvNet correctly (the test file ran successfully) and I force the sever be true (since I have no access to matlab server), I cannot find setup_autonn, vl_nnillumD. Thus the following codes Cannot be run and I cannot get the value for illD. (I could achieve all others pre-defined parameters, but in the code I just use random variable in setup block). Since I cannot run matlab code properly, the whole python code are built based just on my unserstanding of the paper and matlab code.

        illumDlayer = Layer.fromFunction(@vl_nnillumD);
        illD   = illumDlayer(CCT,illumDNorm);
        illuminantD = illD.*weightD; 

3. In computeSpecularities: it says %     Specularities    : H x W x 1 x B, but I think it should be  Specularities    : H x W x 3 x B.

# p3

The overall architecuture is great since it utilizes the residual block and re-build the image step-by-step.
Here are some ideas on improvements

1. May be we can add a few layers at the beginning to do some semantic segmentation or masking to remove the backgroung (pre-trained model or a few conv layers can be used).
2. 
3. Most of the parameters setting are domain-specific, is it possible to train them simultaneously in the model? For instance, let the model selects the number dimensions of camera model. (weighted sum of different dimension's value).


