## 2.2节的练习
### 练习 2.2.1

考虑下面的上下文无关文法：

S ->  S S +  | S S * | a

1) 试说明如何使用该文法生成串 aa+a* 。

2) 试为这个串构造一颗语法分析树。

3) 该文法生成的语言是什么？证明你的答案。

解答：

1) 首先使用文法 S -> S S \*
。然后箭头右边第一个 S 由 S S + 替换，第二个 S 由 a 替换，生成 SS+a\* 。再用 a 替换 S ，得到 aa+a*。

2) 根据 1) 的解答

![](/resources/section2/2.2.1-1.png)

3) 该文法生成的应该是只有加法和乘法运算的后缀数学表达式。具体怎么该证明还没有想法。

### 练习 2.2.2

下面的各个文法生成什么语言？ 证明你的每一个答案。

1) S -> 0 S 1 | 0 1

2) S-> + S S | - S S | a

3) S -> S ( S ) S | $\epsilon$

4) S -> a S b S | b S a S | $\epsilon$

5) S -> a | S + S | S S | S * | ( S )

解答：

1) 0^n 1^n

2) 只含有加减运算的前缀数学表达式

3) 应该是 lisp 语法

4)

5)

### 练习 2.2.3

练习 2.2.2 中哪些文法具有二义性？

### 练习 2.2.4

为下面的各个语言构建无二义性的上下文无关文法，并证明你的文法都是正确的。

1) 用后缀方式表示的算术表达式。

2) 由逗号分隔开的左结合的标志符列表。

3) 由逗号分隔开的右结合标志符列表。

4) 由整数、标识符、四个二目运算符 + 、- 、 \* 、/ 构成的算术表达式。

!5) 在 4) 的运算符中增加单目 + 和单目 - 构成的算术表达式。

解答：

1) S -> S S + | S S - | S S * | S S / | a

### 练习 2.2.5：

1) 证明：用下面文法生成的所有二进制串的值都能被 3 整除。（提示：对语法分析树的节点数目使用数学归纳法。）

num -> 11 | 1001 | num 0 |num num

2) 上面的文法是否能够生成所有能被 3 整除的二进制串？

解答：

1) 首先针对 num -> 11 使用数学归纳法。

基础情形，二进制串 11 的十进制值为 3，显然能被 3 整除。

现在假设二进制串 num 能被 3 整除，要证明 num 0 也能被 3 整除。

我们知道移位操作 num 0 相当于把 num 翻倍，于是当 num 能被 3 整除时，num 0 自然也能被 3 整除。

而 num num 这个串相当于吧 num 左移多位之后再与 num 相加，自然也能被 3 整除。

针对 num -> 1001 如法炮制也能证明。

### 练习 2.2.6：

为罗马数字构建一个上下文无关文法

解答：

S -> S S | S | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 9

## 2.3 节的练习

### 练习2.3.1：

构建一个语法制导翻译方案，该方案吧算术表达式从中缀表达式翻译成运算符在运算分量之前的前缀表示方式。例如，-xy 是表达式 x-y 的前缀表达式法。给出输入 9 - 5 + 2 和 9 - 5 * 2 的注释分析树。

解答：

产生式|语义规则
---|---
expr -> expr_1 + term | expr.t = '+' ~ expr_1.t ~ term.t
expr -> expr_1 - term | expr.t = '-' ~ expr_1.t ~ term.t
expr -> expr_1 * term | expr.t = '\*' ~ expr_1.t ~ term.t
expr -> expr_1 / term | expr.t = '/' ~ expr_1.t ~ term.t
expr -> term | expr.t = term.t
expr -> 0 | '0'
...|...
expr -> 9 | '9'

首先写出表达式 9 - 5 + 2 的语法分析树

![](2.3.1-1.png)

然后再利用语义规则转换成注释分析树

![](2.3.1-2.png)

然后是 9 - 5 * 2 的注释分析树（同样的原理）

![](2.3.1-3.png)

### 练习 2.3.2：

构建一个语法制导翻译方案，该方案将算术表达式从后缀表达方式翻译成中缀表达方式。给出输入 95-2\* 和 952\*- 的注释分析树。

解答：

产生式|语义规则
---|---
expr -> expr_1 term + | expr.t = '(' ~ expr_1.t ~ '+' ~ term.t ~ ')'
expr -> expr_1 term - | expr.t = '(' ~ expr_1.t ~ '-' ~ term.t ~ ')'
expr -> expr_1 term \* | expr.t = expr_1.t ~ '\*' ~ term.t
expr -> expr_1 term / | expr.t = expr_1.t ~ '/' ~ term.t
expr -> term | expr.t = term.t
expr -> 0 | '0'
...|...
expr -> 9 | '9'

注释分析树 95-2\*

![](2.3.2-1.png)

注释分析树 952\*-

![](2.3.2-2.png)

### 练习 2.3.3：

构建一个将整数翻译成罗马数字的语法制导翻译方案。

### 练习 2.3.4

构建一个将罗马数字翻译成整数的语法制导翻译方案。

### 练习 2.3.5

构建一个将后缀算术表达式翻译成等价的前缀表达式的语法制导翻译方案。

## 2.4 节的练习

练习 2.4.1：
为下列文法构造递归下降语法分析器：

1) S -> + S S | - S S | a

2) S -> S ( S ) S | $\epsilon$

3) S -> 0 S 1  | 0 1

解答：

1.
```java
void S(){
  switch(lookahead){
    case "+":
      match("+"); S(); S();
      break;
    case "-":
      match("-"); S(); S();
      break;
    case a:
      match(a);
      break;
    default:
      report("syntax error");
  }
}

void match(terminal t) {
  if(lookahead == t) {
    lookahead = nextTerminal;   
  }else {
    report("syntax error");
  }
}
```

2.
```java
void S() {
  switch(lookahead) {
    case
  }
}

```

3.
```java
void S() {
  switch(lookahead) {
    case 0:
      match(0); S(); match(1);
      break;
    case 1;
  }
}
```

## 3.1 节的练习

### 练习3.1.1

根据3.1.2 节中的讨论，将下面的C++程序

```c++
float limitSquare(x) {float x;
  /* returns x-squared, but never more than 100*/
  return (x <=  -10.0 || x >= 10.0) ? 100: x*x;
}
```
划分成正确的词素序列。哪些词素应该有相关联的词法值，应该具有什么值？

解答：
```
<id, float>
<id, limitSquare>
<id, x>
<id, float>
<id, x>
<id, return>
<id, x>
<comparasion, <=>
<number, -10.0>
<?>
<number, 100>
<:>
<id, x>
<op, *>
<id, x>
```
