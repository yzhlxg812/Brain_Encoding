# Brain_Encoding

We submitted an article on using machine learning technology for brain coding and related analysis to the AAAI 2023 conference.

Encoding models of brain activity provide new insights to understand how the brain represents real-world objects and to investigate the relations between biological and artificial neural networks. The majority of current neuroAI studies focused on the correspondence between the human visual system and computer vision models. We proposed that language-derived representation of natural scenes show more prominent effects than the perception knowledge and strongly engaged cortical regions beyond visual areas. Our results confirmed the coexistence of two distinct forms of knowledge representation of visual scenes in the human brain. 

Our main findings include: 1) compute vision models mostly captured neural activity in the visual system; 2) natural language models better encoded scene images in frontoparietal and attention networks; 3) multimodal fusion of image and text information highly boost knowledge representation in both visual and frontoparietal areas; 4) the inter-subject variability in scene understanding was dominant by the semantic component rather visual perception. Our study suggests that the neural representation of natural scenes was dominant by language rather than perception and may have a big impact on neuroAI and compute vision by seeing beyond the visual system.

Our method framework is roughly shown in the following figure.

![image](https://github.com/yzhlxg812/Brain_Encoding/assets/42958127/689ffb8c-b5bb-4ce4-8628-190345a6d6a9)

如图所示，我们采用了图像，文字和图像+文字等方式来构建脑编码模型，用以比较究竟是哪种编码方式更加接近大脑的真实认知过程。

对于图像信息：
    我们分别采用了ResNet-50, Vision Transformer（ViT） 来提取图像特征。
ViT:
    对于输入的图像，将图像分成若干小块，添加一个可学习的类别块，这个类别块将用于与所有的图像小块进行交互。对图像小块进行flatten操作，即将每个图像块一维向量，再将一维向量拼接起来组成二维向量。再对二维向量使用全连接层进行降维得到二维特征，至此完成了linear projection of flattened patches的操作。随后对输入特征加入位置编码。位置编码用于标示每一个图像块的相对位置。将预处理特征送入transformer encoder中得到交互特征f，也就是我们所提取的特征。

ResNet-50:
    我们将图像输入ResNet-50网络中，并且提取出了每一个stage的最后一层作为该stage的特征提取结果。此前的研究表明，分层神经网络的进化模式与大脑的工作方式很接近：越深的层往往学习的是更加抽象的信息。
