---
title: vscode阅读kernel使用的c_cpp_properties.json
date: 2021-05-10 18:30:00
categories: Kernel
tags: 
    - Kernel
    - Linux 
    - Vscode 
---

```json
{
    "configurations": [
        {
            "name": "Linux",
            "includePath": [
                "${workspaceFolder}/**",
                "${workspaceFolder}/include",
                "${workspaceFolder}/arch/arm/include" 
            ],
            "forcedInclude": [
                "${workspaceFolder}/include/generated/autoconf.h"
            ],
            "defines": [
                "__KERNEL__"
            ],
            "compilerPath": "/opt/arm-gcc/bin/arm-linux-gnueabihf-gcc",
            "cStandard": "c11",
            "intelliSenseMode": "gcc-x64"
        }
    ],
    "version": 4
}
```
