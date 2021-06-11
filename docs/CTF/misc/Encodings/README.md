# 编码

- [ASCII编码](#ascii)
- 进制
  - 二进制
  - 八进制
  - 十六进制
- URL编码
- HTML实体编码
- Base编码

?> 强烈推荐在线工具 https://gchq.github.io/CyberChef/

## ASCII编码 :id=ascii

ASCII（**A**merican **S**tandard **C**ode for **I**nformation **I**nterchange，**美国信息交换标准代码**）是基于拉丁字母的一套电脑编码系统。它主要用于显示现代英语。

![](https://upload.wikimedia.org/wikipedia/commons/1/1b/ASCII-Table-wide.svg)

## 进制

> Windows系统自带计算器的程序员模式，支持进制转换

### 二进制 :id=bin

以2为底的进位制，使用数字0和1表示。

### 八进制 :id=oct​

以8为底的进位制，使用数字0-7表示。

### 十六进制 :id=hex

以16为底的进位制，使用数字0-9和字母A-F表示。

十六进制普遍应用在计算机领域，这是因为$log_216=4$，一个字节8比特能够用2位十六进制表示。为和其他进制区分，通常使用`0x`前缀，如`0x1`

## URL编码

URL（**U**niform **R**esource **L**ocator，统一资源定位符）俗称网页地址，简称网址。

URL编码，又称百分号编码。

URL 不能包含空格。URL 编码通常使用 加号（+）或`%20` 来替换空格。

2005年1月发布的RFC 3986，

```
建议所有新的URI必须对未保留字符不加以百分号编码；其它字符建议先转换为UTF-8字节序列, 然后对其字节值使用百分号编码。
```

网络标准[RFC1738](https://www.ietf.org/rfc/rfc1738.txt)规定：

```
"...Only alphanumerics [0-9a-zA-Z], the special characters "$-_.+!*'()," [not including the quotes - ed], and reserved characters used for their reserved purposes may be used unencoded within a URL."

"只有字母和数字[0-9a-zA-Z]、一些特殊符号"$-_.+!*'(),"[不包括双引号]、以及某些保留字，才可以不经过编码直接用于URL。"
```
示例：
`http://www.test.com/?query=你好`经过URL编码为
`http%3A%2F%2Fwww.test.com%2Fquery%3D%E4%BD%A0%E5%A5%BD`

## HTML实体编码

HTML 实体是一段以连字号（`&`）开头、以分号（`;`）结尾的文本（字符串），如`&#8212;`。实体常常用于显示保留字符（这些字符会被解析为 HTML 代码，如`<`、`>`）和不可见的字符（如“不换行空格”）。你也可以用实体来代替其他难以用标准键盘键入的字符。

[HTML实体介绍](ttps://developer.mozilla.org/zh-CN/docs/Glossary/Entity)

## Base家族

- [Base32](#Base32)
- [Base64](#Base64)
- Base58
- [Base85](#Base85)

### Base32

在Base32中的32个可打印字符包括大写字母`A-Z`和数字`2-7`。

### [Base64](https://zh.wikipedia.org/wiki/Base64)

Base64是一种基于64个可打印字符来表示二进制数据的表示方法。由于$log_264=6$，所以每6个比特为一个单元，对应某个可打印字符。在Base64中的可打印字符包括字母`A-Z`、`a-z`、数字`0-9`以及`+`、`/`。

如果要编码的字节数不能被3整除，最后会多出1个或2个字节，那么可以使用下面的方法进行处理：先使用0字节值在末尾补足，使其能够被3整除，然后再进行Base64的编码。在编码后的Base64文本后加上一个或两个`=`号，代表补足的字节数。也就是说，当最后剩余两个八位(待补足)字节（2个byte）时，最后一个6位的Base64字节块有四位是0值，最后附加上两个等号；如果最后剩余一个八位(待补足)字节（1个byte）时，最后一个6位的base字节块有两位是0值，最后附加一个等号。 

### Base85

在Base32中的32个可打印字符包括大写字母`A-Z`和数字`2-7`。

| 算法   | 字符集                                                       |
| ------ | ------------------------------------------------------------ |
| Base32 | 大写字母`A-Z`、数字`2-7`                                     |
| Base64 | 字母`A-Z`、`a-z`、数字`0-9`以及`+`、`/`                      |
| Base58 | 与Base64相比，去除数字`0`、大写字母`O`、大写字母`I`、小写字母`i`、字符`+`和`/` |
| Base85 | `！`-`u`（ASCII 33-117）和`z`（ASCII 122）                   |

## 参考资料

阮一峰 [《字符编码笔记：ASCII，Unicode 和 UTF-8》](http://www.ruanyifeng.com/blog/2007/10/ascii_unicode_and_utf-8.html)

