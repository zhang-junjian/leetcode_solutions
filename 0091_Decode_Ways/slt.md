### 思路1 dp

dp[i]表示长度为i的str的可能解码方式。这里我们dp的总长度是`str.size()+1`。dp[0]存放1。不表示0长度的解码种数，只是为了后面的计算

以12345为例，第二行是dp对应的元素。可见当前s[i]在1到9之间时，解码的数量和dp[i-1]持平。但是substr(i-2,2)在10到26之间时，dp[i]还要加dp[i-2];

```txt
 12345
112333
```
