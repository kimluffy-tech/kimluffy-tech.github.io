---
layout: post
title:  "IE10에서 HTML5의 <video>가 동작하지 않을 경우"
categories: troubleshooting
---
# 목표

IE10에서 HTML5의 `<video>` 가 동작하지 않을 경우 원인과 해결 방법을 알아봤습니다.

---
<br />
## 시작하며

환경은 다음과 같습니다.
- 웹페이지에서 비동기로 동영상(mp4)을 서버(AWS S3)에 업로드.
- 업로드한 동영상의 url을 가져와 HTML5 `<video>` 영역에 노출.
- 크롬(Chrome), IE11(Internet Explorer 11) 등에서 정상 동작.
- IE10(Internet Explorer 10)에서는 동작하지 않음.

---
<br />
## 원인

### 브라우저 지원

브라우저가 지원을 안하는걸까? ~~MS 조차도 IE11을 권장하는데 IE10 따위 지원 안했으면 좋겠다.~~ 생각했지만 그렇지 않았습니다. 아래의 표에서 `<video>`의 mp4 에 대한 브라우저 지원 현황을 확인하실 수 있습니다.

|브라우저          |버전   | 지원유무   |
|:---------------|:-----:|:---------:|
|Internet Explorer |9.0   |Yes        |
|Firefox           |3.5   |Yes        |
|Chrome            |4.0   |Yes        |
|Safari            |4.0   |Yes        |
|Opera             |10.5  |Yes        |

### type 속성

`<video>` 하위 노드. `<source>` 의 type 속성에 MIME type 값을 명시해줘야 하는데 빠져서 그런걸까? 해결의 실마리는 MIME type 이 쥐고 있다는 것을 알게 되었습니다. 그래서 먼저 type 속성을 명시해주기로 했습니다.(mp4 파일만을 지원하기로 되어있기 때문에 한가지 type만을 고려하였습니다.)
```
<video>
  <source src="" type="video/mp4">
</video>
```

---
<br />
## 해결

### MIME type

서버(S3)에 업로드된 파일의 MIME type을 확인해보니 업로드 시 MIME type을 지정해주지 않아 업로드된 파일 모두 아래와 같은 Content-Type 을 가지고 있었습니다.
![Content-Type: application/octet-stream](/images/ie10_video_tag_not_working (1).PNG)

```
ObjectMetadata metadata = new ObjectMetadata();
metadata.setContentType("video/mp4");
```
그래서 업로드 시 MIME type을 지정해주고 다시 확인해봤습니다.
![type=video/mp4](/images/ie10_video_tag_not_working (2).PNG)

이렇게 하고나니 IE10에서도 정상적으로 동영상이 실행되는 것을 확인할 수 있었습니다.

마지막으로 MIME type 에 대해 잘 정리된 링크
([MIME 타입 - HTTP | MDN](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types))를 남기고 마칠까합니다.

감사합니다.
