# 活体检测顶会论文及复习代码汇总

## 单帧

2020

### [Regularized Fine-grained Meta Face Anti-spoofing](https://arxiv.org/pdf/1911.10771.pdf)
https://github.com/rshaojimmy/AAAI2020-RFMetaFAS


### [Single-Side Domain Generalization for Face Anti-Spoofing](https://arxiv.org/abs/2004.14043)
https://github.com/taylover-pei/SSDG-CVPR2020

主要思想在于，对于不同数据集中的正常样本，我们去学习一个领域不变的特征空间；但是对于不同数据集中的攻击样本，我们去学习一个具有分辨性的特征空间，使相同数据集中的攻击样本尽可能接近，而不同数据集中的攻击样本尽可能远离。最终效果会使攻击样本在特征空间中张成更大的区域，而正常样本仅仅处在一个紧凑的区域中，从而能够学习到一个对于正常样本包围更紧致的分类器，以达到在未知的目标域上更好的性能，如下图右边所示。

具体来说，我们引用一个域判别器，利用一种单边的对抗学习，让特征提取器仅仅对于正常样本提取更具有泛化性能的特征。并且，我们提出一个不均衡的三元组损失函数，让不同数据集之间的正常样本尽可能接近而攻击样本尽可能远离，以使得攻击样本在特征空间中张成一个更大的范围。同时，我们还引入了特征和参数归一化的思想，进一步地提升模型的性能。大量实验表明，我们提出的方法是有效的，并且在四个公开数据库上均达到了最优的性能。

### [Learning Generalized Spoof Cues for Face Anti-spoofing](https://arxiv.org/abs/2005.03922)
https://github.com/Podidiving/lgsc-for-fas-pytorch

https://github.com/Ontheway361/antispoof-single-image

https://github.com/VIS-VAR/LGSC-for-FAS

从异常检测的角度来解决活体问题，假设活体样本具有某种共同属性，属于一个closed-set，而攻击样本作为这个活体closed-set意外的异常，属于一个open-set（如图1所示）。定义了一个spoof cue map的概念，即攻击和活体之间的difference，并明确这种spoof cue只在攻击中存在，在活体没有（spoof cue map是all-zero map）。为了学习这种spoof cue map，作者通过显式的regression-loss、隐式的metric-learning和辅助分类器来做监督，有意思的是这篇文章里只对活体做了显式监督，只对活体做显式监督，通过隐式监督在特征空间里推开攻击，更神奇的是，这篇文章直接使用spoof cue map的magnitude做预测，而不是用分类器，也就是作者用分类器的作用是为了让整个网络学习到更合适的spoof cue map，而不是用分类器做决策，个人感觉这从一定程度上减轻了通过二分类解决活体模型的泛化性问题。

### [Searching Central Difference Convolutional Networks for Face Anti-Spoofing](https://arxiv.org/pdf/2003.04092v1.pdf)
https://github.com/ZitongYu/CDCN

      depth image改进代码: https://github.com/clks-wzz/PRNet-Depth-Generation
      
      depth image原模型: https://github.com/YadiraF/PRNet

https://github.com/voqtuyen/CDCN-Face-Anti-Spoofing.pytorch

### [Learning Meta Model for Zero- and Few-shot Face Anti-spoofing](https://arxiv.org/abs/1904.12490)
https://github.com/qyxqyx/AIM_FAS

Zero-shot learning 旨在学习一般的区别特征，这些特征对可以从已知的假脸中检测未知的新假脸。Few-shot learning 旨在快速适应反欺骗模式，通过学习预先定义的假脸和收集到的少量新攻击的样本。

### [Deep Spatial Gradient and Temporal Depth Learning for Face Anti-spoofing](https://arxiv.org/abs/2003.08061)
https://github.com/clks-wzz/FAS-SGTD

### [Cross-ethnicity Face Anti-spoofing Recognition Challenge: A Review](https://arxiv.org/abs/2004.10998)

_待定_

https://github.com/1relia/CVPR2020-FaceAntiSpoofing

https://github.com/wgqtmac/cvprw2020

https://github.com/yaojieliu/ECCV20-STDN

https://github.com/JinghuiZhou/awesome_face_antispoofing



2019

### [FeatherNets: Convolutional Neural Networks as Light as Feather for Face Anti-spoofing](https://arxiv.org/pdf/1904.09290.pdf)
https://github.com/SoftwareGift/FeatherNets_Face-Anti-spoofing-Attack-Detection-Challenge-CVPR2019

### [Multi-adversarial Discriminative Deep Domain Generalization for Face Presentation Attack Detection](https://openaccess.thecvf.com/content_CVPR_2019/papers/Shao_Multi-Adversarial_Discriminative_Deep_Domain_Generalization_for_Face_Presentation_Attack_Detection_CVPR_2019_paper.pdf)
https://github.com/rshaojimmy/CVPR2019-MADDoG

### [FaceBagNet: Bag-of-local-features Model for Multi-modal Face Anti-spoofing](https://openaccess.thecvf.com/content_CVPRW_2019/papers/CFS/Shen_FaceBagNet_Bag-Of-Local-Features_Model_for_Multi-Modal_Face_Anti-Spoofing_CVPRW_2019_paper.pdf)
https://github.com/SeuTao/CVPR19-Face-Anti-spoofing

提出FaceBagNet with Model Feature Erasing(MFE)框架：用随机截取的人脸区域代替完整人脸来训练CNN网络，MFE则是在训练中随机去掉某种模态的特征，以增强泛化；提取特征的Backbone设计主要参考ResNext，pipeline也很简单，如下图。作者实验证明来用人脸局部图像作为输入比直接拿人脸有用的多，还对比了不同尺寸的patch对精度的影响，结果显示尺寸为32*32时效果最好，TPR要比全脸高出6个多点！然后作者就用这个尺寸的输入做MFE的实验，同时也比较了用循环余弦学习率方法和标准SGD训练的区别，结果能看出循环余弦学习率和MFE都有贡献。

## 多帧

### [Creating Artificial Modalities to Solve RGB Liveness](https://arxiv.org/abs/2006.16028)
https://github.com/AlexanderParkin/CASIA-SURF_CeFA
