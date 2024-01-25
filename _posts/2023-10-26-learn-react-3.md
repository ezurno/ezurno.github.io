---
title: 🥜 [React] Lazy-Loading 알아보기
date: 2023-10-26 18:24:00 +0800
categories: [Study, Frontend]
tags: [React, lazy-loading]
---

> 해당 페이지는 lazy-loading 에 대해 알아보고
>
> 그에 따른 간단한 사용방법을 알아보는 페이지입니다.


## 왜?

현재 진행 중인 프로젝트에서 글 목록 기능을 구현하는데 글이 너무 많아

사용자가 원하는 만큼만 로딩하는 방법은 없을까 싶어 알아보게 되었다.

<br/>
<hr/>

## Lazy-Loading 이란?

<br/>

> 페이지를 불러오는 시점에 당장 필요하지 않은 리소스들을 추후에 로딩하게 하는 기술
{: .prompt-tip }

<br/>

일반적으로 페이지에 접근하면 페이지 내용이 모두 요청 된다.

사용자가 모든 페이지 내 모든 정보를 다 이용한다면 상관없지만

사용자들은 자기가 원하는 특정 정보를 얻기만 하고 나갈수도 있다.

따라서 그에 따른 쓸데없는 요청과 낭비가 이루어진다.

그러한 상황을 해결하기 위한 것이 `lazy-loading` 이라고 한다.

<br/>
<hr/>

## 구현 방법

> 우선적으로 사용자가 필요한 정보를 얻기 위해 스크롤을 내리므로
>
> 스크롤을 감지하고 있어야 한다.



```tsx
{% raw %}
  const [isLoading, setIsLoading] = useState<boolean>(false);
  const sentinel = useRef<HTMLDivElement | null>(null);
  // 맨 하단 component 의 ref

  useEffect(() => {
    const observer = new IntersectionObserver(
      (entries) => {
        if (entries[0].isIntersecting && !isLoading) {
            // 감지 했을 때의 로직 추가
            // setIsCounter((current) => current + 1);
        }
      },
      { threshold: 1.0 }
    );

    if (sentinel.current) {
      observer.observe(sentinel.current);
    }

    return () => observer.disconnect();
  }, []);
{% endraw %}
```

<br/>


> 현재 보여주고 있는 정보의 마지막 (sentinel) 에 달했을 때
>
> 새로 로딩 (loading) 을 해야한다.

```tsx
  useEffect(() => {
    const getResponse = async () => {
      setIsLoading(true);
      try {
        const response = await getNowPlayingList(isCounter);

        if (response.status === 200 && response.data.results) {
          setIsList((prev) => [...prev, ...response.data.results]);
        }
      } catch (error) {
        // 에러 처리
      } finally {
        setIsLoading(false);
      }
    };

    getResponse();
  }, [isCounter]);
  // counter 가 변경됐을 때 실행
  // getNowPlayingList는 page 를 number type 으로 가짐
```

<hr/>

## 장점

1. 사용자가 처음 웹사이트에 접근할 때 리소스의 일부만 다운로드 되기 때문에 콘텐츠의 제공 속도가 빠르다. 즉 성능이 향상된다.
2. 콘텐츠가 지속적으로 공급되기 때문에 사용자가 웹사이트를 이탈할 확률을 낮출 수 있다.
3. 사용자가 필요로 하는 경우에만 콘텐츠를 불러오기 때문에 배터리, 시간, 시스템 부담 등이 낮아진다. 즉 비용이 감소된다.

## 단점
1. 로딩 시간이 길수록 원하는 타이밍에 로딩을 마치지 못할 수도 있다.


<hr/>

## 확인하는 법

`Dev Tools -> Network -> img` 로 들어가 확인해보면 정상적으로 작동하는지 알 수 있다.

![image-main](../assets/img/2023-10-26/image-main.gif){: .w-50 }
