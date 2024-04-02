---
title: 🌰 [React] SVG 이미지를 통해 404 page 구축
date: 2024-04-02 08:33:00 +0800
categories: [Frontend, React]
tags: [React, react-router-dom, Frontend]
---

평소에 이미지를 넣다보면 확장자가 `svg` 인 파일을 볼 수 있다.

`png`, `jpg` 등 여러 확장자가 있지만 유독 아이콘 부분에서는 `svg` 를 사용을 많이 하는 것 같다.

따라서 이번 페이지에서는 `svg` 에 대해 자세히 알아보고 `svg` 를 통해

한 이미지로 **404 페이지 핸들링** 하는 것을 목표로 하려 한다.

## SVG 란?

> **Scalable Vector Graphics** 의 약자, 벡터 기반 그래픽 파일 형식
{: .prompt-tip}

XML 기반 파일으로 메모장과 같은 문서 편집기로 편집이 가능하다.

***크기를 조절해도 품질이 저하되지 않아 화질이 깨지지 않는다*** 라는 특징이 있는데

여기서 벡터기반 이미지가 무엇인지에 대해 알아보자

## Vector vs Raster

| Vector                      | Raster| 
| :--------------------------- | :--------------- | 
| 수학 공식을 통해 컴퓨터가 랜더링          | 픽셀로 구성     |
| 로고, 아이콘에 적합               | 사진에 적합    |
| EPS, SVG, AI | GIF, JPG, PNG |

- `Raster` 는 픽셀 하나하나가 이루어져 있어 크기가 정해져 있어 동적이지 않음
- `Vector` 는 직접 그리는 방법을 벡터이미지를 통해 그리는 것으로 사이즈에 제약되지 않음
- 하지만 너무 복잡한 이미지는 `Vector` 이미지에 적합하지 않으며 `Raster` 가 더 유리

<br/>

> 처음엔 `Vector` 이미지의 설명만 듣고
>
> 그럼 왜 고화질 사진에는 `Vector` 이미지를 사용하지 않지 싶었는데
>
> 로고나 아이콘처럼 단순한 이미지가 아니면 그리는데 오래 걸려서 오히려 성능이 저하 된다고 한다
>
> 서로 장단점이 명확했다.
>
> 그래서 사진은 `Raster`, 아이콘은 `Vector` 를 자주 쓰는구나

<hr/>

## SVG 에 애니메이션 적용하는 방법

방법은 생각보다 간단했다..

```html
<circle id="star_4" cx="565" cy="1073" r="9" fill="white" />
```

`svg` 는 이런식으로 구성 되어 있는데, 해당 태그들의 `id`, `class` 명을 주어

일반 `css` 처럼 애니메이션을 추가해주면 되는 것 이었다.

```css
#planet_1 {
  animation-name: rotation;
  animation-duration: 3s;
  animation-timing-function: linear;
  animation-iteration-count: infinite;
  transform-box: fill-box;
  transform-origin: center;
}

#number-0 {
  animation: appearFromBottom 3s;
  animation-timing-function: cubic-bezier(0.79, 1.31, 0.82, -0.36);
}
```

여기서 `animation-timing-function` 에 준

`cubic-bezier` 란 뭘까?


## cubic-bezier 란?

베지어 곡선을 정의하는 함수

[페이지를 참고](https://cubic-bezier.com/#.17,.67,.83,.67) 하자

> 컴퓨터 그래픽 등에서 사용되는 매개변수 곡선
>
> - 부드러운 곡선을 만드는데에 사용
> - 피에르 베지에가 1960년대 차체 곡선 제작에 사용
> - 폰트, 애니메이션 등에 자주 사용
{: .prompt-tip}



<br/>
<hr/>

## 후기

![image-main](../assets/img/2024-04-02/image-01.gif){: .w-50 }
_(리소스 출처 : 패스트캠퍼스)_

정말 귀여운 404 page 를 만들었다!

~~여태껏 애니메이션을 만들려면 디자이너들이 만들어줘야 하는 줄 알았는데...~~

`vector` 이미지를 활용하면 하나의 이미지로 애니메이션을 만들 수 있다는 점에 대해

충격을 먹었다...

앞으로도 `svg` 를 더 애용하는 계기가 될 것 같다.