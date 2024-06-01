---
title: Vitis HLS 基础
date: 2024-05-31 21:21:26
categories: 
- HLS
tags: 
- Vitis HLS
- FPGA
---

Vitis HLS 基础学习笔记

## 数据类型

### 1. 任意精度数据类型  
```
#include <ap_int.h>
ap_[u]int<W>  // 最大可扩展至32k位

#include <ap_fixed.h>
ap_[u]fixed<W, I, Q, O>    // W总位宽、I整数位宽、Q量化模式、O溢出模式
```
### 2. 变量初始化
```
ap_int<6> a_6bit_var_c = -22;
ap_int<6> a_6bit_var_d(22);
ap_int<6> a_6bit_var_r2("0b101010", 2);   // 指定进制数
ap_int<6> a_6bit_var_r2("101010", 2);
```
### 3. 数据类型转换  
显示转换
``` 
(Expected type) Variable
Expected type (Variable)
```  
常用运算的数据类型转换  
{% asset_img 1.jpg 数据类型转换 %}
