---
marp: true
theme: default
size: 4:3
backgroundImage: url('../../_res/xq.png')
header: Marp使用：[第一节>](#1-第一节)[第二节>](#2-第二节) <hr>
footer: Copyright © 2024 XQ ![icon](../../_res/xq_icon.png)
paginate: true
style: |
  section {
    background-color: ;
    color: ;
    font-size: 0.6cm;
    text-align: left;
    font-family: KaiTi
  }
  h1{
    font-size: 1.2cm;
  }
  h2{
    font-size: 1cm;
  }
  h3{
    font-size: 0.8cm;
  }
---

<style scoped>
h1 {
    color: lightskyblue;
    font-size: 2cm;
    text-align: center;
}
h2 {
    font-size: 1cm;
    text-align: center;
}
</style>
<!-- _paginate: skip -->
<!-- _header: '' -->
<!-- _footer: '' -->

## ![w:100px, h:100px center](../../_res/xq.png)

# Marp使用
## ——使用教程
__目录__
[第一节>](#1-第一节)
[第二节>](#2-第二节)
页码跳过本页：`<!-- _paginate: skip -->`
自适应标题：`# <!-- fit --> 自适应标题`
更多参考：[01](https://marpit.marp.app/directives)、[02](https://github.com/favourhong/Awesome-Marp/blob/main/README.md)、[03](https://www.jianshu.com/p/7702cddafca0)

---

# 1 第一节
## 1.1 通过在文件头部的 YAML 命令区输入命令键值对
## 1.2 通过类似 HTML 备注的样式 <!-- directive: value --> 
该命令默认对当前与其后所有的幻灯片生效，可在命令前加一个 $ 使其针对整个文档有效，或在前面加一个下划线 _ 使其仅对当前一张幻灯片生效。

---

# 2 第二节

|测试|效果|
|-|-|
|`**Bold**`|**Bold**|
|`_Italic_`|_Italic_|
|`$x=y$`|$x=y$|
|本页背景`<!-- _backgroundColor: orange -->`|<!-- _backgroundColor: orange -->|
|背景图片|统一命令无法设置opacity，只能单个背景图片里分别设置|
|目录|手动引用|
|输出PPT|点击marp图标，选择export: PPT为图片无法编辑，建议convert output PDF to PPTX by Adobe Acrobat.|

---

# 3 第三节
![bg left:33%](../../_res/xq.png)
- 背景测试1

---

# 4 
![bg opacity:.2](../../_res/xq.png)
![bg](../../_res/xq.png)
![bg](../../_res/xq.png)
- 背景测试2

---

# 5
![bg opacity:.2 vertical](../../_res/xq.png)
![bg opacity:.2](../../_res/xq.png)
![bg opacity:.2](../../_res/xq.png)
- 背景测试3

---

# 6 html分栏
<style>
.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container">

<div class="col">
Column 1 Content
</div>

<div class="col">
Column 2 Content
</div>

<div class="col">
Column 3 Content
</div>
</div>

---

# 7 表格分栏

|图片|![](/_res/xq.png)|
|-|-|
|||