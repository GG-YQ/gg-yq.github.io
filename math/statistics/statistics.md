# 统计原理

## 检验步骤
1. 提出原假设和备择假设
2. 确定适当的检验统计量
3. 规定显著性水平a
4. 计算检验统计量的值
5. 作出统计决策

## 检验类型
参考：https://py4ss.net/spss/

### 参数检验
参数检验要利用到总体的信息(总体分布、总体的一些参数特征如方差)，以总体分布和样本信息对总体参数作出推断；参数检验只能用于等距数据和比例数据。

- 正态总体均值的假设检验：检验1组数据样本的均值是否等于、大于或小于某个值，或者检验两组数据样本的均值的大小情况。其中的统计量z般服从t分布。
- 正态总体方差的假设检验：检验1组数据样本的方差是否等于，大于或小于某个值或者检验两组数据样本的方差的大小情况。其中单样本检验的统计量X2一般服从卡方分布。双样本检测的统计量F一般服从F分布。
- 非正态总体的假设检验：非正态总体的假设检验有很多，二项分布总体的假设检验相对较为常用，常用于随机抽样实验的成功概率的检验。

### 非参数检验
非参数检验不需要利用总体的信息(总体分布、总体统计参数特征)，以样本信息对总体分布的特征(例如如称性、分位数大小等等假设)作统计检验；非参数检验主要用于记数数据。也可用于等距和比例数据，但精确性就会降低。


- 独立性检验：具体有Pearson卡方检验，Fisher精确独立性检验。这些检验方法通常用于检验数据的分布和假设的影响因素的关系。
- 符号检验和秩和检验：检验样本与总体的情况，或样本总体间的差异。
- 拟合优度检验：统计量包括计数、秩、符号秩。对单个总体的分布形态等进行推断的方法，其中包括卡方检验、二项分布检验、K-S检验以及变量值随机性检验等方法。
    - Neyman-Pearson χ2拟合优度检验：检验样本数据是否符合某种分布，既可以用于检验数据的分布特性，又可以检验不同组数据之间的分布关系(是否是同一分布)。自由度为1时χ2变为独立性检验，自由度为正无穷大时χ2变为正态分布。
    - 二项分布检验：判断是否服从制定p的二项分布或两个是否服从同一二项分布。
    - 单样本K-S检验：Kolmogorov-Smirnov检验亦称D检验法，和Pearson方法一样属于拟合优度检验方法。Kolmogorov-Smirnov方法无需对要检验的数据分组，且使用经验累积分布函数(ECDF)来定义统计量，可以用于任何分布的检验;但是，Kolmogorov-Smirnov只适用于一元分布的情况。因此适用面与Pearson方法相比稍小。
- 游程检验：变量值随机性检验
- 总体分布的卡方（Chi-square）检验


# 计量模型

## 概述

### 评价指标

- 无偏性：估计值的期望等于真值。
    - 渐近无偏性：当样本容量n趋于无穷大时，估计值的期望等于真值。

- 有效性：无偏估计值中相对真值方差最小的估计。
    - 渐近有效性：某些估计值在中小样本时可能不是最有效的，但随着样本数的增加，慢慢变得有效（没有其它无偏估计可以得到更小的方差）。

- 相合性(一致性)：随着样本的增加，估计值与真值的差的绝对值趋近于零。无偏但是标准差不收敛到0也不一定相合。
    - 强相合：a.s.收敛
    - 弱相合：依概率收敛
    - Lp相合

### 基本方法

-   最小二乘法(OLS)

    -   原理：当从模型总体随机抽取n组样本观测值后，最合理的参数估计量应该使得模型能最好地拟合样本数据

    -   适用：误差项需要满足一些假设，例如要求正态分布、解释变量与误差项不相关

-   最大似然法(ML)

    -   原理：当从模型总体随机抽取n组样本观测值后，最合理的参数估计量应该是使得从模型中抽取该n组样本观测值的概率最大

    -   适用：误差项分布已知

-   矩方法(MM)：工具变量估计(采用工具变量法，当工具变量多于待估计参数个数，则工具变量估计具有信息上损失，不是有效估计)、GMM。

    -   原理：由辛钦大数定律知，简单随机样本的原点矩依概率收敛到相应的总体原点矩，总体原点矩又是分布中未知参数的一个函数，因此用样本矩估计总体矩，进而可以找出未知参数的估计。

    -   适用：允许随机误差项存在异方差和序列相关；不需要知道随机误差项分布

    -   优点

        -   可以克服随机解释变量问题

        -   可以充分利用多个工具变量的信息，进而克服过度识别问题

        -   不需要对模型随机项分布进行事先的设定

    -   局限

        -   对总体原点矩不存在的分布不能用：如柯西分布

        -   只涉及总体的一些数字特征，并未用到总体的分布，因此矩法估计量实际上只集中了总体的部分信息，这样它在体现总体分布特征上往往性质较差，只有在样本容量n较大时，才能保障它的优良性，因而理论上讲，矩法估计是以大样本为应用对象的。

-   从计量经济学模型方法论角度看，三个问题成为广义矩估计方法发展的导向。

    -   一是解释变量的内生性问题。计量经济学模型中变量的内生或者外生、随机或者确定，并不是变量本身所固有的绝对的属性，而是相对于模型的研究对象、模型系统，甚至模型中的参数而言的。经济变量，如果一定要给出它们的固有属性，只能说它们都是内生的和随机的，因为它们都是在社会经济系统中，在互相影响和作用的过程中生成的。同一个经济变量，相对于不同的研究对象、不同的模型系统，甚至不同的关注参数，可能有不同的设定。所以，如何克服解释变量的内生性问题，成为任何一项计量经济学应用研究回避不了的一个重要的问题。

    -   二是模型的过度识别问题。经济系统是复杂的，系统所包含的变量之间存在错综复杂的关系，有直接影响，也有间接影响。任何一个计量经济学结构模型，所包含的解释变量总是有限的，即对被解释变量产生显著的直接影响的变量。大量的对被解释变量产生间接影响的变量的存在，一方面造成了解释变量的内生性，另一方面带来了模型的过度识别问题。建立联立方程模型系统，可以解决过度识别问题。但是，研究者所关注的往往只是系统的一个局部，为了一个局部而建立庞大的模型系统，不仅耗费巨大，而且系统中误差的传递和积累，往往会得不偿失。所以，解决单方程计量经济学模型的过度识别问题，也是计量经济学应用研究中回避不了的一个重要的问题。

    -   三是模型随机项分布的设定问题。计量经济学模型通过对随机抽取的样本的一次观测值估计总体的参数，最常用的估计方法都需要首先对总体的分布进行设定，例如假设模型随机项服从正态分布或其它某一已知分布。在应用研究中，由于不可能实现对某一样本的"重复抽样"，所以该分布是不可能准确设定的。

## OLS

### 基本假设

-   保证无偏估计的基本假设

    -   假设1线性模型假设：线性于参数

    -   假设2随机抽样假设：样本之间相互独立，保证误差项之间不相关。

        -   混合横截面数据一般也可认为满足独立抽样假设，关键问题是相互之间的关系有多大、前后结构变化有多大：空间回归中的样本相关性问题

        -   一般来说，时间系列数据不满足独立抽样假设，不同时间之间样本具有相关性：如果样本是弱相关的，即$(x_t,y_t)$和$(x_{t-s},y_{t-s})$随着时间推移渐进不相关，则依然可以使OLS估计一致

    -   假设3非完全共线性

    -   假设4外生性假设：解释变量均是外生的，保证解释变量和误差项不相关

-   保证OLS BLUE的假设

    -   假设1~4

    -   假设5同方差性假设：样本估计的方差是条件方差，没有无条件方差。$Var(\hat{\beta}|X) =( X'X )^{-1}\sigma^2$
        > $$
        \begin{aligned}
        \hat{\beta} &= {(X'X)}^{-1}X'Y \\
        &= (X'X)^{-1}X'(X\beta + \varepsilon) \\    
        &= \beta + (X'X)^{-1}X'\varepsilon \\ \\
        Var(\hat{\beta}|X) &= Var[(X'X)^{-1}X'\varepsilon|X] \\
        &= E[(X'X)^{-1}X'\varepsilon\varepsilon'X(X'X)^{-1}|X] \\
        &= (X'X)^{-1}X'E(\varepsilon\varepsilon'|X)X(X'X)^{-1} \\
        &= (X'X)^{-1}\sigma^2
        \end{aligned}
        $$

### 参数估计
- 矩方法

### 残差分析
- 残差独立服从同一正态分布：$u \stackrel{iid}{\sim} N(0,\sigma^2)$
    - 小样本下需要检验是否服从正态分布
    - 大样本下基本会近似服从正态分布，只需要检验是否独立同方差

- 残差图：$u-\hat{Y}$，以残差为纵坐标，其他的量（一般为拟合值）为横坐标的散点图。
    - 误差随着横坐标的增加而增加
    - 误差随着横坐标的增加而减少
    - 误差中间大，两端小
    - 误差规律变动：回归函数可能非线性，或者误差相关或者漏掉重要的自变量。可适当增加自变量的二次项或者交叉项，具体问题具体分析。

- 残差图中显示误差方差不相等(方差非齐性)：可以对变量做适当的变换，使得变换后的相应变量具有近似相等的方差(方差齐性)。最著名的方法是Box-Cox变换。


### 推断
- 显著性推断
    - F检验
    - t检验
- 解释能力评价
    - 调整R2

## 常见问题

### 奇异值问题

-   产生的原因

    -   数据采集错误；

    -   可能是上帝疯狂了几次，奇异值中可能包含了重要的信息。

-   带来的问题

    -   会导致模型的估计不稳定：删除少数非奇异值，对估计的影响不大，而删除几个奇异值，则会显著地改变结果；如何定义奇异值，也可以用这个是否显著改变估计结果来判断。

-   处理

    -   是否处理：依赖于产生奇异值的原因

        -   数据错误：应该处理。

        -   上帝无意的疯狂：属于小概率事件，应该处理，因为计量经济学是看平均；

        -   上帝有意的疯狂：需要进一步分析奇异值的原因。实际上，研究人员一般不清楚奇异值产生的原因，而在金融领域，一般认为应该进行处理。

    -   处理方法

        -   删除；

        -   winsorize，即把大（小）于某一阀值的观测值改为等于阀值。

### 多重共线性

-   产生原因

    -   样本量相对待估参数量太少

    -   "虚拟变量陷阱"的错误

    -   多重交叉变量

-   多重共线性显然是样本的问题，而不是总体的问题

    -   参数不可估计（完全共线性时）

    -   不影响无偏性，但影响估计精度

-   多重共线性的表象

    -   几个参数的F检验很显著，但单个参数的t检验不显著

    -   估计非常不稳健，对样本的微小变化变得高度敏感

    -   参数估计的符号与直观相反

    -   Correlation matrix of regressors, >0.75 (say)

-   Formal test: VIF

    -   方差为$\sigma^2/(SST_j*(1-R^2))$

    -   $VIF=1/(1-R^2)$

-   处理

    -   增大样本

    -   删除共线性的变量

### 异方差问题

-   原因：主要是模型设置问题

    -   比如正确的模型应该是二次型，但错误地设为线性

    -   比如缺失关键控制变量

    -   同时可能有内生问题，也可能没有

    -   最可能产生的情况：在横截面数据中，与规模有关的被解释变量，特别是以货币为单位的变量，比如R&D支出、投资等。大的y往往有大的拟合误差

-   影响

    -   没有方差的正确估计，从而不能做假设检验

    -   但估计本身还是无偏的和一致的

    -   不是BLUE的

-   Testing for heteroskedasticity

    -   Detecting Heteroscedasticity (I)

        -   Graphical method --good starting point

        -   Plot the squared value of estimated error term with explanatory variables or fitted dependent value

        -   Any systematic pattern suggests heteroscedasticity

    -   Detecting Heteroscedasticity (II): statistical test

        -   method

        ![](./media/image1.png)

    -   White test

        ![](./media/image2.png)
        Or
        ![](./media/image3.png)

    -   BP test

-   处理

    -   在同方差的情况下$\sigma_i^2 = \sigma^2$，我们可以估计$\sigma^2$，在异方差的情况下，不可能估计$\sigma_i^2$，OLS下可以估计β的方差：

        ![](./media/image4.png)

    -   大多数情况下，方差的稳健估计会比标准的估计大些，Robust estimate of variance: multivariate case
        
        ![](./media/image5.png)
        heteroskedasticity-robust t statistic.
        heteroskedasticity-robust F test.

    -   Generalized Least Square Estimation

    -   Case I: The heteroskedasticity is known up to a multiplicative constant

        ![](./media/image6.png)

    -   Case II: The Heteroskedasticity Function Is Unknown

        -   Feasible GLS

        -   First guess the heteroskedasticity function form and estimate it

            ![](./media/image7.png)
            ![](./media/image8.png)
            ![](./media/image9.png)

    -   Special case for FGLS

        ![](./media/image10.png)

    -   GLS is BLUE，How about FGLS? Is FGLS consistent?

-   FGLS or OLS with robust variance estimator?

    -   the FGLS estimator is consistent and asymptotically more efficient than OLS, but OLS is unbiased FGLS estimator is biased.

        -   For large sample size, FGLS is often better

        -   For small sample size, it is not clear which one is better

### 内生问题
- [内生问题根源](https://blog.csdn.net/celine0227/article/details/120770535)：致使自变量和误差项相关的因素
    - 双向因果：Y、X互为因果
    - 样本选择偏差：样本选择不随机。Hansen在《ECONOMETRIS (V2021)》第27章第9小节给出了推导，并且还介绍了一种流行的解决方法一一Heckman两步法。
    - 自选择偏差：解释变量选择不随机，即可能存在其他因素影响解释变量，这些无法观测或遗漏的因素若被归入干扰项，造成内生。
    - 缺失关键控制变量：X1同时影响X和Y，需要控制X1——也就是对X1进行分层，才能判断X对Y的因果效应；若要判断X1对Y的因果效应，则不能控制X——也就是不能对X分层，因为X只是X1影响Y的一条路径，并不代表X1对Y的全部影响；否则会导致辛普森悖论。
    - 观测误差
        - 如果误差发生在被解释变量上，一般没问题，误差可以归入模型误差
        - 如果误差发生在解释变量上，这时就有问题。看下面一般情况：
            ![](./media/image11.png)
            ![](./media/image12.png)

- 影响
    - 有偏
    - 不一致
    - 对预测来说，没有问题：
        - $Y = X\beta + \varepsilon，E( \varepsilon | X) \neq 0$
        - 可以假设$\varepsilon = Xb + \mu$
        - 所以Y对X的回归等价于$Y = X\beta + Xb + \mu = X(b + \beta) + \mu$
        - 估计出$b+\beta$，有偏，但预测反而更好
        - $\hat{Y} = E( Y | X = X_0) = X_0\beta + E( \varepsilon | X = X_0 )=X_{0}(\beta + b)$

- 处理
    - 工具变量法
    - FE
    - PSM

### 时间序列里的问题

-   违背独立随机抽样：Durbin-Watson Test，D-W statistic symmetrically distributed around 2, if it is far from 2, there is autocorrelation.没有DW统计量的分布，但知道DL<DW<DU, DW与DL（DU）的误差很小，并且知道DL和DU的分布。

    ![](./media/image13.png)

    -   影响：无偏的、一致的？、not BLUE

    -   处理：

        -   As in heterskedasticity, two approaches
            > -   Correlation-robust variance estimator
            > -   Correct it while do estimation: FGLS
            > > -   若已经知道相关模式，则直接进行GLS不需要FGLS了
            > > -   若不知道相关模式，则用FGLS：先估计相关模式+再进行GLS

    -   FGLS vs. OLS with robust variance estimator

    -   FGLS is not BLUE

    -   FGLS is asymptotically more efficient than the OLS estimator when the AR(1) model for serial correlation holds (and the explanatory variables are strictly exogenous).

    -   these assumptions are stronger than the requirement for OLS to be consistent.

    -   In fact, it can be shown that the weakest assumption that must hold for FGLS to be consistent, in addition to comtemporary exogenous (required for OLS)，is that the sum of $x_{t+1}$ and $x_{t-1}$ is uncorrelated with $u_t$:

-   确定性趋势模型能否可以用OLS估计

    -   解释变量不再是随机的，而是确定的时间，它本质上是缺少关键控制变量问题

    -   经典假设讨论的其实是更广的问题，确定性的变量可以看做退化的随机变量，因此经典假设没有问题

    -   只要模型是正确设定的，OLS就可以用

    -   对这些确定性趋势数据，有可能的伪回归问题，而更好的处理方法是首先去趋势，再做OLS，至少这样的好处在于R2有意义

-   面板回归

    -   FE：面板数据的优势：减少由于缺少关键控制变量导致的内生问题。固定效应模型可以解决未知个体特征问题，这导致了解释变量x中不能有不随时间变化的因素。即估计不出那些不随时间变化的因素对y的影响。

        -   从技术的角度看，这里不随时间变化的因素变量与个体特征变量完全共线性.

        -   从经济学的角度看，个体特征变量不随时间变化，它包括了所有的不随时间变化的因素，因此没法区分它们。

    -   RE：

        -   如果ui 与 Xit 之间不相关，并且对y的拟合优度不是我们的关注度，而beta的估计与检验是我们的关注度，这时估计FE那么多的虚拟变量的系数显然不是最优的。

        -   模型误差的目的是为了那些没法包括进来的因素（或结构），或者不想包括进来的因素，我们可以把这些ui归入模型误差，而用GLS来估计模型会更有效率，毕竟我们对ui不感兴趣。

        -   这时我们要假设ui 是服从一个均值为零随机变量： ui ~ IID(0, σ2u)。但对一个具体的个体观测值， ui 会有一个具体的实现，并且保证组内不变。这样的模型称作Random effect。但是，如果 ui and Xit 相关，这个模型会有内生问题.

        -   RE模型满足线性回归模型经典假设的前四条，可以用OLS估计，但有误差系列相关的问题：因此需要用RE的FGLS估计。

    -   选择过程

        -   FE or RE：Hausman 检验，H0：RE。

        -   FGLS（RE） or OLS：BP test （Breusch & Pagan， 1980），H0：没有组内系列相关，用pooled OLS。

    -   FE VS RE VS OLS

        -   Fixed effect, the most general model: Allow Ui; Allow possible correlation between xi and Ui

        -   Random effect: Allow Ui, but no correlation between xi and Ui; Can be treated as random variable with zero mean

        -   Pooled cross-sectional model, the most restricted model: No Ui

        -   从模型的要求看，RE处在FE和OLS之间

    -   其他问题

        -   FE不能估计那些不随时间变化的因素对y的影响，如果这些不随时间变化的因素正好是我们的目标，这时FE就有问题，即完全共线性问题。

        -   甚至有时我们感兴趣的变量在不同时间有变化，但组内变化非常小，这时FE估计有多重共线性问题。

## 面板模型

### 面板数据

相对于一维的截面数据和时间序列数据进行经济分析而言，面板数据有很多优点。(1)由于观测值的增多，可以增加自由度并减少了解释变量间的共线性，提高了估计量的抽样精度。(2)面板数据建模比单截面数据建模可以获得更多的动态信息，可以构建并检验更复杂的行为模型。(3)面板数据可以识别、衡量单使用一维数据模型所不能观测和估计的影响，可以从多方面对同一经济现象进行更加全面解释。

-   二维面板数据

    -   平衡面板数据

    -   非平衡面板数据：某些公司i在某些年份t没有观测值

-   广义的面板数据

    -   $x_{i,j}，i = 1,2,\ldots,n, j = 1,2, \ldots, m$。比如i为公司系列，j为分析师系列，$x_{i,j}$为j分析师为公司i做的EPS预测报告

    -   广义面板数据与严格的面板数据，在计量经济学上没有差别

-   高维面板数据

    -   $x_{i,j,t}，i = 1,2,\ldots,n, j = 1,2, \ldots, m, t = 1,2, \ldots, T$。比如i为公司系列，j为分析师系列，t为时间系列，$ x_{i,j,t}$为j分析师为公司i做的第t年的EPS预测报告

-   伪面板数据（类聚数据）

    -   $x_{i,j}，i = 1,2,\ldots,n, j = 1,2, \ldots, m$。比如i为公司系列，j为公告系列，$x_{i,j}$为公司i的第j次公告。与前面的核心差别在于j不是一个指标，而是一个观察值排序，没有实际含义。本质上是混同横截面数据

### 面板模型

- 面板数据模型的选择通常有三种形式：

    -   一种是混合估计模型（Pooled Regression Model）。如果从时间上看，不同个体之间不存在显著性差异；从截面上看，不同截面之间也不存在显著性差异，那么就可以直接把面板数据混合在一起用普通最小二乘法（OLS）估计参数。

    -   一种是固定效应模型（Fixed Effects Regression Model），包含个体固定效应模型、时刻固定效应模型和个体时刻固定效应模型三种。如果对于不同的截面或不同的时间序列，模型的截距不同，则可以采用在模型中添加虚拟变量的方法估计回归参数。

    -   一种是随机效应模型（Random Effects Regression Model）。如果固定效应模型中的截距项包括了截面随机误差项和时间随机误差项的平均效应，并且这两个随机误差项都服从正态分布，则固定效应模型就变成了随机效应模型。

    ![C:\\Users\\ADMINI\~1.SC-\\AppData\\Local\\Temp\\1555169449(1).png](./media/image14.png)
    ![C:\\Users\\ADMINI\~1.SC-\\AppData\\Local\\Temp\\1555169493(1).png](./media/image15.png)

-   拟合优度：Panel模型中有三个R2的定义，它们反映的都是x对y的解释力度，但具体计算上有差别，SAS报告的是within effect的R2。

    -   Overall R2

    -   Between effect R2

    -   Within effect R2

    -   固定效应模型的系数估计是within effect模型的，所以，固定效应模型的R2中最相关的是within effect R2

    -   Overall R2表示x在总体上对y的解释力度（除开个体ui）

    -   Between effect R2 与 within effect R2的对比告诉我们x在总体上对y的解释主要来自组间变化还是组内变化

### 面板模型回归步骤

步骤一分析数据的平稳性（单位根检验）：避免伪回归。

步骤二协整检验或模型修正：协整检验是考察变量间长期均衡关系的方法，通过了协整检验，说明变量之间存在着长期稳定的均衡关系，其方程回归残差是平稳的。因此可以在此基础上直接对原方程进行回归，此时的回归结果是较精确的。

或许还想进一步对面板数据做格兰杰因果检验（因果检验的前提是变量协整）。但如果变量之间不是协整（即非同阶单整）的话，是不能进行格兰杰因果检验的，不过此时可以先对数据进行处理。引用张晓峒的原话，"如果y和x不同阶，不能做格兰杰因果检验，但可通过差分序列或其他处理得到同阶单整序列，并且要看它们此时有无经济意义。"

步骤三：面板模型的选择与回归

### Fama-MacBeth回归

-   Fama-MacBeth回归：另一种处理面板数据的方法，即先在每个时间点做横截面回归，再把所有时间上的回归估计结果计算平均值并简单t检验。这样的处理方法，不但能处理面板数据，还能处理伪面板数据(混同横截面数据)。

    -   完全控制了时间固定效应

    -   可能部分解决了X与个体效应直接的相关性

    -   没有考虑RE中的组内误差相关性，不像前面Hausman & Taylor 1981的IV方法

## 时间序列模型

### Stationarity——平稳的时间序列才能基于历史序列预测未来

-   Weak stationary

    ![](./media/image16.png)

-   Strong stationary

    ![](./media/image17.png)

-   序列平稳性检验

    -   Dickey-Fuller检验

        > 检验带有截距项的一阶自回归模型 $Y_t= a_0+ρY_{t-1}+e_t$中的参数ρ是否小于1，H0：ρ =1，意味不平稳；H1：ρ <1。等价于检验它的变换形式$Y_t-Y_{t-1}=a_0+ (ρ-1)Y_{t-1}+e_t，即 ∆Y_t=a_0+δY_{t-1}+e_t $中的参数δ是否小于0

    -   ADF（Augment Dickey-Fuller ）检验

        ![](./media/image18.png)
        检验的假设都是针对H1: δ<0，检验H0：δ=0，即存在一单位根。

### Identifying ARMA model

$$y_t = \alpha + \beta_1y_{t-1} + \cdots + \beta_py_{t-p} + \varepsilon_t + \theta_1\varepsilon_{t-1} + \cdots + \theta_q\varepsilon_{t-q}$$

-   讨论这个模型有以下几个理由：AR（自回归）和MA（移动平均）

    -   帮助了解时间系列模型及数据的平稳性问题

    -   帮助了解时间系列模型的参数估计，模型选择及预测

    -   本身是一个预测模型，特别是用于季节性问题

    -   是随机波动率模型（GARCH）的基础

    -   是多元线性时间系列模型（VAR）的基础

-   阶数确定：ACF，比较自相关系数与偏自相关系数，可以看见是什么控制了更近的历史

    -   原则1：在大样本时，BIC比AIC更准确些，而小样本时，AIC比BIC准确程度高些

        -   Akaike information Criterion:

            > $AIC(p)= -\{2/T (max log-likelihood )- 2/T (No. parameters)\}$
            The first part measures the lack of fit and the second part penalizes the complexity of the model. Prefer smaller AIC model.

        -   Bayesian information criterion (or SBC):

            > $BIC(p)= -2/T (max log-likelihood )+ Log(T)/T (No. parameters)$
            Similar to AIC，BIC penalize more on the complexity of model than AIC，所以BIC偏好BIC更小的模型。

    -   原则2：Model checking based on forecasting

    -   SAS实操：minc命令输出所有自相关延迟数小于设定值的ARMA模型的BIC的信息量，并指出其中信息量最小的模型阶数

### GARCH

-   横截面模型中，(条件)异方差的处理方法：GLS

    -   $y_i = \alpha + \beta x_i + \varepsilon_i$

    -   $\varepsilon_i = \sigma_i\mu_i$

    -   $\ln\sigma_i = a_0 + a_1x_i$

-   GARCH的基本思路：直接对条件异方差进行模型化；与GLS不同的是，这里方差不是直接可观察变量的函数，而是滞后的拟合误差的函数

-   一种导致不收敛的原因是outliers的存在

    -   简单地去掉

    -   如果不能去掉outlier，如何解决模型的收敛问题（包括其他不能收敛的情况）

        -   改变参数估计的初始值

        -   改变最大化似然函数的数值方法

        -   改变模型，用简单些的模型

-   Volatility estimate and forecast in GARCH

    -   Recursive

    -   Depends on initial condition

        -   The error term at time 0 is assumed to be 0 or a to-be-estimated parameter

        -   the volatility at time 0 is assumed to be sample variance, or long-term variance, or a to-be-estimated parameter

-   数据选择问题

    -   一般来说，大多金融市场的GARCH模型都是用日度或高频数据，很少有用月度或更低频的数据。这是因为低频数据中的GARCH effect比较弱。

    -   做GARCH模型，用多长时间的数据？一般原则是：应该用几年（日度数据）的数据，样本大到使得当进行样本窗口滚动前移时，参数估计相对稳定（肯定是越多越稳定），但又没有多到包括直观认为以前没有影响的"outliers"。

-   Comments on GARCH

    -   Advantages

        -   Simplicity

        -   Generates volatility clustering

        -   Heavy tails (high kurtosis)

    -   Weaknesses

        -   Provides no explanation, a pure statistical model

        -   Not sufficiently adaptive in prediction

        -   Symmetric btw positive & negative prior returns

        -   Restrictive on parameters

-   Other GARCH models：GARCH, EGARCH or IGARCH, which one to use?

    -   AIC/BIC要考虑

    -   还要考虑是否有非对称效应存在，如有较强的非对称效应，要考虑用EGARCH

### VAR

-   ARMA是一个有力的预测模型，但是VAR：

    -   同时利用x和y，能获得更好的预测效果。

        -   比如学生数量及结构数据对培训市场的预测作用

    -   理解几个变量的动态关系。

        -   货币政策放松，要几个月后，CPI、就业才会有影响？

        -   现货价格与期货价格，谁影响谁？

        -   横截面回归模型不能解决这类问题。

-   Building a VAR model：同一元模型，要利用VAR模型进行分析预测，首先要从数据中得出一个模型

    -   Three steps

        -   Order selection

        -   Model estimation

        -   Model checking

    -   Because order selection is usually based on estimated model, so we discuss estimation first

    -   Estimation:

        -   One-by-one if no concurrent dependence：OLS or MLE

        -   Jointly if there is concurrent dependence：MLE (similar to univariate AR)

    -   Order selection

        -   Method I: a stepwise Chi-2 test

        -   Method II: use AIC , BIC, or others

    -   Model checking

        -   similar to the univariate case

        -   The predictability test (Q test) of the residual vectors

        -   SAS does it in the estimation procedure

    -   Forecasting: similar to the univariate case

    -   VAR预测经常比ARMA好，但有时不一定：这是由于ARMA模型可以有很复杂的结构，而VAR不能太复杂

-   Pros. and Cons. of VAR modeling

    -   VARs are very popular because:

        -   Easy to implement and estimate

        -   allow the data to talk about themselves (almost) without any binding constraints imposed by the theory

        -   often lead to better results than theory-based systems of simultaneous equations

        > the true relations among economic variables are usually unknown, thus dealing with their lags might overcome the misspecification error problem

    -   Cons:

        -   So many coefficients! n vars, k lags → n + k*n^2：由于这个原因，我们一般先做单变量的季节调整，VAR就可以简单很多

        -   no theory to choose appropriate variables
    
- VAR使用场景

    - 预测

    - 脉冲分析

        -   在时间t时，$y_t$的值会比预期的高一个单位，或者说在时间t时$y_t$会受到一个单位的正向冲击，那预期在时间t+s时，$y_{t + s}$会比原来的预期的差别为$d_{s}，d_{s}$作为s的函数，被称作脉冲反应函数

            > $$d_s = \frac{dE(y_{t + s}|F_t)}{dy_t}$$

        -   VAR(p)比较复杂，需要用VMA形式。

        -   Variance decompositions is check how does the variance of forecast error for future y depend on the variance of current x

            ![](./media/image19.png)
            ![](./media/image20.png)
            ![](./media/image21.png)

    - Granger Causality

        -   Granger因果关系是一种定性讨论两个系列的关系的方法

        -   多数情况下，因在前，果在后：但如何判断谁在前，谁在后？

            > 都只动一次的情况简单

            > 如果都在不断的运动中？
            > > futures market and the 
            > > underlying market:谁先动？谁后动？A-H market？

            > 如何判断谁先动？
            > > x能够预测y，x先动
            > > 但要控制y的过去！ Given the past information of y, the past information of x may not provide any help to predict y.
            > > Granger Causality 中的 close to close,open to open.

    -   panel data VAR model：对Granger测试加以修改、扩充，将可能的其他变数纳入测试，扩充版可以产生更有效的估计结果。

    -   panel data GARCH model：将其他变量纳入GARCH

    -   panel data VAR+GARCH model?

    -   一个信息对市场的影响，不仅依赖于信息本身，还依赖于信息的受众与信息的发布者之间的信任关系。

## 事件研究

-   事件研究法是研究某一类事件对市场的影响

-   事件研究法的基本步骤

    -   事件的定义

        -   事件要是同一类的，特别是应该考虑市场反应的方向。比如，M&A研究中，并购方与被并购方的反应可能会有不一样，故应该只看并购方（或被并购方）。分析师报告，有调高的，有调低的，应该分开来。

        -   事件相对于股票市场价格的变化是外生的：是事件影响股价，还是股价触发事件？

        -   For endogenous event, can we do event study? yes, but the explanation is different. The result shows correlation, not causality.

    -   事件样本准备

    -   估计正常与异常收益率

    -   Statistical test and/or regression analysis

        -   t-检验，是通过样本均值除样本标准差（调整样本规模）进行。这个公式要求观测值不相关，这里的观测值是各个事件的异常收益，因此要求各个事件不相关、计算AR的过程不相关！

        -   因此，事件在时间上要分散，要不然，异常回报之间存在高度的相关性。

-   宏观事件的问题：央行调整利率对个股的市场影响？

    -   变化，不是归因分析

    -   DID

-   事件发生时间大量重叠问题

    -   What if events happens in the consecutive days？

    -   对相关的AR情况，有两种处理方法

        -   Bootstrapping

        -   pseudo-portfolio

-   除了t-检验，还有基于回归的方法

    -   考察那些因素影响异常收益的大小

    -   但一般是先做t-检验

## 其他线性模型
- Lasso回归：一种既进行变量选择又进行正则化的方法，以提高其生成的统计模型的预测精度和可解释性。Lasso虽然是有偏估计，但是在引入一定的偏差的同时，可能可以大量降低估计的方差，从而降低整体的MSE。Lasso的优点不言而喻：如果我们拥有的样本信息是有限的，那么我们想要用有限的信息去估计过多的系数，此时信息很可能会出现不够用的情况，所以筛选变量提高估计效果十分必要。
    - 超参$\lambda$选取准则：
        - CV（Cross Validation）：可以选择平均误差最小的那个lambda，也可以选择平均误差在一个标准差以内的最大的lambda。
        - AIC, BIC等：当存在真模型的假设下，常常选取BIC准则。
    - 求解：LARS算法
- 岭回归
- 弹性网络回归
- 偏最小二乘法回归：一种统计学方法，与主成分回归有关系，但不是寻找响应和独立变量之间最小方差的超平面，而是通过投影预测变量和观测变量到一个新空间来寻找一个线性回归模型。
- 分位数回归：是统计和计量经济学中使用的一种回归分析。而最小二乘法估计条件均值跨预测变量的值的响应变量的，位数回归估计条件中值(或其它位数的响应可变的)。分位数回归是在不满足线性回归条件时使用的线性回归的扩展。
