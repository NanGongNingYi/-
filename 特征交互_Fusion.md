# 二、Fusion
融合不同的多模态信息，与bridge相比，融合更关注项目之间的多模态内部关系。  
它可以灵活地融合不同权重和焦点的多模态信息。  
注意机制是应用最为广泛的特征融合。
## 2.1 粗粒度注意力。
一些模型应用注意力机制在粗粒度级别融合来自多种模式的信息。  
### 注：将多模态信息分为用户侧和项目侧，包括各自的id信息和side信息：UVCAN、MCPTR。  
### UVCAN: User-Video Co-Attention Network for Personalized Micro-video Recommendation
在本文中，我们探讨的一个假设是，不仅用户具有多模态兴趣，而且微视频也具有多模态目标受众群体。使用注意力机制从用户和微视频端学习多模态信息。此外，UVCAN 以堆叠注意力网络方式解释用户和微视频的注意力。  
UVCAN[32]将多模态信息分为用户侧和物品侧，包括各自的id信息和side信息。它利用用户侧的多模态数据，通过自注意力生成项目侧的融合权重。  
![image](https://github.com/NanGongNingYi/-/assets/61775768/cb0033f3-14a5-4cd8-bc0d-7e57bad42769)
协同过滤的插图通过三步推理堆叠了注意力网络框架来探索用户对微视频特征的关注。  
### MCPTR: 

### 注：CMBF、MML、MCPTR、HCGCN引入交叉注意力机制来分别共同学习图像和文本模态的语义信息。  
### CMBF:

### MML: 

### MCPTR: 

### HCGCN: 

