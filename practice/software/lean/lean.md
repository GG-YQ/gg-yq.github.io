# 简介
Lean 是基于一个被称为构造演算（Calculus of Constructions）的依值类型论的版本，它拥有一个可数的非累积性宇宙（non-cumulative universe）的层次结构以及归纳类型（Inductive type）。
- [依值类型论（Dependent type theory）](https://www.bananaspace.org/wiki/%E4%BE%9D%E5%80%BC%E7%B1%BB%E5%9E%8B%E8%AE%BA)：类型可以依赖于参数
    - 类型：类似于集合论中的集合，类型直接通过规则来定义。大部分数学都能以类型论为基础而重新表述。
    - 值：类型的实例，类似集合的元素。
    - 语境：在类型论中, 语境大致表示之前做的构造。
    - 宇宙：记作$\mu$，来代表类型的类型。不能存在以自己为类型的类型，否则导致 Girard 悖论。

