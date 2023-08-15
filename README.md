# Brain_Encoding

We submitted an article on using machine learning technology for brain coding and related analysis to the AAAI 2023 conference.

Encoding models of brain activity provide new insights to understand how the brain represents real-world objects and to investigate the relations between biological and artificial neural networks. The majority of current neuroAI studies focused on the correspondence between the human visual system and computer vision models. We proposed that language-derived representation of natural scenes show more prominent effects than the perception knowledge and strongly engaged cortical regions beyond visual areas. Our results confirmed the coexistence of two distinct forms of knowledge representation of visual scenes in the human brain. 

Our main findings include: 1) compute vision models mostly captured neural activity in the visual system; 2) natural language models better encoded scene images in frontoparietal and attention networks; 3) multimodal fusion of image and text information highly boost knowledge representation in both visual and frontoparietal areas; 4) the inter-subject variability in scene understanding was dominant by the semantic component rather visual perception. Our study suggests that the neural representation of natural scenes was dominant by language rather than perception and may have a big impact on neuroAI and compute vision by seeing beyond the visual system.

Our method framework is roughly shown in the following figure.

![1](https://github.com/yzhlxg812/Brain_Encoding/assets/42958127/d09d9e6a-8fe4-4c39-a4f4-293e504e0426)


As shown in the figure, we used methods such as images, text, and image+text to construct a brain encoding model, in order to compare which encoding method is closer to the real cognitive process of the brain.

For image information, we used ResNet-50 and Vision Transformer (ViT) to extract image features.

**_ViT_**:
    For the input image, divide the image into several small blocks and add a learnable category block that will be used to interact with all the image blocks. Perform a flat operation on small image blocks, which involves concatenating the one-dimensional vectors of each image block to form a two-dimensional vector. Then, using a fully connected layer to reduce the dimensionality of the two-dimensional vector and obtain the two-dimensional features, the linear projection of flattened patches operation is completed. Subsequently, position encoding is added to the input features. Position encoding is used to indicate the relative position of each image block. Feed the preprocessed features into the transformer encoder to obtain the interactive feature f, which is the feature we extract.

**_ResNet-50_**:
    We input the image into the ResNet-50 network and extract the last layer of each stage as the feature extraction result for that stage. Previous studies have shown that the evolutionary pattern of hierarchical neural networks is very similar to the way the brain works: deeper layers often learn more abstract information.
       

For the capture of semantic information, we use the following methods:

**_BERT_**: 
    Enter the text description corresponding to each image provided in the COCO dataset into the BERT model. When using BERT for feature extraction of this sentence, first use a word splitter to segment it and add special tokens [CLS] and [SEP] at the beginning and end. Next, in order to maintain consistency in the length of all sentences in the training set, we will specify a "maximum length" max_ Length. For lengths less than this max_ Complete the sentence with length (fill in with [PAD]); And for those exceeding this max_ Cut the sentence with length. After using [PAD] as padding, an indicator is also required to indicate that [PAD] is only used for padding and does not represent any meaning. Here, a list called attention mask is used to represent it, which has a length equal to max_ Length. For each sentence, if the word at the corresponding position is [PAD], the element value of the attention mask at this position is 0, and vice versa, it is 1. Finally, since the model cannot directly recognize words and can only recognize numbers, it is also necessary to map words to numbers. We will first create a dictionary for the entire word library, with each word having a corresponding number (which is a non repeating number). After preparing the above data, the token can be_ Ids and attention_ The mask is input into the pre trained BERT model to obtain the embedded representation of each word.
    
**_Multi-hot_**: 
    We have established a matrix with dimensions (number of images, number of categories) based on the definition of COCO, and determined the matrix based on whether each image contains a certain category. If the image contains a certain category (such as people), we will set the value to 1 in the corresponding position of that category, otherwise it will be set to 0,. Through this simple method, we have represented the category information contained in the image.

Finally, we also adopted **_ViLT_**, a concise and efficient multimodal fusion model, to simulate brain encoding. Vision and Language Transformer (ViLT) was published at the International Conference on Machine Learning (ICML) 2021 ViLT can be seen as a minimalist multimodal learning framework baseline It distinguishing feature lies in minimizing the feature extraction process for each modality, while placing the main computational boundary on the feature fusion stage This approach has greatly advanced the field of multimodal learning To fuse the multimodal information of text and image, ViLT is pre trained on the following objectives: image text matching, masked language modeling, and word patch alignment The image and text encoding parts of ViLT are very similar to BERT and ViT, respectively, making them suitable for use as multimodal models in our experiments.


    
