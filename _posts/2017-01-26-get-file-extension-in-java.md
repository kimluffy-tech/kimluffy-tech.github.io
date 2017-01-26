---
layout: post
title:  "파일의 확장자 구하기(JAVA)"
---
# 목표
JAVA 에서 파일의 확장자를 구해보자.

# 시작하며
간혹 ~~파일의 확장자가 필요하거나 파일의 확장자가 필요할 때..~~ 파일의 확장자명이 필요한 경우가 있습니다.
기억을 더듬어 '음..[lastIndex()]()로 파일명의 뒤에서 부터 . 을 찾고.. 어.. 그 다음에 뭐였더라 어디 만들어뒀을텐데..' 하다가 결국 웹 검색을 되풀이 합니다.
이번에 공유하게 될 방법은 다시는 파일 확장자 때문에 제 블로그를 재방문하실 일이 없는 그런 방법이라 여겨집니다.

# 해결방법

## FilenameUtils.getExtension

[Apache Commons IO](https://commons.apache.org/proper/commons-io/) 에서 제공하는 [FilenameUtils.getExtension](http://commons.apache.org/proper/commons-io/javadocs/api-2.5/src-html/org/apache/commons/io/FilenameUtils.html#line.1034) 이 바로 그것입니다.


```

1034    public static String getExtension(final String filename) {
1035        if (filename == null) {
1036            return null;
1037        }
1038        final int index = indexOfExtension(filename);
1039        if (index == NOT_FOUND) {
1040            return "";
1041        } else {
1042            return filename.substring(index + 1);
1043        }
1044    }

```

위의 소스를 눈으로 따라가보시면 **파일의 확장자 또는 공백값을 리턴** 해주기 때문에 시작할 때 고민했던 것들을 모두 해결해줍니다.

앞으로 file 을 치고 cmd+space(eclipse intellisense)를 이용하여 손쉽게 파일 확장자를 구할 수 있게 되었습니다.
