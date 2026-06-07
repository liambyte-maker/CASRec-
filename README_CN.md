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





