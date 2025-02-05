# 千载阑珊 —— 多模态文言古诗文映射系统


## 项目概述
**"寂然凝虑，思接千载；悄焉动容，视通万里。"**  ——  刘勰《文心雕龙·神思》  
当您驻足西湖烟雨时，是否渴望一句「山色空蒙雨亦奇」的应景？当您仰望边塞明月时，是否期待有人轻诵「明月出天山，苍茫云海间」？  
我们生活中的每时每刻，都藏着古诗的DNA。  
本项目致力于构建穿越千年的诗意桥梁，通过多模态embedding技术，实现从文字描述、图像、音频到经典古诗文的精准映射。  

## 灵感来源
在学习了Seq2Seq结构之后，不禁有种感觉，这种序列到序列的模型可以将任何两项有相关性的目标有机地联系起来。而在学习Embedding模型的过程中，这种体会越发加深了。  
比如，既然一个意境可以由文字来描述，那由文字堆砌成的意境也一定可以转化成一个嵌入在高维空间中的向量，相同的意境所代表的向量距离相近。  
这样一来，就可以做到，我们输入对某场景的文字描述，拍的景色或人物照片、录的视频、山涧幽谷的声音后，由一个Embedding模型从数据库中匹配到最合乎当前意境的古诗。  

计算机程序（至少目前）无法真正的感受这个世界，但却能够恰如其分地区分开这些体验；  
而人在感受着当下的体验时，不一定能立刻想起那句最恰逢其会的诗，但只要脑海中浮现出来这句诗，就会有种齿轮啮合，碱基配对，榫卯相接一样的圆满感受。  
这种计算机与人的互补，又怎么不算得上一种浪漫呢？  

## 技术架构
### 阶段一：文本语义匹配（进行中）  
- **模型架构**
  - 基座模型：`lier007/xiaobu-embedding-v2`  
  - 语义判别器：在R1问答数据上微调的Qwen-14B的增强标注模型  

- **训练数据**  
  | 数据类型       | 数量      | 来源                         |
  |----------------|-----------|------------------------------|
  | 原始古诗       | 54万+     | [chinese-poetry数据集](https://github.com/chinese-poetry/chinese-poetry)         |

- **微调方式**  
  提取一部分诗句作为锚点，然后用上述未经微调的embedding模型返回20句最相关的诗，送入本地部署的语义判别器详细分析哪一句最相近，然后把这一句最相近的诗作为正例，再让embedding模型返回1句最不相关的诗作为反例，构建三元组，作为微调数据集。  

- **评估指标**  
*待补充*  

### 阶段二：多模态扩展（即将到来）  
*待补充*  

