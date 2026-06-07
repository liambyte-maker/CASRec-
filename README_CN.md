# CASRec:面向冷启动序列推荐的置信度感知

# 项目简介
序列推荐（Sequential Recommendation)旨在根据用户的历史行为序列预测其下一步能感兴趣的物品。
近年来，基于Transformer的序列推荐模型，如SASRec,凭借自注意力机制（self attention)能够有效捕捉用户兴趣的动态变化，在工业界和学术界都得到了广泛应用
然而，SASRec 存在一个重要问题：
## 过度依赖 Item ID Embedding
对于热门物品，由于交互数据充足，其ID Embedding能够得到充分训练

然而对于长尾物品或者冷启动物品，由于曝光和点击较少，其ID Embedding往往训练不足，导致推荐效果明显下降
为了解决这一问题，本项目提出：
## CASRec（Confidence-Aware SASRec）
一种基于置信度感知的序列推荐框架
核心思想：
并非所有Item Embedding都同样可靠

CASRec 通过学习每个物品的置信度（Confidence),动态决定应该更相信 Item ID表示 or 物品特征表示，从而提升冷启动和长尾场景下的推荐效果

研究背景
SASRec 的局限性
Quality(embedding_cold​)≪Quality(embedding_popular​)

## 项目创新点：复现SASRec

<img width="1062" height="752" alt="image" src="https://github.com/user-attachments/assets/a77fb569-702a-4616-8e05-d6222b73c3b8" />

*Figure adapted from the original SASRec paper (Kang & McAuley, 2018).*

利用Self-Attention 建模

短期兴趣/长期兴趣/行为转移规律

模型会自动发现：商品之间的关系

## 创新点2：多因素置信度网络
https://github.com/liambyte-maker/CASRec-/blob/main/README_CN.md
CASRec认为： 不同商品的Embedding可信度不同

因此构建Multi-Factor Confidence Network，评估item Id embedding的可靠性
输入特征包括：
✳Interaction Count
✳CTR
✳Popularity
✳Item Age
✳Text Quality
✳Image Quality

输入MLP：

$$
g=\sigma(Wx+b)
$$

输出：g∈[0,1]
其中 g 表示当前物品 ID Embedding 的可信度。

## 创新点2：置信度感知融合机制

传统方法，只使用 eid
CASRec增加：特征Embedding

例如：✳类别
✳品牌
✳价格
✳文本
✳图片

构建e_feature

后进行自适应融合：

e=g*e_id+(1−g)e_feature

CASRec能够自动判断当前商品应该相信ID，还是内容特征
	​





