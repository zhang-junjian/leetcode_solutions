## 思路1 不断把x从地位取走，然后从高位构建一个新的数

注意如果x以0结尾直接pass掉，因为不可能以0开头。

```cpp
class Solution {
public:
    bool isPalindrome(int x) {
        if (x < 0 || (x != 0 && x % 10 == 0)) return false;
        int res = 0;
        while (res < x)
        {
            res = res * 10 + x % 10;
            x /= 10;
        }
        // each represent case of "123321" and "12321"
        return x == res || x == res / 10;
    }
};
```

```py
class Solution:
    def isPalindrome(self, x: int) -> bool:
        if x < 0 or (x != 0 and x % 10 == 0):
            return False

        sum = 0
        while sum < x:
            sum = sum*10 + x%10
            x //= 10
        
        return (x == sum) or (x == sum//10)
```

## 思路2 依次取左右两边的数字来比较

首先题目提示我们不要用转换成字符串的方法来做。如果转换成字符串，用python一行就可以搞定。

```py
return int(str(abs(x))[::-1]) == x
```

我们这里的思路是用一个`ranger`来表示输入的x的位数，如x是`123321`，我们的`ranger`就是`100000`。然后分别取出左右两边的数进行比较。

注意`python3`中的取整除法是`//`

```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        if x < 0:
            return False
        
        ranger = 1
        while x // ranger >= 10:
            ranger *= 10
            
        while x:
            left = x // ranger
            right = x % 10
            if left != right:
                return False
            
            x = (x % ranger) // 10
            ranger //= 100
        
        return True
```