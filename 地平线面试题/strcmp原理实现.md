``` cpp
int strcmp(const char* str1, const char* str2) {
    int i = 0;
    while (str1[i] != '\0' && str2[i] != '\0') {
        if (str1[i] < str2[i]) {
            return -1;
        } else if (str1[i] > str2[i]) {
            return 1;
        }
        i++;
    }
    if (str1[i] == '\0' && str2[i] == '\0') {
        return 0;
    } else if (str1[i] == '\0') {
        return -1;
    } else {
        return 1;
    }
}

```
以上代码中，我们使用了一个循环来逐个比较两个字符串的字符。如果str1的当前字符小于str2的当前字符，则返回-1；如果str1的当前字符大于str2的当前字符，则返回1。如果两个字符串的当前字符相等，则继续比较下一个字符。

当循环结束时，如果str1和str2都已经遍历完毕（即当前字符为'\0'），则说明两个字符串相等，返回0。如果str1已经遍历完毕而str2还有剩余字符，则说明str1小于str2，返回-1。如果str2已经遍历完毕而str1还有剩余字符，则说明str1大于str2，返回1。

这样，我们就实现了一个简单的strcmp函数。需要注意的是，这个实现是基于C风格的字符串，即以'\0'结尾的字符数组。在使用时，需要确保传入的字符串是以'\0'结尾的。
