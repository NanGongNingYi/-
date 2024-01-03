# 二、Fusion
融合不同的多模态信息，与bridge相比，融合更关注项目之间的多模态内部关系。  
它可以灵活地融合不同权重和焦点的多模态信息。  
注意机制是应用最为广泛的特征融合。
## 2.1 粗粒度注意力。
一些模型应用注意力机制在粗粒度级别融合来自多种模式的信息。  
### 注：将多模态信息分为用户侧和项目侧，包括各自的id信息和side信息：UVCAN、MCPTR。  
### UVCAN: User-Video Co-Attention Network for Personalized Micro-video Recommendation 2019
UVCAN将多模态信息分为用户侧和物品侧，包括各自的id信息和side信息。它利用用户侧的多模态数据，通过自注意力生成项目侧的融合权重。  
![image](https://github.com/NanGongNingYi/-/assets/61775768/cb0033f3-14a5-4cd8-bc0d-7e57bad42769)
协同过滤的插图通过三步推理堆叠了注意力网络框架来探索用户对微视频特征的关注。 

### MCPTR: Multi-Modal Contrastive Pre-training for Recommendation 2022
MCPTR建议并行合并项目和用户信息。每个模态占据相同的位置，自注意力机制决定融合权重。  
方法包含两个过程：预训练和微调。  
**在预训练阶段**，我们提出了一种基于辅助信息和隐式反馈矩阵 R 的多模态对比表示模型。具体来说，我们提出的预训练模型包含两个组成部分：用户建模和项目建模。  
**在用户建模部分**，我们首先使用文本编码器来获取每个评论文本的表示，然后使用模内聚合来获取用户的评论嵌入。接下来，应用图编码器来捕获齐次图 Gu 的结构信息。对于这两种不同的模态信息，我们开发了模态间聚合以获得用户的多模态表示。  
**在项目建模中**，我们利用文本编码器、图像编码器和图编码器对每个项目的描述文本、图像和齐次图 Gi 进行编码。然后，我们应用模间聚合来获得项目的多模态表示。此外，由于对于同一项目，描述文本和图像信息是互补的，因此它们具有相似的语义。我们开发了一种自我监督的对比学习方法来调整它们之间的表示。  
最后，采用基于反馈矩阵R的二元交叉熵损失函数来捕获目标用户u与其对应的目标项目i的潜在相关性。**在微调过程中**，现有的推荐模型利用预先训练的用户/项目嵌入作为初始化，并仅基于反馈矩阵 R 微调这些嵌入。  
![image](https://github.com/NanGongNingYi/-/assets/61775768/d1deaaab-da29-486e-8ab0-8b3e60508da9)

### 注：CMBF、MML、MCPTR、HCGCN引入交叉注意力机制来分别共同学习图像和文本模态的语义信息。  
### CMBF: Cross-Modal-Based Fusion Recommendation Algorithm 2021
CMBF引入交叉注意力机制来分别共同学习图像和文本模态的语义信息，然后将它们连接起来。  
现有的多模态推荐算法都是提取单一模态的特征并简单拼接不同模态的特征来预测推荐结果。这种融合方法不能完全挖掘多模态特征的相关性，丢失了不同模态之间的关系，影响了预测结果。  
在本文中，我们提出了一种基于跨模态的融合推荐算法（CMBF），该算法可以捕获单模态特征和跨模态特征。我们的算法使用一种新颖的跨模态融合方法来完全融合多模态特征并学习不同模态之间的交叉信息。  
![image](https://github.com/NanGongNingYi/-/assets/61775768/7fbfe257-1887-42de-bdd8-26c9d011a1d3)  
基于CMBF的拟议框架概述。图像/文本特征学习层和跨模态融合层的详细信息分别如图2和图3所示。  
![image](https://github.com/NanGongNingYi/-/assets/61775768/8507b835-fd00-4f0c-b1c4-63570b8a37d6)  
特征学习层的图示。(a)代表图像特征学习层，(b)代表文本特征学习层。  
![image](https://github.com/NanGongNingYi/-/assets/61775768/8e74386a-66c5-4ff9-924c-b3d875b47b5e)  
跨模式融合层的图示。  

### MML: Multimodal Meta-Learning for Cold-Start Sequential Recommendation 2022
MML基于id信息设计了一个注意力层，并辅以视觉和文本信息。  
在MAML框架下，我们提出的MML将多模态信息（即相关的文本和图像数据）作为一种辅助信息纳入元学习过程中，以减少任务发散并提高跨任务知识迁移的有效性。具体来说，我们在两个方面利用项目的多模态信息。  
**首先**，为了尽量减少新老用户顺序特征的差异，我们精心设计了一组对应三种不同模态（即ID、文本和图像）的多模态元学习器，这可以通过参考彼此的预测来稳定和改进元训练过程。  
**其次**，考虑到新项目的特征差异，我们设计了一个冷启动项目嵌入生成器，它利用多模态信息来预热新项目的 ID 嵌入。 MML的整体架构如图1(a)所示。  
为了快速适应数据不足的冷启动用户，我们将MAML扩展到我们的场景，并设计一个三阶段算法来训练元学习器、嵌入生成器和依次预测融合层如图1(b)所示。**文章详细介绍了训练算法。**  
![image](https://github.com/NanGongNingYi/-/assets/61775768/58390983-049c-498f-95cd-fadcd99c6786)  

### HCGCN: Learning Hybrid Behavior Patterns for Multimedia Recommendation 2022
MCPTR每个模态占据相同的位置，自注意力机制决定融合权重。相比之下，HCGCN更关注项目本身的视觉和文本信息。  
![image](https://github.com/NanGongNingYi/-/assets/61775768/f0c38f0c-68f9-42ec-8857-114a8546f31c)

## 2.1 细粒度注意力。
多模态数据包含全局和细粒度特征，例如录音的音调或一件衣服上的图案。  
由于粗粒度融合通常是侵入性和不可逆的，它会损坏原始模态的信息并降低推荐性能。  
细粒度融合，选择性地融合不同模态之间的细粒度特征信息  
### 注：细粒度融合在时尚推荐场景中意义重大。
### POG: Personalized Outfit Generation for Fashion Recommendation at Alibaba iFashion 2019
POG是一个基于Transformer架构的大型在线服装推荐系统。在编码器中，通过多层注意力挖掘时尚图像中属于搭配方案的深层特征，不断实现细粒度的集成。  
![image](https://github.com/NanGongNingYi/-/assets/61775768/88a61273-e778-4f1c-9412-25a9b1aa227b)  
FOM 的架构。我们一次掩盖一件衣物。例如，我们在套装中遮盖一条牛仔裤。模型学会从候选池中选择正确的牛仔裤，以完成对套装中其它衣物的搭配。  
![image](https://github.com/NanGongNingYi/-/assets/61775768/5a2a3781-d771-4e04-b2f2-66f4c04bc898)  
POG的架构，是一个带有Per网络和Gen网络的编码器-解码器架构。套装物品是根据Per网络的用户偏好信号和Gen网络的兼容性信号逐步生成的。  

### NOR: Explainable Outfit Recommendation with Joint Outfit Matching and Comment Generation 2019
NOR应用了编码器-解码器变压器架构，其中包含细粒度的自注意力结构。它可以根据搭配信息生成相应的方案描述。  
![image](https://github.com/NanGongNingYi/-/assets/61775768/88507f16-a831-43ee-be96-d71bcbf645ee)  
所提出的神经套装推荐 (NOR) 架构的概述。 NOR包含三个部分：（1）顶部和底部图像编码器（对应图（a）），（2）匹配解码器（对应图（b）），以及（3）生成解码器（对应于图(c))。  
![image](https://github.com/NanGongNingYi/-/assets/61775768/f13d6c33-ac16-4a29-96a8-40e78962c419)  
神经时尚推荐架构 (NOR) 的详细信息。 (a) 顶部和底部图像编码器从图像中提取视觉特征 Ft 和 Fb。 (b) 使用相互注意机制，我们将视觉特征转换为潜在表示vt和vb。然后匹配解码器预测匹配指示符rtb。 (c) 在每个时间戳 τ 处，生成解码器采用跨模态注意机制来生成单词 wτ 。  

### EFRM: Explainable Fashion Recommendation: A Semantic Attribute Region Guided Approach 2019
EFRM还设计了语义提取网络（SEN）来提取局部特征，最后将两个特征与细粒度的注意力偏好融合。  
大多数先前的时尚推荐模型都以全局内容表示来理解服装图像，缺乏对用户语义偏好的详细理解，这通常会导致推荐性能较差。  
![image](https://github.com/NanGongNingYi/-/assets/61775768/9e99567d-d3eb-4394-a474-0a2b68ab9c0a)  
传统的（a）全局视觉空间和我们的（b）语义属性视觉空间之间的区别。  
![image](https://github.com/NanGongNingYi/-/assets/61775768/97c1c8f5-3390-45cb-a130-d688f0cff42e)
SAERS包含两个主要组件，即语义提取网络（SEN）和细粒度偏好注意（FPA）。  
具体来说，利用 SEN，我们首先获得语义特征空间中的时尚商品投影。接下来，我们设计 FPA 将用户投影到相同的语义特征空间中。  
然后，我们在成对学习框架下共同学习全局视觉空间和语义属性视觉空间中的项目表示。  
最后，通过属性偏好推断，我们可以生成可解释的推荐。  

### VECF: Personalized Fashion Recommendation with Visual Explanations based on Multimodal Attention Network 2019
VECF执行图像分割，将每个补丁的图像特征与其他模态集成。  
![image](https://github.com/NanGongNingYi/-/assets/61775768/db1995b2-72ad-46dc-98ce-7637142dd01c)  
所提出的 VECF 模型。红线表示为时尚形象建模设计的注意力机制。蓝线突出显示了用户评论的建模。  
对于一个时尚图像来说，并不是所有的区域对于用户来说都同样重要，即人们通常会关心时尚图像的少数部分。为了模拟这种人类感觉，我们在许多预先分割的图像区域上学习了一个注意力模型，基于该模型我们可以了解用户对图像上的哪些地方真正感兴趣，并相应地以更准确的方式表示图像。此外，通过发现这种细粒度的视觉偏好，我们可以通过突出显示图像的某些区域来直观地解释推荐。  
为了更好地学习注意力模型，我们还引入了用户评论信息作为弱监督信号，以收集更全面的用户偏好。在我们的最终框架中，视觉和文本特征通过多模态注意力网络无缝耦合。  

### UVCAN



### MM-Rec



























