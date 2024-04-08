---
title: 🥜 [JavaScript] 정규표현식에 대해 알아보자
date: 2024-04-08 08:00:00 +0800
categories: [Frontend, JavaScript]
tags: [JavaScript, 정규표현식]
toc: true
---

## 개요

여태껏 정규표현식은 `validation` 을 적용할 때 밖에 써보지 않았다.

하지만 요즘 `javascript` 로 코딩테스트를 준비하다 보면

정규표현식을 사용하는 일이 잦은 것 같아 제대로 알아보려 한다.

<br/>
<hr/>

## 정규표현식이란?

> 정규표현식 (RegExp, Regular Expression)
>
> 문자를 검색하거나 대체, 추출 할 때 사용하는 일종의 패턴
{: .prompt-tip}

쉽게 말해 문자열에 쉽게 접근할 수 있는 패턴이라고 보면 된다.

<br/>
<hr/>

## 사용 방법

정규표현식은 크게 두 가지 방법이 있는데 `생성자 방식`과 `리터럴 방식`이 있다.

```js
// 1. 생성자 방식

new RegExp("표현", "옵션");
new RegExp("[a-z]", "gi");

// 2. 리터럴 방식

/표현/옵션
/[a-z]/gi
```

여기서 먼저 `생성자 방식`으로 알아보자

### 생성자 방식

```js
const str = `
010-1234-5678
thesecond@gmail.com
hello world!
https://ezurno.github.io/
The quick brown fox jumps over the lazy dog.
`;

const reg = new RegExp("the", "");
// 변경이 될 부분
console.log(str.match(reg));
```

이러한 함수가 존재한다고 치자

해당 함수를 동작시키면 콘솔에서는

```console
["the", index: 15, input: ~~~~] //[`찾은 값`, `값의 위치`, `입력한 값`]
```

이렇게 로그가 찍혀나오는데 각각 `찾은 값`, `값의 위치`, `입력한 값` 으로

배열 데이터로 나타난다.

그럼 이번엔 옵션 데이터에 `g` 를 추가 해보자

```js
const reg = new RegExp("the", "g");
console.log(str.match(reg));

// ["the", "the"]
// 매칭 된 데이터들을 배열로 반환
//  단 대소문자 구별을 하므로 The 는 매칭되지 않음
```

그럼 이번엔 대소문자 구분을 하지 않을려면 어떻게 해야할까?

간단하게 옵션 데이터에 `i` 를 추가하면 된다.

```js
const reg = new RegExp("the", "gi");
console.log(str.match(reg));

// ["the", "The", "the"]
// 매칭 된 데이터들을 배열로 반환
```

<br/>
<hr/>

### 리터럴 방식

이러한 정규표현식을 생성할 때, `리터럴 방식`을 사용하면 더 간단하게

코드를 작성할 수 있다.

```js
// 1) const reg = new RegExp("the", "g");
const reg = /the/g;

// 2) const reg = new RegExp("the", "gi");
const reg = /the/gi;
```

그럼 이번에는 정규표현식에서 주로 사용하는 함수를 알아보자

<br/>
<hr/>

### 정규표현식 함수

자주 사용하는 함수는 크게 3가지가 있다.

|test|match|replace|
|:---|:----|:------|
|일치여부 반환|일치하는 문자 배열 반환|일치하는 문자를 대체|
|정규식|문자열|문자열|

`test` 는 정규식에 사용하고

`match`, `replace` 는 문자열에 사용하는 함수다.

```js
const str = `
010-1234-5678
thesecond@gmail.com
hello world!
https://ezurno.github.io/
The quick brown fox jumps over the lazy dog.
`;

const reg = /fox/gi;
console.log(reg.test(str)); // false
console.log(str.match(reg)); // ["fox"]
console.log(str.replace(reg, "cat")); // fox 를 cat 으로 교체
```

<br/>
<hr/>

### 플래그

> 정규표현식을 사용할 때 옵션 데이터에 추가하는 값
{: .prompt-tip}

이러한 플래그에는 3가지가 있다.

|g|i|m|
|:-|:-|:-|
|모든 문자 일치|영어 대소문자를 구분하지 않고 일치 |여러줄 일치, 각각 줄을 시작과 끝으로 인식|

<br/>

플래그를 사용하기 전에 먼저 `escape-character` 에 대해 알아보고 들어가려한다.

> escape-character
>
> 정규식이 가지고 있는 기본적인 기능을 탈출해 문자로서의 기능만을 사용하는 문자
{: .prompt-info}

시작으로는 `\`, 끝으로는 `$` 를 사용해 나타낸다.

```js
// \$ 를 사용
console.log(str.match(/\.$/gi));
// . 을 찾는다는 의미
```

```js
const str = `
010-1234-5678
thesecond@gmail.com
hello world!
https://ezurno.github.io/
The quick brown fox jumps over the lazy dog.
`;

console.log(str.match(/the/)); // the 의 인덱스 및 정보 배열
console.log(str.match(/the/g)); // the 일치
console.log(str.match(/the/gi)); // 대소문자를 구분하지 않고 the 와 일치
console.log(str.match(/\.$/gi)); // 이스케이프 값으로 . 을 찾음
console.log(str.match(/\.$/gim)); // 줄을 나눠서 . 을 찾음
```

<br/>
<hr/>

### 패턴

```js
^ab     // 줄 시작에 있는 ab 와 일치
ab$     // 줄 끝에 있는 ab 와 일치
.       // 임의의 한 문자와 일치
a|b     // a 또는 b 와 일치
ab?     // b 가 없거나 b 와 일치
{3}     // 3개 연속 일치
{3, }   // 3개 이상 연속 일치
{3, 5}  // 3개 이상 5개 이하 일치
+       // 1회 이상 연속 일치 {1, }

[ab]    // a 또는 b
[a-z]   // a 부터 z 간의 문자 구간에 일치
[A-Z]   // A 부터 Z 간의 문자 구간에 일치
[0-9]   // 0 부터 9 까지의 숫자 구간에 일치
[가-힣] // 한글

\w      // 63 개의 문자(대소영문 52개 + 숫자 10개 + _)와 일치
\b      // 64 개의 문자와 일치하지 않는 문자 경계 (boundary)
\d      // 숫자에 일치 (digit)
\s      // 공백 (space, tab) 등에 일치

(?:)    // 그룹 지정
(?=)    // 앞쪽 일치
(?<=)   // 뒷쪽 일치
```

등이 있다.

## 마치며...

정규표현식... 생각보다 쓰기는 편해서 좋았는데

평소에 보지 못했던 문법도 처음 보게 되어 생각보다 디테일 하다는 것을 알게 되었다.

앞으로 정규표현식을 사용해서 문자열을 좀 더 쉽게

관리할 수 있을 것 같다. ~~편하네~~