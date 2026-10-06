---
title: "블로그를 시작하며"
date: 2026-10-07
draft: true
description: "예시 글 — 코드 하이라이팅과 목차 확인용"
tags: ["stm32"]
---

## GPIO 토글

```c
#include "stm32f4xx_hal.h"

int main(void) {
    HAL_Init();
    while (1) {
        HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5); // LD2
        HAL_Delay(500);
    }
}
```

## 다음 글

`HAL_Delay` 대신 타이머 인터럽트로 바꿔 본다.
