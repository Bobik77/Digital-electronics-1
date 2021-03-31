# BPC-DE1 Lab_08
:paperclip: Repository:
[Bobik77](https://github.com/Bobik77) 
/
[Digital-electronic-1](https://github.com/Bobik77/Digital-electronics-1) 
/
[LAB_08](https://github.com/Bobik77/Digital-electronics-1/tree/main/LAB_08)

## 1. Preparation task


| **Input P** | `0` | `0` | `1` | `1` | `0` | `1` | `0` | `1` | `1` | `1` | `1` | `0` | `0` | `1` | `1` | `1` |
| :-- | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| **Clock** | ![rising](img/eq_uparrow.png) | ![rising](img/eq_uparrow.png) | ![rising](img/eq_uparrow.png) | ![rising](img/eq_uparrow.png) | ![rising](img/eq_uparrow.png) | ![rising](img/eq_uparrow.png) | ![rising](img/eq_uparrow.png) | ![rising](img/eq_uparrow.png) | ![rising](img/eq_uparrow.png) | ![rising](img/eq_uparrow.png) | ![rising](img/eq_uparrow.png) | ![rising](img/eq_uparrow.png) | ![rising](img/eq_uparrow.png) | ![rising](img/eq_uparrow.png) | ![rising](img/eq_uparrow.png) | ![rising](img/eq_uparrow.png) |
| **State** | A | A | B | C | C | D | A | B | C | D | B | B | B | C | D | B |
| **Output R** | `0` | `0` | `0` | `0` | `0` | `1` | `0` | `0` | `0` | `1` | `0` | `0` | `0` | `0` | `1` | `0` |

pre![scheme](img/sw_led_scheme.png)

| **RGB LED** | **Artix-7 pin names** | **Red** | **Yellow** | **Green** |
| :-: | :-: | :-: | :-: | :-: |
| LD16 | N15, M16, R12 | `1,0,0` | `1,1,0` | `0,1,0` |
| LD17 | N16, R11, G14 | `1,0,0` | `1,1,0` | `0,1,0` |