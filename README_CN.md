CASRec:面向冷启动序列推荐的置信度感知SASRec
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

传统 SASRec 中：

每个物品表示为：

e
i
	​

=Embedding(item_id)

例如：

商品	交互次数
iPhone 15	500000
Nike Air Jordan	300000
新上架跑鞋	10

训练过程中：

热门商品
被点击几十万次
Embedding不断更新
参数逐渐收敛

最终：

e
popular
	​


质量很高。

冷启动商品

可能只出现几次：

e
cold
	​


几乎没有被训练。

因此：

Quality(e
cold
	​

)≪Quality(e
popular
	​

)

导致：

推荐不准
长尾物品难曝光
新商品难获得流量





