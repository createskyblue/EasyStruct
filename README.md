# 介绍 Introduction

*提示：解包 Unpack功能有问题，正在修复*

`EasyStruct` 是`struct`项目的简化版，允许一次性对结构体进行打包和解包

`EasyStructure` is a simplified version of the `struct` project, allowing one-time packaging and unpacking of structures.

具体使用方法和`struct`项目有差异

The specific use method is different from the `struct`.

## 格式 Format

`struct` uses following format characters (note that `struct` does not fully
support the Python struct module's format):

Table 1. Byte order

Character | Byte order             
----------|-----------
 `=`      | native                 
 `<`      | little-endian          
 `>`      | big-endian             
 `!`      | network (= big-endian) 


Table 2. Format characters

Format | C/C++ Type         | Standard size
-------|--------------------|--------------
 `b`   | char               | 1
 `B`   | unsigned char      | 1
 `h`   | short              | 2
 `H`   | unsigned short     | 2
 `i`   | int                | 4
 `I`   | unsigned int       | 4
 `l`   | long               | 4
 `L`   | unsigned long      | 4
 `q`   | long long          | 8
 `Q`   | unsigned long long | 8
 `f`   | float              | 4
 `d`   | double             | 8
 `s`   | char[]             |
 `p`   | char[]             |
 `x`   | pad bytes          |
 `v`   | go/pbuf svarint    |
 `V`   | go/pbuf varint     |

## 打包 Pack

```c
#include "struct.h"
...
typedef struct
{
    char device_name[16];
    char device_FW_Ver[16];
    uint8_t device_MAC[6];
    uint8_t device_DHCP;
    uint32_t device_IPv4;
    uint32_t device_IPv4_mask;
    uint32_t device_IPv4_gateway;
    uint32_t device_IPv4_DNS;
    uint8_t passwdHash[16];
    uint8_t serial_count;
    uint8_t remote_count;
    uint8_t gateway_count;
    uint8_t scanCMD_count;
}config_static_t;

config_static_t config_static;
config_init(&config_static);

char buf[1024];
struct_pack(buf, "!16s16s6BBLLLL16BBBBB", config_static);
```

## 解包 Unpack (不可用 Not available)

```c
...
config_static_t config_static_unpack;
struct_unpack(buf, "!16s16s6BBLLLL16BBBBB", config_static_unpack);
```


# 参考文献 References
[Original svperbeast-struct](https://github.com/svperbeast/struct "svperbeast-struct project")

[The Practice of Programming (9.1 Formatting Data)](http://www.amazon.com/Practice-Programming-Addison-Wesley-Professional-Computing/dp/020161586X/ref=sr_1_1?ie=UTF8&qid=1359350725&sr=8-1&keywords=practice+of+programming "The Practice of Programming")

[Python struct](http://docs.python.org/2/library/struct.html#module-struct "Python struct module")

# 许可证 License
Code released under [the MIT license](https://github.com/svperbeast/struct/blob/master/LICENSE).
