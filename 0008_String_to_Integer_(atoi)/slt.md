## 思路1 遍历字符串

按照题意，遇到第一个（非正负号 && 非空格 && 非数字）的字符就停止。
检查溢出的思路类似第七题，不过这道题在计算中不带符号，都是正的，所以只用检查正溢出。如果结果是INT_MIN的话，正溢出的判断也能检查到。
