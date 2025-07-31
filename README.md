# Human Response to Decision Support in Face Matching: The Influence of Task Difficulty and Machine Accuracy
This repo contains the “Code & Data” of the paper “Human Response to Decision Support in Face Matching: The Influence of Task Difficulty and Machine Accuracy”, presented at the 4th International Conference on Hybrid Human-Artificial Intelligence (HHAI 2025, June 9-13, in Pisa, Italy).

## License
This data and code is released under the GPL License. Please, consider consulting the licenses of the dataset [DemogPairs](https://ihupont.github.io/publications/2019-05-16-demogpairs) and the models [IR50](https://openaccess.thecvf.com/content_cvpr_2016/papers/He_Deep_Residual_Learning_CVPR_2016_paper.pdf) (available in [face.evoLVe](https://github.com/ZhaoJ9014/face.evoLVe)) and [LightCNN](https://ieeexplore.ieee.org/abstract/document/8353856).

****

## Contents
* [Introduction](#Introduction)
* [Hard Set and Normal Set](#HardSetandNormalSet)
* [Models](#Models)
* [Citations](#Citations)

## Introduction

In this repo you can find the _Normal Set_ and the _Hard Set_ used to carry out our experiments. Both sets consist of pairs from the [DemogPairs](https://ihupont.github.io/publications/2019-05-16-demogpairs) testing database, and their classification as _Normal_ or _Hard_ is based on the results obtained in [A Comparison of Human and Machine Learning Errors in Face Recognition](https://arxiv.org/pdf/2502.11337). In this study, a total of 540 pairs were tested by a total of 162 participants (10 different pairs per participant, 3 different participants per pair). Participants rated these pairs by answering the question "Are they the same person?" with the options "No", "Probably not", "Not sure", "Probably yes", or "Yes". This allows us to categorize some of these pairs according to the difficulty experienced by participants in solving the task. These 540 pairs were also evaluated by two state-of-the-art models jointly. These two models are [IR50](https://openaccess.thecvf.com/content_cvpr_2016/papers/He_Deep_Residual_Learning_CVPR_2016_paper.pdf) and [LightCNN](https://ieeexplore.ieee.org/abstract/document/8353856), and the joint accuracy over DemogPairs test dataset is above 95%. By "joint accuracy" we mean the accuracy based on the mean response of both models. This ensemble machine is the base decision support system we use in our experiments.

## Hard Set and Normal Set

* ***Hard Set***: We selected those pairs whose mean participant response was very close to "Not sure", and at least one of the three participants made a mistake. We also selected those pairs where the mean response is exactly "Not sure". We obtained a total of 69 pairs (63 positive and 6 negative). After a careful manual inspection, from among the 63 positive pairs we chose the 24 most difficult ones which together with the 6 negative ones (with no occlusion _i.e._, no objects obstructing parts of the face) form the _Hard Set_. These 30 pairs can be found in `sets > hard > imgs`. In `sets > hard > images.npy` we provide an ordered array of the filenames of the images, so each pair of filenames defines a pair of images.
* ***Normal Set***: We define another set of pairs with a slightly more relaxed human certainty condition: we selected those pairs whose mean response is close to "Not sure", avoiding those whose mean is exactly "Not sure". From these pairs we randomly choose 30 pairs of images, maintaining the above ratio of 24 positive and 6 negative pairs, and avoiding repetitions with the "Hard Set". This left us with 30 pairs that will form the _Normal Set_. These 30 pairs can be found in `sets > normal > imgs`. In `sets > normal > images.npy` we provide an ordered array of the filenames of the images, so each pair of filenames defines a pair of images.

## Models
LightCNN pre-trained model is available [at its repo](https://github.com/AlfredXiangWu/LightCNN/tree/master), while IR50 pre-trained model is available through the frameworks [face.evoLVe](https://github.com/ZhaoJ9014/face.evoLVe?tab=readme-ov-file#Model-Zoo). For our experiments we used the ensemble model IR50+LightCNN (we considered the mean response of both models). In `sets > hard/normal > score.npy` we provide an ordered array of the scores obtained from the ensemble model for the pairs in each set (hard/normal). These scores refer to the similarity of each pair and range from 0 to 1. Also, `sets > hard/normal > output.npy` we provide an ordered array with the outputs obtained from the ensemble model for the pairs in each set. The outputs can be TP (True Positive), TN (True Negative), FP (False Positive), or FN (False Negative). 

## Citations
Please consult and consider citing the following papers:

      @inproceedings{hupont2019demogpairs,
        title={Demogpairs: Quantifying the impact of demographic imbalance in deep face recognition},
        author={Hupont, Isabelle and Fern{\'a}ndez, Carles},
        booktitle={2019 14th IEEE international conference on automatic face \& gesture recognition (FG 2019)},
        pages={1--7},
        year={2019},
        organization={IEEE}
      }
      @article{wang2021face,
        title={Face. evolve: A high-performance face recognition library},
        author={Wang, Qingzhong and Zhang, Pengfei and Xiong, Haoyi and Zhao, Jian},
        journal={arXiv preprint arXiv:2107.08621},
        year={2021}
      }
      @inproceedings{he2016deep,
        title={Deep residual learning for image recognition},
        author={He, Kaiming and Zhang, Xiangyu and Ren, Shaoqing and Sun, Jian},
        booktitle={Proceedings of the IEEE conference on computer vision and pattern recognition},
        pages={770--778},
        year={2016}
      }
      @article{wu2018light,
        title={A light CNN for deep face representation with noisy labels},
        author={Wu, Xiang and He, Ran and Sun, Zhenan and Tan, Tieniu},
        journal={IEEE Transactions on Information Forensics and Security},
        volume={13},
        number={11},
        pages={2884--2896},
        year={2018},
        publisher={IEEE}
      }
