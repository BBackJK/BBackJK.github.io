---
title: "Why Typescript ?"
toc: true
toc_sticky: true
date: 2020-03-04 12:09:20 -0400
categories: TypeScript
tag:
  - TypeScript
---

> 해당 포스팅은 **alligator** 사의 **Benefits of Using TypeScript**을 번역한 내용입니다. 혹시 잘못된 번역이 있으면 댓글 남겨주시면 참고하겠습니다.

## Intro

저는 몇 년 전에 Angular가 주요 버전 간에 typescript가 어떻게 바뀌었는지 이해하려고 노력했습니다.

여러분도 알다시피, Angular framework의 첫번째와 두번째 버전 사이의 변화는 큰 변화가 있었습니다. 그래서 저는 그 변화를 시도해보았습니다.

모든 것이 TypeScript로 작성되었지만 여러분처럼 왜? 그런지 잘 몰랐습니다. JavaScript의 superset(상위 집합 - TypeScript)을 사용할 때 어떤 이점이 있는지 알아봅시다.

## Typing

여러분도 알다시피, **JavaScript는 type을 가지고 있지 않습니다.** 그래서 우리가 사용하고 있는 모든 변수들과 그 변수들을 통제하고 검증하는 것은 매우 어렵습니다.

이 점은 여러분의 코드에서 실수를 너무나도 쉽게 유발할 수 있다는 것입니다. 변수를 선언하는 것을 잊거나, 존재하지 않는 기능을 변수라고 부르거나, 모든 코드를 깨트릴 변수를 매개 변수로 전달하는 것처럼 말이죠.

그래서 우리는 이렇게 말합니다. **TypeScript는 type을 가지고 있는 JavaScript와 같다.**

이 점은 코드를 쉽게 읽을 수 있게 만들어 주고 디버깅 악몽을 불러일으키는 에러를 피할 수 있습니다.

자, 그렇다면 JavaScript가 TypeScript로 어떻게 변환하는지 예를 보겠습니다.

```javascript
// alligators-service.js
class AlligatorsService {
    public alligators = [];

    public addAlligator(alligator) {
        if (this.isValis(alligator)) {
            alligators.push(alligator);
        }
    }

    private isValid(alligator) {
        return alligator.name;
    }
}
```

```javascript
// alligators-service.ts
class AlligatorsService {
    public alligators: Alligator[] = [];

    public addAlligator(alligator: Alligator): void {
        if (this.isValid(alligator)) {
            alligators.push(alligator);
        }
    }

    private isValid(alligator: Alligator): boolean {
        return alligator.name;
    }
}
```

여기서, Alligator는 어디에서나 정의될 수 있고 우리 파일로 가져올 수 있는 인터페이스입니다. 이 인터페이스는 Alligator type의 객체에 대한 shape을 정의합니다.

강조 표시된 코드에서 볼 수 있듯이, parameter와 return type에 대한 설명을 추가했습니다.

이 점은 여러분에게 더 많은 맥락을 가져다 주고, TypeScript 컴파일러가 여러분의 코드를 변환할 때, 잘못된 장소에서 잘못된 유형을 사용한다면 여러분에게 오류를 통지할 것입니다.

## 최신 Javascript 기능 지원

TypeScript의 또 다른 멋진 점은 코드에 **JavaScript의 최신 기능을 사용**할 수 있다는 점입니다.

우리가 최신 기능을 사용한다면 모든 최신 브라우저가 우리의 코드를 이해할 수 있는 것은 아니며, 가능하면 Babel과 같은 추가 tool을 사용해야 한다. 그러나 TypeScript를 사용하면 컴파일러가 모든 힘든 일을 할 것입니다.

TypeScript는 **npm**을 통해 프로젝트에 설치할 수 있는 패키지로, 버전을 계속 업데이트하면 자동으로 모든 새로운 기능을 사용할 수 있게 됩니다.

> 컴파일러는 여러분의 코드를 JavaScript로 변환하고 있으므로, 여러분은 클라이언트와 서버, 양쪽에서 TypeScript를 사용할 수 있습니다!

## IDE 지원

대부분 최신 IDEs는 코딩하는 동안에 여러분을 도와줍니다.

TypeScript는 typed language이기 때문에, 아래에 보이는 이미지와 같이 IDE는 여러분에게 몇 가지 코드를 암시할 것입니다.

![](https://BBackJK.github.io/assets/images/typescript-benefit-IDE-support.png){: .align-center}

## 브라우저 호환성

브라우저 호환성은 제(원 글쓴이)가 가장 좋아하는 특징입니다.

IE와 여러분의 코드와의 호환성에 대한 문제는 잊어버리고, 컴파일러는 여러분의 코드를 변형시키고 모든 최신 브라우저와 호환되도록 약간의 마술을 부립니다.

즉, 기본적으로 **TypeScript 컴파일러에서 꺼내는 코드는 ES5 호환**이며, 모든 최신 브라우저들은 JavaScript의 ES5를 이해합니다.

## Outro

이 글을 번역하면서 사람들이 왜 TypeScript에 열광하며, 많이 사용하는지를 전체적으로 파악할 수 있게 되었다.

왜 사용하는지 알았으니 다음 포스팅은 프로젝트에 TypeScript를 셋팅하는 법을 알아보겠다.

> 출처 <https://alligator.io/typescript/typescript-benefits/>
