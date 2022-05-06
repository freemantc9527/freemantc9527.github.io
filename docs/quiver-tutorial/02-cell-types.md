# 单元格类型

目前支持五种单元格类型:

1. 文本单元格：支持富文本编辑，图像和链接。
2. 代码单元格：使用 ACE 代码编辑器，语法高亮显示支持 120+ 语言、 20 + 主题、 支持自动缩进、 代码自动补全，功能多多。
3. Markdown 单元格：支持自定义 CSS，即时预览。
4. LaTeX 单元格： 使用 MathJax 来排版笔记中的数学公式。
5. 图表单元格：使用纯文本创建序列图和流程图。

## 文本单元格

This is a **text cell** with *some* simple* formatting*.

This is *an example* of a text cell with complex styles applied.

你可以使用工具栏按钮或键盘快捷方式更改文本格式。在"格式"菜单下可以找到所有格式设置选项和键盘快捷方式。

## 代码单元格

```js
// 这是一个代码单元格设置为 JavaScript 模式:
void hello()
{
    console.log("Hello World!");
}
```

```coffee
# 这是一个代码单元格设置为 CoffeeScript 模式:
hello = -> console.log 'Hello World!'
```

代码单元格支持 120 + 语言的语法高亮、 20 + 主题、 自动缩进，代码折叠，多个游标和选择、 代码自动补全、tab 触发，Vim/Emacs 键绑定等。在 Ace 代码编辑器的网站 [http://ace.c9.io](http://ace.c9.io) 上，你可以读到更多 Ace 代码编辑器的功能。

## Markdown 单元格

Markdown 单元格支持标准 Markdown 语法以及 GitHub Flavored Markdown (GFM)。

### 基本格式

```markdown
# 标题 1
## 标题 2
### 标题 3
#### 标题 4
##### 标题 5
###### 标题 6
```

---

*斜体*, **粗体**, ~~划除~~

`行内代码`

### 列表

1. 第一个有序的列表项
2. 另一个列表项
  * 无序的子列表
1. 实际数字不重要
  1. 有序的子列表
4. 另一个列表项

### 引用

> 和平不能靠武力; 它只可以通过理解来实现。

### 链接

[行内链接](https://www.google.com)
http://example.com


你可以创建链接到另一个笔记：(“笔记”菜单 -> 复制笔记链接 -> 粘贴)

[01 - Getting Started](quiver:///notes/D2A1CC36-CC97-4701-A895-EFC98EF47026)


### 表格

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

### GFM 任务列表

- [ ] a task list item
- [ ] list syntax required
- [ ] normal **formatting**, @mentions, #1234 refs
- [ ] incomplete
- [x] completed

### 行内 LaTeX 

您可以在 Markdown 单元格中使用行内 LaTeX，例如，$x^2$。

## LaTeX 单元格

使用 LaTeX 单元格可以很容易地排版数学公式。例如，

\begin{align}
  \nabla \times \vec{\mathbf{B}} -\, \frac1c\, \frac{\partial\vec{\mathbf{E}}}{\partial t} & = \frac{4\pi}{c}\vec{\mathbf{j}} \\
  \nabla \cdot \vec{\mathbf{E}} & = 4 \pi \rho \\
  \nabla \times \vec{\mathbf{E}}\, +\, \frac1c\, \frac{\partial\vec{\mathbf{B}}}{\partial t} & = \vec{\mathbf{0}} \\
  \nabla \cdot \vec{\mathbf{B}} & = 0
\end{align}

也可以在行内使用 LaTeX，例如，`$x^2$`。

您还可以在设置中添加自定义宏。添加的自定义宏可以在所有的 LaTeX 单元格中使用。

## 图表单元格

使用图标单元格可以很方便地创建序列图和流程图。

序列图示例:

```sequence
Title: Here is a title
A->B: Normal line
B-->C: Dashed line
C->>D: Open arrow
D-->>A: Dashed open arrow
```

流程图示例:

```flow
st=>start: Start:>http://www.google.com[blank]
e=>end:>http://www.google.com
op1=>operation: My Operation
sub1=>subroutine: My Subroutine
cond=>condition: Yes
or No?:>http://www.google.com
io=>inputoutput: catch something...

st->op1->cond
cond(yes)->io->e
cond(no)->sub1(right)->op1
```