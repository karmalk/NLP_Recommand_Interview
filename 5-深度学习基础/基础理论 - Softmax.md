# 基础理论 - Softmax

---

## 1. Softmax 定义

$$
P(i) = \frac{e^{a_i}}{\sum_{k=1}^T e^{a_k}} \in [0,1]
$$



## 2. Softmax 损失

$$
L = - \sum_{j=1}^T y_j \, log \, s_j  \\
$$



## 3. Softmax回归

Softmax回归（Softmax Regression）又被称作多项逻辑回归（multinomial logistic regression），它是逻辑回归在处理多类别任务上的推广。

在逻辑回归中， 我们有m个被标注的样本： ![[公式]](https://www.zhihu.com/equation?tex=%5Cleft%5C%7B+%28x%5E%7B%281%29%7D%2Cy%5E%7B%281%29%7D%29%2C...%2C+%28x%5E%7B%28m%29%7D%2Cy%5E%7B%28m%29%7D%29+%5Cright%5C%7D) ，其中 ![[公式]](https://www.zhihu.com/equation?tex=x%5E%7B%28i%29%7D%E2%88%88R%5E%7Bn%7D) 。因为类标是二元的，所以我们有 ![[公式]](https://www.zhihu.com/equation?tex=y%5E%7B%28i%29%7D%E2%88%88%5Cleft%5C%7B+0%2C1%5Cright%5C%7D) 。我们的**假设**（hypothesis）有如下形式：![[公式]](https://www.zhihu.com/equation?tex=h_%CE%B8+%28x%29%3D%5Cfrac%7B1%7D%7B1%2Be%5E%7B-%CE%B8%5ET+x+%7D%7D)

代价函数（cost function）如下：

![img](https://pic4.zhimg.com/80/v2-dcd58c1784f47654d4713b942f045b3f_hd.jpg)

在Softmax回归中，类标是大于2的，因此在我们的训练集![[公式]](https://www.zhihu.com/equation?tex=%5Cleft%5C%7B+%5Cleft%28+x%5E%7B%281%29%7D%2C+y%5E%7B%281%29%7D%5Cright%29%2C...%2C%5Cleft%28+x%5E%7B%28m%29%7D%2C+y%5E%7B%28m%29%7D%5Cright%29+%5Cright%5C%7D) 中， ![[公式]](https://www.zhihu.com/equation?tex=y%5E%7B%28i%29%7D%5Cin%5Cleft%5C%7B+1%2C2%2C...%2CK+%5Cright%5C%7D) 。给定一个测试输入*x*，我们的假设应该输出一个K维的向量，向量内每个元素的值表示*x*属于当前类别的概率。具体地，**假设** ![[公式]](https://www.zhihu.com/equation?tex=h_%7B%5Ctheta%7D%28x%29) 形式如下：

![img](https://pic4.zhimg.com/80/v2-1dfdd8b84d08418d77d5d0cc526a209b_hd.jpg)

代价函数如下：

![img](https://pic1.zhimg.com/80/v2-4cb79560dcab6a2a8efafa4c23cae74c_hd.jpg)

其中1{·}是指示函数，即1{true}=1,1{false}=0



既然我们说Softmax回归是逻辑回归的推广，那我们是否能够在代价函数上推导出它们的一致性呢？当然可以，于是：

![img](https://pic1.zhimg.com/80/v2-bb919929ec2d7ac77b02409c552ca354_hd.jpg)

可以看到，逻辑回归是softmax回归在K=2时的特例。

---

## QA

### 1. 为何一般选择 softmax 为多分类的输出层

虽然能够将输出范围概率限制在 [0,1]之间的方法有很多，但 Softmax 的好处在于， 它**使得输出两极化**：正样本的结果趋近于 1， 负样本的结果趋近于 0。 可以说， Softmax 是 logistic 的一种泛化。

