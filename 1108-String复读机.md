# 1108 String复读机

- **分值：** 20分

### 题目描述

给定一个长度不超过 $10^{4}$ 的、仅由英文字母构成的字符串。请将字符重新调整顺序，按 `StringString....` （注意区分大小写）这样的顺序输出，并忽略其它字符。当然，六种字符的个数不一定是一样多的，若某种字符已经输出完，则余下的字符仍按 `String` 的顺序打印，直到所有字符都被输出。例如 `gnirtSSs` 要调整成 `StringS` 输出，其中 `s` 是多余字符被忽略。

### 输入格式：

输入在一行中给出一个长度不超过 $10^{4}$ 的、仅由英文字母构成的非空字符串。

### 输出格式：

在一行中按题目要求输出排序后的字符串。题目保证输出非空。

### 输入样例：
```
sTRidlinSayBingStrropriiSHSiRiagIgtSSr
```

### 输出样例：
```
StringStringSrigSriSiSii
```


### 解题思路

本题的核心是：按给定步长循环取字符，直到回到起点，构造循环字符串。程序先读取题目输入，再按照上述规则完成数据处理，最后严格按照题目要求输出结果。实现时应优先根据题目约束选择合适的数据类型和数据结构，避免溢出或不必要的重复计算。

时间复杂度为 O(L)；空间复杂度取决于输入规模，主要用于保存题目数据和中间结果。

### 代码流程说明

1. 读取 1108 String复读机 所需的输入数据。
2. 初始化计数器、数组或其他辅助变量。
3. 按给定步长循环取字符，直到回到起点，构造循环字符串。
4. 按题目规定的格式输出计算结果。

### 代码实现

```java
import java.io.*;
import java.util.*;

public class Main {
    static class FastScanner {
        private final InputStream in; private final byte[] buffer = new byte[1 << 16]; private int ptr, len;
        FastScanner(InputStream in) { this.in = in; }
        private int read() throws IOException { if (ptr >= len) { len = in.read(buffer); ptr = 0; if (len < 0) return -1; } return buffer[ptr++]; }
        String next() throws IOException { StringBuilder b = new StringBuilder(); int c; do c = read(); while (c <= 32 && c >= 0); while (c > 32) { b.append((char)c); c = read(); } return b.toString(); }
        char[] nextChars() throws IOException { return next().toCharArray(); }
        int nextInt() throws IOException { return Integer.parseInt(next()); }
        long nextLong() throws IOException { return Long.parseLong(next()); }
        double nextDouble() throws IOException { return Double.parseDouble(next()); }
        void skip() throws IOException { next(); }
    }
    static int strlen(char[] s) { int n = 0; while (n < s.length && s[n] != 0) n++; return n; }
    static int strcmp(char[] a, char[] b) { return new String(a, 0, strlen(a)).compareTo(new String(b, 0, strlen(b))); }
    static int strncmp(char[] a, char[] b) { return strcmp(a, b); }
    static void printf(String format, Object... args) { Object[] x = new Object[args.length]; for (int i=0;i<args.length;i++) x[i] = args[i] instanceof char[] ? new String((char[])args[i], 0, strlen((char[])args[i])) : args[i]; System.out.printf(format.replace("%lld", "%d"), x); }
    static void puts(Object x) { System.out.println(x instanceof char[] ? new String((char[])x, 0, strlen((char[])x)) : x); }
    static void putchar(char c) { System.out.print(c); }
    static void putchar(int c) { System.out.print((char)c); }
    static final int EOF = -1;
    static int getchar() { return -1; }
    static int isupper(char c) { return Character.isUpperCase(c) ? 1 : 0; }
    static char tolower(int c) { return Character.toLowerCase((char)c); }
    static int strchr(char[] s, char c) { for (int i=0;i<strlen(s);i++) if (s[i]==c) return i; return -1; }
/*
 * 题目：1108 字符串循环
 * 实现原理：按给定步长循环取字符，直到回到起点，构造循环字符串。
 * 复杂度：O(L)
 * 实现步骤：
 * 1. 读取 1108 String复读机 所需的输入数据。
 * 2. 初始化计数器、数组或其他辅助变量。
 * 3. 按给定步长循环取字符，直到回到起点，构造循环字符串。
 * 4. 按题目规定的格式输出计算结果。
 */

static FastScanner fs = new FastScanner(System.in);

    public static void main(String[] args) throws Exception {
    char[] s = new char[10005]; char[] o = "String".toCharArray();
    int[] c = new int[6];
    s = fs.nextChars();
    for (int i = 0; i < strlen(s); i ++) for (int j = 0; j < 6; j ++) if (s[i] == o[j]) c[j] ++;
    int left = 1;
    while (left != 0) {
        left = 0;
        for (int j = 0; j < 6; j ++) if (c[j] != 0) putchar(o[j]), c[j] --, left = 1;
    }
    putchar('\n');

}
}
```

### 代码流程图

```mermaid
flowchart TD
  A[开始] --> B[读取输入]
  B --> C[初始化数据和辅助变量]
  C --> D[执行核心算法]
  D --> E[整理输出结果]
  E --> F[结束]
```

### 解题流程图

```mermaid
flowchart TD
  A[输入题目数据] --> B{{数据是否满足处理条件}}
  B -- 是 --> C[按照题意进行计算]
  B -- 否 --> D[处理边界情况]
  C --> E[输出答案]
  D --> E
  E --> F[程序结束]
```

### 常见易错点

- 注意输入数据的范围，选择足够大的整数类型，并正确处理边界值。
- 循环、数组下标和字符串结束位置要严格对应题目定义，避免越界。
- 输出格式必须与题目要求完全一致，包括空格、换行、大小写和特殊符号。
- 如果存在排序、去重、进位、约分或四舍五入等操作，应在输出前统一完成。
