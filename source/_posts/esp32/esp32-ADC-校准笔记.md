---
title: esp32-ADC-校准笔记
date: 2021-06-18 16:36:25
categories: esp32
tags: 
    - esp32
---

读取校准信息  
```
python components\esptool_py\esptool\espefuse.py --port COM3 adc_info
```
写入二点校准值  
```
python components\esptool_py\esptool\espefuse.py burn_block_data --offset 12 BLOCK3 C:\Users\27207\Desktop\temp\efuse_blk3.bin --port COM3
python components\esptool_py\esptool\espefuse.py burn_efuse BLK3_PART_RESERVE 1 --port COM3
```

```
```