# practical-algorithm-note

**常用算法和数据结构的基本操作**

# 算法
- [回溯算法](algorithm/backtracking.md)

# 数据结构
- [链表](data_structure/linked_list.md)
# 一些tricks
- [位运算符](tricks/bitwise_operators.md)
- [整型溢出](tricks/integer_overflow.md)
- 当需要重复移动数组中的元素时，可以尝试从后面开始遍历移动。eg.《剑指offer》第5题
- 形参是容器时，可以考虑用迭代器来作为形参，来节省空间，尤其当容器作为迭代函数的形参时
- 循环和递归都能实现重复计算。递归往往代码简单，但效率较低；循环实现效率一般更高
- 在有序或部分有序的数组中查找一个数字或统计某个数字出现的次数时，可以尝试采用二分查找算法。eg.《剑指offer》第11题
