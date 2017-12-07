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
