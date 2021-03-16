---
title: "ERROR:root:code for hash md5 was not found"
date: 2021-03-17 00:08:00
categories: error_fix
---

# ERROR:root:code for hash md5 was not found
webRTC를 빌드하다가 아래와 같은 에러가 발생했다.
```
ERROR:root:code for hash md5 was not found
```

인터넷에 검색하여 찾아보니 Python을 지웠다가 깔던가 다시 깔라고 하였다.

보니 Python 2점대 버전을 사용해야 하는것으로 보였다.

나는 맥 개발환경인데, 아래의 검색어로 python을 찾아보니
```
$brew search python
```
![nmCommandResult](https://hankyojeong.github.io/assets/images/error/brew_python.png)

homebrew에는 python 3점대로 설치되어 있는것으로 보인다.

사람들이 하라는 대로 python 2점대를 uninstall하고 다시 install해보았다.
```
$ brew uninstall python@2
$ brew install python@2
```
하지만 이 때 brew install python@2에서 문제가 발생했다.
```
==> Searching for similarly named formulae...
Error: No similarly named formulae found.
Error: No available formula or cask with the name "python@2".
==> Searching for a previously deleted formula (in the last month)...
Error: No previously deleted formula found.
==> Searching taps on GitHub...
Error: No formulae found in taps.
```

homebrew에서 나의 mac 버전(10.15.5 Catalina)에서는 더 이상 python 2점대를 지원하지 않는다고 하였다.

## 해결방법
직접 python 사이트에 들어가 python 2점대를 설치하니 해당 문제가 해결되었다.

Python Site: https://www.python.org/downloads/release/python-2718/

설치 후 폴더 안에 있는 'Install Certificates.command' 파일을 실행해주니 문제 없이 잘 동작하였다.