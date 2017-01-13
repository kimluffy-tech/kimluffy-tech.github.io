---
layout: post
title:  "Windows에서 git bash $HOME 설정"
tags: [windows,jekyll,github,pages,setting,git bash]
categories: github pages
---
# 시작하며
현재 저는 로컬에 jekyll을 이용하여 Github Pages를 세팅한 상태입니다.

출근하여 jekyll을 실행하려고보니 git bash 에서 에러가 났습니다.

> '아, 여기(폴더)가 아니구나..'

```vim
$ cd
```
를 입력하다가

> 'git bash 를 실행할 때 내가 원하는 로컬 폴더가 바로 나오게 할 수 없을까?'

생각했습니다.

# 해결방법
1.마우스 우클릭 > 'Git Bash Here' 선택.

![git bash here](/images/git_bash_here.png)

2.'.bashrc' 파일 수정

git bash 실행.

[vi](https://namu.wiki/w/vi)(텍스트 에디터) 를 이용해 편집.

```vim
$ vi ~/.bashrc
```

INSERT 모드(i)에서 원하는 경로를 입력 후 저장(:wq).

{% highlight ruby %}
cd My\ Documents/GitHub/kimluffy-tech.github.io
{% endhighlight %}

git bash 재실행.

원하는 경로인지 확인.

```vim
$ pwd
```

# 마치며
문득 느낀 불편함을 해결하고, 그 내용을 첫 글로 공유할 수 있어 기쁩니다.
