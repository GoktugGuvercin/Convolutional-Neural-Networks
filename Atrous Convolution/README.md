# Atrous Convolution

As we add more number of convolution layers to the network, we enlarge receptive field of feature maps and capture long range contextual 
information of the image as feature maps. However, while doing that, we need to reduce spatial resolution by max-pooling or striding. 
There are 2 main reasons for that:

1) Without striding and pooling, we cannot enlarge receptive field sufficiently and learn long range contextual features.
2) We need to decrease spatial size if we increase the number of channels to create a balance in terms of computational complexity. 

This situation triggers 2 main problems:

1) Reduced resolution due to consecutive striding and max pooling causes important low level details to be lost, which affects
   segmentation of object boundaries and small scale pieces adversely. This is called as decimation of detailed information. 

2) As we go deeper in neural networks, extracted features become more generalized and abstract, which is not useful to dense prediction
   tasks like segmentation. 

Atrous convolution can solve both of these problems. By adding holes between filter weights, it enlarges filter kernels before 
convolution operation. The number of holes is controlled by dilation rate. This approach helps to extract denser feature maps and 
increase receptive field rapidly without any need of pooling or striding. In other words, it is claimed that we do not have to use 
max-pooling and striding in consecutive convolution layers to obtain rapid increase in receptive field, instead we can use dilated 
convolution. It can enlarge the receptive field with same proportion, but it can also preserve spatial resolution at the same time. 
Apart from this, it allows us to control how densely feature maps are computed in convolution backbone. At this point, the phrase 
"the generation of dense/denser feature maps" seems confusing, but this is related to the proportion of input resolution to final 
feature map resolution. Let's assume that input image is 256x256, and final feature maps to be fed into dense layer are of 16x16, 
which means that the ratio would be 16. If we apply one max-pooling and downsample it into 8x8 maps, spatial density of computed 
feature responses would be lower. Hence, denser features can be interpreted as smaller input-output spatial ratio. 

<p align="center">
  <img src="https://github.com/GoktugGuvercin/Convolutional-Neural-Networks/blob/main/Atrous%20Convolution/images/dilated%20convolution.png" width="1000" height="400" />
</p>

The usage of atrous convolution with spatial pyramid pooling, called as ASPP module, was proposed in DeepLabV2, but it was also incorporated in next version, which is DeepLabV3. Atrous convolution layers in this module are initialized with different dilation 
rates and applied in parallel to capture multi-scale information. Detection and segmentation of objects at multiple scales are some issues encountered in deep convolution architectures. ASPP module is capable of extracting multi-scale context, so can alleviate this problem. 

## DeepLabV3

All ResNet architectures, no matter what version it is, start with a convolution layer of 7x7 kernel and 3x3 max-pooling. Both of them downsample the image by stride of 2. Hence, at the end of these two layers, the proportion of input resolution to extracted feature maps is equal to 4. Then, 4 convolution blocks show up in any version of this neural architecture; the structure and the size of filters in these blocks tend to vary depending on which version of ResNet is. However, the common property for all of them is that feature map resolution is reduced by half per block. This means that the output of entire network has 64 input-output resolution ratio. 

The design of DeepLabV3 actually relies on ResNet combined with ASPP module to alleviate its reduced feature map resolution hierarchy. ASPP module consists of 4 parallel convolution layers followed by batch-norm and relu activation. 3 of these layers utilizes 3x3 kernel with dilation rate of 6, 12, and 18, whereas last convolution adopts 1x1 kernel. For all of them, 256 filters are used with same padding option.

The main problem in ASPP module is the degeneration: As dilation rate gets larger, filter weights of its convolution layers are surpassed. In other words, fewer number of kernel weights are applied to valid image context. To solve this problem and cover global feature representatives to model, we insert global context module between ResNet backbone and ASPP module, which is composed of average pooling, 1x1 convolution with 256 filters and batch-norm layer:

* Window size of average pooling = (Width, Height) of its input
* 1x1 convolution has same padding.
* Batch-norm output is passed to relu activation. 
