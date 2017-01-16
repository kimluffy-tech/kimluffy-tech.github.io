---
layout: post
title:  "공유 콘텐츠 캐싱"
---
# 목표
- SNS에 URL을 공유 시 노출되는 콘텐츠를 변경 후 캐시 관리

# 시작하며
운영 중인 사이트에서 새로운 이벤트 페이지를 오픈했습니다.
해당 페이지에서 SNS 공유 기능을 필요로 하지 않아 넣지 않은 상태였는데요.

>"사용자가 해당 페이지를 공유했을 때 불러온 이미지,타이틀,Description 을 변경하고 싶다."

는 요청사항을 접수하였습니다.

# 해결 방법
## 1.페이스북(Facebook)
- [웹마스터 공유 가이드](https://developers.facebook.com/docs/sharing/webmasters) 를 참고하여 open graph meta tags를 입력해줍니다.

```html
<meta property="og:url" content="http://www.nytimes.com/2015/02/19/arts/international/when-great-minds-dont-think-alike.html" />
<meta property="og:type" content="article" />
<meta property="og:title" content="When Great Minds Don’t Think Alike" />
<meta property="og:description" content="How much does culture influence creative thinking?" />
<meta property="og:image" content="http://static01.nyt.com/images/2015/02/19/arts/international/19iht-btnumbers19A/19iht-btnumbers19A-facebookJumbo-v2.jpg" />
```

- 페이스북에서는 [Sharing Debugger](https://developers.facebook.com/tools/debug/sharing/) 를 제공합니다.
해당 페이지에서 SNS에 공유하려는 페이지 URL을 입력 후 **디버그** 합니다.

## 2.트위터(Twitter)
- [Summary Card](https://dev.twitter.com/cards/types/summary) 를 참고하여 meta 태그(tags)를 입력해줍니다.

```html
<meta name="twitter:card" content="summary" />
<meta name="twitter:site" content="@flickr" />
<meta name="twitter:title" content="Small Island Developing States Photo Submission" />
<meta name="twitter:description" content="View the album on Flickr." />
<meta name="twitter:image" content="https://farm6.staticflickr.com/5510/14338202952_93595258ff_z.jpg" />
```

- 트위터에서는 [Card Validator](https://cards-dev.twitter.com/validator) 를 제공합니다.
해당 페이지에서 SNS에 공유하려는 페이지 URL 을 입력 후 **Preview card** 합니다.

## 3.링크드인(LinkedIn)
- [Shared on LinkedIn](https://developer.linkedin.com/docs/share-on-linkedin) 을 참고하여 open graph meta tags 를 입력해줍니다.

```html
<meta property="og:title" content="My Shared Article Title" />
<meta property="og:description" content="Description of shared article" />
<meta property="og:url" content="http://example.com/my_article.html" />
<meta property="og:image" content="http://example.com/foo.jpg" />
```

- 링크드인에서는 페이스북의 Sharing Debuuger, 트위터의 Card Validator 와 같이 Preview(캐시 갱신 방법)를 제공하지 않습니다.
[Shared on LinkedIn](https://developer.linkedin.com/docs/share-on-linkedin) 페이지의 **Shared Content Caching** 항목을 요약해보면
>The first time that LinkedIn's crawlers visit a webpage when asked to share content via a URL, the data it finds (Open Graph values or our own analysis) will be cached for a period of approximately 7 days.

링크드인의 크롤러가 최초에 수집한 데이터를 캐시로 **약 7일간 유지** 하게 됩니다.

**하지만 방법은 있습니다.** 예를 들어 공유하려는 페이지의 URL 이 http://example.com 이고 이미 크롤러가 최초에 수집한 데이터를 캐시하고 있다면,

http://example.com?1 과 같이 파라미터로 versin을 추가하여 링크드인에 공유하기를 시도하면 링크드인 크롤러가 데이터를 재수집하게 됩니다.
