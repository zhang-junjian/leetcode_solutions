# OOP basics

## 类和对象的基本概念和用法

对象占用的内存空间大小：等于所有成员变量的大小只和。注意成员函数只有一份，不会放在对象中。

和结构变量一样，对象之间可以用 = 进行赋值，但是不能直接用“== != > < >= <=”进行比较，除非对他们进行了重载。

### 类成员的可访问范围

缺省类型是私有。

在类的成员函数的内部，可以访问：

- 当前对象的全部属性，函数
- 同类其他对象的全部属性，函数

## 构造函数

对象的存储空间不是构造函数分配的。构造函数只是在已经分配好的存储空间中去做一些初始化的工作。

构造函数在数组中的使用：

```cpp
class Test{
    public:
        Test(int n){}           // 1
        Test(int n, int m) {}   // 2
        Test(){}                // 3
};
Test array1[3] = {1, Test(1,2)};            // 三个元素分别用1 2 3 初始化
Test array2[3] = {Test(2,3), Test(1,2), 1}; // 三个元素分别用2 2 1初始化
Test *pArray[3] = {new Test(4), new Test(1,2)}
```

注意`pArray`是指针数组，需要用new创建对数组元素（即指针）所指向的对象。这里只创建了两个对象。pArray[2]没有被初始化。

## 复制构造函数

- 只有一个参数，即对同类对象的引用
- 形如：`X::X(X &)`或`X::X(const X &)`，后者能以常量对象最为参数
- 如果没有复制构造函数，编译器会自动生成一个

复制构造函数起作用的三种情况

1 当用一个对象去初始化同类的另一个对象

```cpp
Complex c2(c1);
Complex c2 = c1;    // 同上面的语句效果一样，注意这是初始化语句，不是赋值语句！！！！
```

注意这两种情况调用的不是复制构造函数

```cpp
Complex c1 = Complex(1,2);
Complex c2(Complex(1,2));
```

2 函数的参数是类的对象。调用函数时，复制构造函数被调用。
3 函数的返回值是一个对象，则函数返回时，复制构造函数被调用。

**注意：对象间赋值不会调用复制构造函数**

```cpp
class CMyclass{
public:
    int n;
    CMyclass(){};
    CMyclass(CMyclass & c){
        n = 2 * c.n;
    }
};
int main(){
    CMyclass c1, c2;
    c1.n = 5;
    c2 = c1;               // 注意这是赋值语句，不是初始化，复制构造函数不会被调用
    CMyclass c3 = c1;      // 这是初始化，复制构造函数会被调用
    cout << "c2.n" << c2.n << endl;
    cout << "c3.n" << c3.n << endl;
    return 0;
}
```

输出

```cpp
c2.n = 5
c3.n = 10
```

常量引用参数的使用：

```cpp
void fun(CMyclass obj_){
    cout << "fun" << endl;
}
```

- 这样的函数，调用时形参会引发复制构造函数调用，开销较大
- 可以考虑使用`CMyclass &`引用类型作为参数。引用是原对象的一个别名
- 如果希望原对象的值不被改变，可以加上`const`关键字

## 类型转换构造函数
