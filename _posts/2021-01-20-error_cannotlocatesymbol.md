---
title: "dlopen failed: cannot locate symbol xxx"
date: 2021-01-20 00:03:00
categories: error_fix
---

# dlopen failed: cannot locate symbol xxx
동적함수를 사용할때 "<b>dlopen failed: cannot locate symbol</b>" 에러가 발생할때가 있다.

이러한 에러가 발생할 경우 라이브러리에 symbol이 실제로 존재하는지 여부를 확인해야 한다.

동적 라이브러리에 symbol 정보를 확인하기 위해서는 <b>nm -D xxx.so</b> 명령어를 사용하면 알 수 있다.

![nmCommandResult](https://hankyojeong.github.io/assets/images/error/dynamicLibSymbol.png)

symbol type에 'U'는 Undefined를 의미한다. U가 있으면 symbol이 정의되어 있지 않다는 의미.

확인하여 symbol 정보가 동적 라이브러리에 있는지 확인 후 없으면 라이브러리를 다시 빌드해주어야 한다.

