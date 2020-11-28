# 整型溢出问题的处理方法
下面仅讨论两数相加时，整数溢出的情况。
## INT_MAX
在头文件<climit>中，定义了 INT_MAX 表示有符号整型的最大值。
## 处理方法一
由于无符号整型最大值比有符号整型大，故可将有符号转化为无符号
```c++
if((unsigned)a + (unsigned)b > INT_MAX){
  std::cerr << " error message " << '\n';
}
```
## 处理方法二
加法转减法
```c++
if(a > INT_MAX - b){
  std::cerr << " error message " << '\n';
}
```
## 处理方法三
转化为字符串相加,下面给出字符串相加的函数
```c++
string getSum(string n1, string n2) {
    //从后往前加
    string sum;
    //进位
    int carry = 0;
    //注意哦，i 的初始值为 1 。
    for (unsigned int i = 1; i <= n1.length() || i <= n2.length(); i++)
    {
        int n = carry;
        //从后向前取字符串每个下标的字符
        //根据美国信息交换标准代码（即常称的 ASCII ）可知，字符 0 的十进制码表示为 48，所以在此需要减去 48 。
        n += i <= n1.length() ? n1[n1.length() - i] - 48 : 0;
        n += i <= n2.length() ? n2[n2.length() - i] - 48 : 0;
        carry = n / 10;
        n %= 10;
        //将整数转换为字符，所以加上 48 。
        //（在开头插入 1 个字符）
        sum = sum.insert(0,1,char(n + 48));
    }
    if (carry > 0)
        sum = sum.insert(0,1, '1'); ;
    return sum;
}
```
