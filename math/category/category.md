## 逻辑
### 基本概念
- 哥德尔不完备定理：对给定公理体系有限的系统
    - 完备性：任何形式系统都不能完全刻画数学理论，总有某些问题从形式系统的公理出发不能解答。
    - 自洽性：任一自洽的形式系统均无法证明其本身的自洽性
    - 可决性：否定自指无法判定结果(例如物理世界中一般体系下谱隙的有无不可判定，即使完美地描述了2个粒子之间的微观相互作用，通常也不足以推断宏观性质，会面临图灵机停机问题)
    > 命题真伪_GYQ：可能命题真实发生时为真命题，可能命题未发生或不可能命题为否命题。自洽性、完备性、可决性？有限公理不能描述全部现实，那么给定有限现实，最小公里体系是什么？
- 类：令Wi为一超穷基数域，f为定义在Wi上的一个性质，那么所有符合f的对象u构成一个“类”。类的问题：
    - 是不是C中的所有对象u都具有性质f？特别是，C本身具有性质f吗？（同一性判定）
    - 是不是C中的所有对象u，都有f(u)或者﹁f(u)成立吗？（完备性判定）
    - 是不是C中的所有对象u，都有f(u)和﹁f(u)不能同时成立吗？（一致性判定）
- 集合
    - 基本符号
        - 定义："=:"，如果一个表达式或一系列操作无歧义地确定了一个数学对象, 与一切辅助资料的选取无关, 则称该对象为 “良好定义”或 “确切定义” 的, 简称良定.
        - 集合内操作：$属于\in、等价\sim、商集S/\sim$
            > $等价：\forall n\ge 1, 集合X上的n元关系R是X^n=X\times X \cdots \times X的一个子集。例如二元关系xRy表示(x,y)\in R。满足以下性质的 (二元) 关系 ∼ 称作等价关系:$ 
            > > $反身性 x ∼ x \\
            对称性 x ∼ y \Rarr y ∼ x \\
            传递性 (x ∼ y) ∧ (y ∼ z) \Rarr (x ∼ z)$
            
            > $[x]:= \{y\in X:y\sim x\} \\
            X/\sim:=\{[x]:x\in X\}$
        - 集合间操作：$包含\sub、交\cap、并\cup、差\setminus、积\times、积\prod、无交并\sqcup、元素个数或者基数|S|$
        - 映射：$集合间映射f:A\rarr B、元素间映射f:a\mapsto b、单射\hookrightarrow、满射\twoheadrightarrow、双射\xleftrightarrow{1:1}、同构\simeq、f的像im(f)、f的原像f^{-1}(b)$、集合S到自身的恒等映射$\mathrm{id}_S$
        - $X^Y:=\{f:Y\xrightarrow{f} X\}$
    - 序结构
        -  偏序集意指资料 (P, ≤), 其中 P 是集合而 ≤ 是 P 上的二元关系 (偏序), 满足于。(仅满足反身性与传递性的结构称为预序集)
            > $反身性：\forall x\in P,x\le x \\
            传递性：(x\le y)\land(y\le z)\Rarr x\le z \\
            反称性：(x\le y)\land(y\le x)\Rarr x=y$
        - 确界：对于偏序集 P, 根据反称性, 其子集 P' 的上确界或下确界若存在则是唯一的, 分别记为 sup P' 和 inf P'.
        - 偏序集 P, Q 之间的同构$\phi: 其中\phi:P\rarr Q是双射且\phi,\phi^{-1}皆保序$
        - 全序集：若偏序集 P 中的任一对元素 x, y 皆可比大小 (即: 或者 x ≤ y, 或者 y ≤ x),则称 P 为全序集. 全序集又称作线序集或链.
        - 良序集：每个全序集 P 的非空子集都有极小元.
        - 序数：如果一个集合 α 的每个元素都是 α 的子集 (换言之, α ⊂ P(α)), 则称 α 为传递的. 若传递集 α 对于 $x<y\xLeftrightarrow{定义}x\in y$ 成为良序集, 则称 α 为序数.
        - On：序数构成的类。
            > 对序数定义 β < α 当且仅当 β ∈ α, 则这定义了 On 上的一个全序, 而且对任意序数 α 都有 α = {β : β < α}.
            若 C 是一个由序数构成的类, C $\neq$ ∅, 则 inf C := $\cap$C 也是序数, 而且 inf C ∈ C; 我们有 α $\sqcup$ {α} = inf{β : β > α}.
            若 S 是一个由序数构成的集合, S $\neq$ ∅, 则 sup S := $\cup$ S 也是序数.
        - 后继：给定序数 α, 置 α + 1 := α $\sqcup$ {α} > α, 称为 α 的后继; 它是大于 α 的最小序数. 若α 不是任何序数的后继, 则不难看出 α = sup{β : β < α}, 这样的 α 称为极限序数.
        - 极限序数：若 α 不是任何序数的后继, 则不难看出 α = sup{β : β < α}, 这样的 α 称为极限序数. 约定空 sup 为 ∅ 使得 “零序数” ∅ 是极限序数.
    - 基数：描述集合大小的一种标杆
        - 等势：若两集合 X, Y 之间存在双射 φ : X → Y , 则称 X, Y 等势.
    - ZFC公理: ZFC处理的所有对象x, y等都为集合; 特别地, 集合的元素本身也是一个集合.
        - A.1 外延公理: 若两集合有相同元素, 则两者相等.
            > 空集 ∅ 的形式定义: $\{u\in X: u\neq u \}$, 其中 X 是任意集合, ∅ 无关 X 的选取, 前提是集合X确实存在. 
        - A.2 配对公理: 对任意 x, y, 存在集合 {x, y}, 其元素恰好是 x 与 y.
            > 有序对 (x, y) 的概念可用配对公理来实作: (x, y) := {{x}, {x, y}}, 由此定义积集 X × Y := {(x, y) : x ∈ X, y ∈ Y }.
        - A.3 分离公理模式: 设 P 为关于集合的一个性质, 并以 P(u) 表示集合 u 满足性质 P, 则对任意集合 X 存在集合 Y = {u ∈ X : P(u)}.
        - A.4 并集公理: 对任意集合 X, 存在相应的并集$\cup X:= \{u : ∃v ∈ X 使得 u ∈ v\}$. 公理中的 X 通常视作一族集合, $\cup X$也相应地写成$\cup_{v\in X}v$.
        - A.5 幂集公理: 对任意集合 X, 其子集构成一集合 P(X) := {u : u ⊂ X}.
        - A.6 无穷公理: 存在无穷集, $\exist x[(\empty\in x)\land \forall y\in x(y\cup\{y\}\in x)]$.
        - A.7 替换公理模式: 设 F 为以一个集合 X 为定义域的函数, 则存在集合 F(X) ={F(x) : x ∈ X}.
            > 分离和替换公理模式里的性质 P 和函数 F 并非集合论意义下的寻常定义, 故无循环论证之虞, 它们实际是由一阶逻辑的合式公式定义的: 以函数$x\mapsto y$为例, 这可以诠释为一阶逻辑中带有两个自由变元 x, y 的合式公式 ϕ, 适合于 ∀x ∃!y ϕ(x, y). 由于对每个 P 或 F 都产生一条相应的公理, 它们被称作公理模式.
        - A.8 正则公理: 任意非空集都含有一个对从属关系 ∈ 极小的元素.
            > 正则公理的一个重要推论是对于任意集合 x, 不存在无穷的从属链$x\owns x_1\owns x_2\owns\cdots$, 特别地$x\notin x$. 由之可建立集合的层垒谱系.
        - A.9 选择公理: 设集合 X 的每个元素皆非空, 则存在函数$g:X\rarr\cup X$使得∀x ∈ X, g(x) ∈ x (称作选择函数).
    - 宇宙-集合U: 对于集合 X, 若 X ∈ U 则称为 U-集; 若 X 和一个 U-集等势, 则称为 U-小集.这套概念的神髓在于在 U 内部可以实行大部分常见的数学操作而不涉及真类, 这就为棘手的集合论问题建起一道防火墙. 然而是否有充分多、充分大的宇宙可资调用则是另一个问题.
        - U的性质
            > U.1 u ∈ U ⇒ u ⊂ U, 即: U 是传递集;
            U.2 u, v ∈ U ⇒ {u, v} ∈ U;
            U.3 u ∈ U ⇒ P(u) ∈ U;
            U.4 若 I ∈ U, 一族集合 $\{u_i: i ∈ I\}$ 满足 ∀i, ui ∈ U, 则$\cup_{i∈I}u_i ∈ U$;
            U.5 $\Bbb{Z}_{≥0} ∈ U$, 换言之: ∅ ∈ U.
        - U的推论
            > u ⊂ v ∈ U ⇒ u ∈ U;
            $u ∈ U ⇒\cup u =\cup_{x∈u}x ∈ U$;
            u, v ∈ U =⇒ u × v ∈ U;
            若 I ∈ U, 一族集合 $\{u_i: i ∈ I\}$ 满足 ∀i, ui ∈ U, 则$\prod_{i∈I}u_i ∈ U$.
- 范畴：对象+对象间的态射. 序结构连同拓扑和代数结构一道组成了数学结构的三大母体.映射不保持运算，还要运算有何用？所以在研究带结构的集合的时候，当然要配套地把映射，单射，满射，双射通通换成同态，单同态，满同态和同构
    ```mermaid
    flowchart LR
        subgraph A[范畴A]
            direction TB
            X(对象X) --->|态射f|Y(对象Y)
            X --->|态射g|Z(对象Z)
        end
        subgraph B[范畴B]
            direction TB
            U(对象U) --->|态射h|V(对象V)
        end
        A --- F("函子F<br>F(X)→U<br>F(Y)→V<br>F(f):F(X)→F(Y)") --> B
        A --- G(函子G) -->B
        A --- H(函子H) -->B
        G -->|"自然变换η:<br>G→H"| H
    ```
    $$
    \begin{CD}
        F(x) @>F(f)>> F(y) \\
        @V\eta_x VV @V\eta_y VV \\
        G(x) @>G(f)>> G(y)
    \end{CD}
    $$
    - 范畴系C
        - 集合Ob(C), 其元素称作 C 的对象.
        - 集合 Mor(C), 其元素称作 C 的态射. 对于 X, Y ∈ Ob(C), 一般习惯记$Home_c(X,Y):=s^{-1}(X)t^{-1}(Y), $或简记为 Hom(X, Y), 称为 Hom-集, 其元素称为从 X 到 Y 的态射, 其中 s 和 t 分别给出态射的来源和目标.
        - 对每个对象 X 给定元素 $id_X ∈ Hom_C(X, X)$, 称为 X 到自身的恒等态射.
        - 一般也将 $f ∈ Hom_C(X, Y )$ 写作 f : X → Y 或 $X\xrightarrow{f} Y$. 对于态射 f : X → Y , 若存在 g : Y → X 使得 $fg = id_Y, gf = id_X$, 则称 f 是同构 (或称可逆, 写作 $f : X\xrightarrow{\sim} Y$), 而 g 称为 f 的逆, 从恒等态射的性质易见逆若存在则唯一. 从 X 到 Y 的同构集记为 $Isom_C(X, Y )$.
        - 记 $End_C(X) := Hom_C(X, X), Aut_C(X) := Isom_C(X, X)$, 分别称作 X 的自同态集和自同构集.
        - 若一个范畴 C 中的所有态射都可逆, 则称之为广群.
        - 反范畴 $C^{op}$
            > $Ob(C^{op}) = Ob(C)$
            对任意对象 X, Y , $Hom_{C^{op}}(X, Y ) := Hom_C(Y, X)$
            态射$ f∈ Hom_{C^{op}}(Y, Z) , g ∈ Hom_{C^{op}}(X, Y ) $在$C^{op}$中的合成$f◦^{op}g$定义为C中的反向合成g◦f
            恒等态射定义同C.
    - 函子
        - $一个函子F:C' → C, C', C为范畴. 从 C'到C和从(C')^{op}到C^{op}的函子是一回事. 为资区分, 对于函子F:C' → C, 反范畴间的相应函子记为 F^{op}: (C')^{op} → C^{op}.$
            > 1、 称 F 是本质满的, 若 C 中任一对象都同构于某个FX;
            2、 称F是忠实的, 若对所有 X, Y ∈ Ob(C') 映射 $Hom_{C'}(X, Y ) → Hom_C(FX, FY )$都是单射;
            3、 称 F 是全的, 如果上述映射对所有 X, Y ∈ Ob(C') 都是满射.
            *两种等价命题：F 是范畴等价$\Lrarr$F 是全忠实, 本质满函子
        - 等价：如果一对函子 $C_1{\xrightarrow{F}\atop \xleftarrow[G]{}} C_2$满足以下性质: 存在函子之间的同构$θ : FG\xrightarrow{\sim}id_{C_2}, ψ : GF\xrightarrow{\sim}id_{C_1}$, 则称 G 是 F 的拟逆函子, 并称 F 是范畴 C1 到 C2 的等价.
        - 如果进一步有 $FG = id_{C_2}, GF = id_{C_1}$, 则称 F 是范畴间的同构, 而 G 是 F 的逆.
        - 函子范畴：设 C1, C2 为 U-范畴, 定义函子范畴 Fct(C1, C2): 其对象是 C1 到C2 的函子, 任两个对象 F, G 间的态射是自然变换 θ : F → G; 态射 θ : F → G 与ψ : G → H 的合成是自然变换的纵合成 ψ ◦ θ : F → H.有时也把 Fct(C1, C2) 写作 $C_2^{C_1}$.
        - 自然变换：函子间的态射
        - 一个范畴 C 的中心定义为 $Z(C) := End(id_C)$ 
            > 中心是范畴是一种极有用的不变量, 其元素无非是一族自同态.
            中心 Z(C) 对二元运算 ◦ 总是交换的.
            范畴等价 F : C1 → C2 诱导中心的同构 Z(C1) ' Z(C2).
    - 子范畴：若C'对象、态射、态射合成都受C限制，则C'为C的子范畴。如果 $Hom_{C'} (X, Y ) = Hom_C(X, Y )$ 则称 C' 是全子范畴.
    - 逗号范畴：对于函子 $\mathcal{A}\xrightarrow{S}\mathcal{C}\xleftarrow{T}\mathcal{B}$, 定义逗号范畴 (S/T) 如下
        - 对象: 形如 $(A, B, f)$, 其中 $A ∈ Ob(\mathcal{A}), B ∈ Ob(\mathcal{B}), f : SA → T B$;
        - 态射: 从 (A, B, f) 到 (A' , B' , f' ) 的态射形如 (g, h), 其中 g : A → A' , h : B → B'分别是 $\mathcal{A, B}$ 中的态射
    - 注意
        - 范畴未必由搭建在集合上的结构组成;
        - 对于其他建基在集合上的范畴, 双射同态也未必可逆: 标准的反例是范畴 Top (对象 = Hausdorff 拓扑空间, 态射 = 连续映射), 其中的同构是拓扑空间的同胚, 然而连续的双射未必是同胚.
    - 范畴实例：群Grp、交换群Ab、R-模R-Mod
        - 同态集合：$\mathrm{Hom_{Grp}}(X,Y)$
        - 自同态$\mathrm{id}_X$对态射合成构成幺半群：End(X)
        - 可逆的自同态称为自同构：Aut(X)
        - 幺半范畴
- 
- 研究对象
    > (I) logic is a branch of mathematics; 
    (2) the goal of logic is to study mathematics itself. 
- 研究方法：
    > proof by induction & define by induction
### Propositional calculus
- basic notions
    > $set$: E、F

    > $f$: a map defined on a subset of E with values in F
    > > $dom(f)$: the domain of f
    $im(f)$: the image of f

    > $f \restriction A: A \subseteq E$, the restriction of f to A is the map from A into F. 

    > $f[A]$: The image of the map $f \restriction A$ is also called the direct image of A under f and is denoted by f[A].

    > $\overline{f} (A)$: $\overline{f}$ denotes the 'direct image' map, with any subset A of E, associates f[A]. 
    
    > $w$: Let E be a set, which we will call the alphabet. A word, w, on the alphabet E is a finite sequence of elements of E.

    > $lg[w]$: the length of the word

    > $\mathcal{W}(E)$: the set of words on E

    > $P=\{A_1,A_2,\dots A_n\}$: the finite set of propositional variables.

    > $\neg \land \lor \Rarr \Lrarr$: symbols for propositional connectives

    > $\mathcal{A}=P \cup \{\neg, \land, \lor, \Rarr, \Lrarr \} \cup \{(,) \}$: Certain finite sequences composed of propositional variables, symbols for propositional connectives, and parentheses will be called propositional formulas (or propositions). Propositional formulas are thus words formed with the alphabet $\mathcal{A}$.

- Definition the set $\mathcal{F}$ of propositional formulas constructed from P is the smallest subset of $\mathcal{W(A)}$ which
    - includes P; 
    - whenever it contains the word F, it also contains the word $\neg F$; 
    - whenever it contains the words F and G, it also contains the words: $(F \land G), (F \lor G), (F \Rarr G), (F \Lrarr G)$.
    > In other words, $\mathcal{F}$ is the smallest subset of W(A) which includes P and which is closed under the operations:
    $F \mapsto \neg F$
    $(F,G) \mapsto (F\land G)$
    $(F,G) \mapsto (F\lor G)$
    $(F,G) \mapsto (F\Rarr G)$
    $(F,G) \mapsto (F\Lrarr G)$

- $F=F[A_1,A_2,\dots,A_n]$: every $F \in \mathcal{F}$ has its variables among $A_1,A_2,\dots,A_n$

-  For any assignment of truth values $\delta \in \{0, 1\}^P$, there exists a unique map $\overline\delta: \mathcal{F} \Rarr \{0, 1\}$ which agrees with $\delta$ on P (i.e. it extends $\delta$) and which satisfies the following properties:
    > (1) for any formula F, 
    $\overline\delta(\neg F) = 1$ if and only if $\overline\delta(F) = 0$;
    (2) for all formulas F and G, 
    $\overline\delta(F \land G) = 1$ if and only if $\overline\delta(F) =\overline\delta(G) = 1$; 
    (3) for all formulas F and G, 
    $\overline\delta(F \lor G) = 0$ if and only if $\overline\delta(F) =\overline\delta(G) = 0$; 
    (4) for all formulas F and G, 
    $\overline\delta(F \Rarr G) = 0$ if and only if $\overline\delta(F) =1 \ and \ \overline\delta(G) = 0$; 
    (5) for all formulas F and G, 
    $\overline\delta(F \Lrarr G) = 1$ if and only if $\overline\delta(F) =\overline\delta(G)$. 
    > > On the two-element field $\mathbb{F}_2=\Z/2\Z$, (1)~(5)can be denoted by: 
    $\overline\delta(\neg F) = 1+\overline\delta(F)$;
    $\overline\delta(F \land G) =\overline\delta(F) \overline\delta(G)$; 
    $\overline\delta(F \lor G) =\overline\delta(F)+\overline\delta(G)+\overline\delta(F) \overline\delta(G)$; 
    $\overline\delta(F \Rarr G) =1+\overline\delta(F)+\overline\delta(F) \overline\delta(G)$; 
    $\overline\delta(F \Lrarr G) =1+\overline\delta(F)+\overline\delta(G)$; 
    
    > Recapitulate conditions above in tables which we call the truth tables for negation, for conjunction, for disjunction, for implication and for equivalence:   

    |$F$|$\neg F$||
    |---|---|---|
    |0|1||
    |1|0||
    |$F$|$G$|$(F \land G)$|
    |0|0|0|
    |0|1|0|
    |1|0|0|
    |1|1|1|
    |$F$|$G$|$(F \lor G)$|
    |0|0|0|
    |0|1|1|
    |1|0|1|
    |1|1|1|
    |$F$|$G$|$(F \Rarr G)$|
    |0|0|1|
    |0|1|1|
    |1|0|0|
    |1|1|1|
    |$F$|$G$|$(F \Lrarr G)$|
    |0|0|1|
    |0|1|0|
    |1|0|0|
    |1|1|1|
    
    关于$F\Rarr G$的真值：本身只是定义的基本运算，没有现实因果逻辑含义。之所以定义成这种形式，是考虑了当F是G的充分条件时，当F出现，Q一定出现 $(i.e. \ \overline{\delta}(F\Rarr G)=1 且 \overline{\delta}(F\Rarr\neg G)=0)$；当F不出现，G可出现，G可不出现，因为可能存在其他前提推出结论G $(i.e. \ \overline{\delta}(\neg F\Rarr G)=1 且 \overline{\delta}(\neg F\Rarr \neg G)=1)$。

- Satisfy: If F is a formula and $\delta$ is an assignment of truth values, we will say that F is satisfied by $\delta$, or that $\delta$ satisfies F, when $\overline{\delta}(F)=1$.

- Tautologies and logically equivalent formulas
    - $\vdash^*F$: F is a tautology. A tautology is a formula that assumes the value 1 under every assignment of truth values.
    - $F \sim G$: F is logically equivalent to G. Given two formulas F and G, F is logically equivalent to G ifand only if the formula $(F \Lrarr G)$ is a tautology.
        > Some tautologies(see Rene's book 1.2.3)
        (1) $((A\land A)\Lrarr A)$: idempotence of conjunction
        (2) $((A\lor A)\Lrarr A)$: idempotence of disjunction
        (3) $((A\land B)\Lrarr (B\land A))$: commutativity of conjunction
        (4) $((A\lor B)\Lrarr (B\lor A))$: commutativity of disjunction
        $\dots$

- cl(F): denotes the equivalence class of the formula F under the equivalence relation $\sim$. The number of equivalence classes for the relation $\sim$ on $\mathcal{F}$ is at most equal to the number of mappings from $\{0,1\}^n$ into $\{0,1\}$, which is to say $2^{2^n}$.

- $\delta_{\epsilon_1,\epsilon_2,\dots,\epsilon_n}$: denotes the distribution of truth values defined by $\delta_{\epsilon_1,\epsilon_2,\dots,\epsilon_n}(A_i) = \epsilon_i$ for each $i \in \{1, 2,\dots , n\}$, in which n-tuple $(\epsilon_1,\epsilon_2,\dots,\epsilon_n) \in \{0,1\}^n$.

- $\epsilon A$: denote the formula that is equal to A if $\epsilon=1$ and to $\neg A$ if $\epsilon=0$.

- $\Delta(F)=\{\delta \in \{0,1\}^P:\overline{\delta}(F)=1\}$: denote the set of distributions of truth values that satisfy F

- $\varphi_F(\epsilon_1,\epsilon_2,\dots,\epsilon_n)=\overline{\delta(\epsilon_1,\epsilon_2,\dots,\epsilon_n)}(F)$: map from $\{0,1\}^P \ into \ \{0,1\}$, the truth table of F.

- complete set of connectives: A set of connectives is called complete if it generates, under composition, the set of all propositional connectives. A complete set of connectives is called minimal when no proper subset is a complete set of connectives. The set $\{\neg,\land,\lor \}$ is a complete set but not a minimal, while $\{\neg,\land \}$ is a minimal complete set.

- Interpolation lemma: 
    - Let F and G be two formulas having no propositional variable in common. Thefollowing two properties are equivalent:
        > (1) Theformula $(F \Rarr G)$ is a tautology. 
        (2) At least one of the formulas $\neg$F or G is a tautology.
    - Let n be a non-zero integer, $A_1,A_2,\dots,A_n$ pairwise distinct propositional variables, and F and G two formulas that have (at most) the propositional variables $A_1,A_2,\dots,A_n$ in common. The following two properties are equivalent:
        > (1) Theformula $F \Rarr G$ is a tautology.  
        (2) There is at least one formula H, containing no propositional variables other than $A_1,A_2,\dots,A_n$, such that the formulas $(F \Rarr H)$ and $(H \Rarr G)$ are tautologies.
    - A corollary of the interpolation lemma, the definability theorem: Let $A,B,A_1,A_2,\dots,A_n$ be pairwise distinct propositional variables and $F=F[A,A_1,A_2,\dots,A_n]$ be aformula (whose variables are therefore among $A, A_1,A_2,\dots,A_n$). We assume that theformula $$((F[A,A_1,A_2,\dots,A_n] \land F[B,A_1,A_2,\dots,A_n])\Rarr (A \Lrarr B))$$ is a tautology. Then there exists a formula $G=G[A_1,A_2,\dots,A_n]$, whose only variables are among $A_1,A_2,\dots,A_n$ and is such that theformula $$(F[A,A_1,A_2,\dots,A_n]\Rarr (A \Lrarr G[A_1,A_2,\dots,A_n]))$$ is a tautology.

- The compactness theorem
    - Satisfaction of a set of formulas: Let $\mathcal{A}$ and $\mathcal{B}$ be two sets of formulas of the propositional calculus on the set of propositional variables P, let G be aformula and let $\delta$ be a distribution of truth values on P.
        > $\mathcal{A}$ is satisfied by $\delta$ (or $\delta$ satisfies $\mathcal{A}$) if and only if $\delta$ satisfies all the formulas belonging to $\mathcal{A}$.

        > $\mathcal{A}$ is satisfiable (or consistent, or non-contradictory) if and only if there exists at least one distribution of truth values that satisfies $\mathcal{A}$.

        > $\mathcal{A}$ is finitely satisfiable if and only if every finite subset of $\mathcal{A}$ is satisfiable. 

        > $\mathcal{A}$ is contradictory if and only if it is not satisfiable.

        > G is a consequence of $\mathcal{A}$ (which we denote by: $\mathcal{A}\vdash^*G$) if and only if every distribution of truth values that satisfies $\mathcal{A}$ satisfies G. (The notation for 'G is not a consequence of A' is: $\mathcal{A}\nvdash^*G$). 
        
        > $\mathcal{A}$ and $\mathcal{B}$ are equivalent if and only if every formula of $\mathcal{A}$ is a consequence of $\mathcal{B}$ and every formula of $\mathcal{B}$ is a consequence of $\mathcal{A}$.
    - For all sets offormulas $\mathcal{A}$ and $\mathcal{B}$, integers m and p >=1, and formulas $G,H,F_1,F_2,\dots,F_m$ and $G_1,G_2,\dots,G_p$, the following properties are verified:(see in Rene's book 1.5)
        > $\mathcal{A}\vdash^*G$ if and only if $\mathcal{A}\cup \{\neg G\}$ is contradictory.
        If $\mathcal{A}$ is satisfiable and if $\mathcal{B} \sube \mathcal{A}$, then $\mathcal{B}$ is satisfiable. 
        If $\mathcal{A}$ is satisfiable, then $\mathcal{A}$ is finitely satisfiable. 
        If $\mathcal{A}$ is contradictory and if $\mathcal{A} \sube \mathcal{B}$, then $\mathcal{B}$ is contradictory.
        ...
    - The compactness theorem for propositional calculus:
        > The compactness theorem, version 1: For any set $\mathcal{A}$ of formulas of the propositional calculus, $\mathcal{A}$ is satisfiable if and only if $\mathcal{A}$ is finitely satisfiable.
        
        > The compactness theorem, version 2: For any set $\mathcal{A}$ of formulas of the propositional calculus, $\mathcal{A}$ is contradictory if and only if at least one finite subset of $\mathcal{A}$ is contradictory.

        > The compactness theorem, version 3: For any set $\mathcal{A}$ of formulas of the propositional calculus and for any formula F, F is a consequence of $\mathcal{A}$ if and only if F is a consequence of at least one finite subset of $\mathcal{A}$.

### Boolean algebras

