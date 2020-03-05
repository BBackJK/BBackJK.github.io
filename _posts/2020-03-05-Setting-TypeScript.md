---
title: "TypeScript Setting"
toc: true
toc_sticky: true
date: 2020-03-05 11:26:20 -0400
categories: TypeScript
tag:
  - TypeScript
---

> 해당 포스팅은 **alligator** 사의 **Setting Up a New TypeScript Project**을 번역한 내용입니다. 혹시 잘못된 번역이 있으면 댓글 남겨주시면 참고하겠습니다.

## Intro

starter project 혹은 Angualr CLI와 같은 도구를 이용할 때 TypeScript는 작업하기가 쉽습니다.

하지만 단순히 Vanilla JavaScript 으로만 이루어져 있는 프로젝트를 TypeScript 프로젝트로 작업하기 위해선 어떻습니까?

지금부터 시작하는 몇 가지 간단한 방법을 살펴보겠습니다.

## 의존성 (Dependencies)

첫 번째로, TypeScript가 설치되어 있어야 합니다.

여러분의 컴퓨터에 global로 설치하거나 프로젝트에 local로 설치하도록 결정할 수 있습니다.

먼저 global로 설치할 때,

```
// command line

$ npm i typescript -g


# or, using yarn:
$ yarn global add typescript
```

그리고 local로 설치할 때,

```
// command line

$ npm i typescript --save-dev

# or, using Yarn:
$ yarn add typescript --dev
```

## 설치 (Setup)

TypeScript는 두 가지 바이너리로 이루어져 있습니다: `tsc`와 `tsserver`.

**tsc**는 TypeScript 컴파일러 이며, 사용 가능한 옵션이 많은 command line 인터페이스를 가지고 있습니다.

TypeScript 프로젝트를 초기화하려면 --init 플래그를 사용합시다.

```
// command line

$ tsc --init
```

local에 설치된 TypeScript 버전을 사용하는 경우 node_modules 폴더에서 tsc를 호출하여 local 버전을 실행하고 있는지 확인하시면 됩니다.

```
// command line

$ ./node_modules/.bin/tsc --init
```

혹은 **npx**를 사용하여 local 버전의 tsc가 사용되도록 하는 것이 더 좋은 선택지가 될 수 있습니다.

```
// command line

$ npx tsc --init
```

**tsc**를 **--init** 플래그와 함께 실행시키면, **tsconfig.json**이 몇 가지 기본값과 주석 처리된 구성 목록으로 여러분의 프로젝트 폴더에 추가될 것입니다.

```typescript
//tsconfig.json
{
    "compilerOptions": {
        "target": "es5",
        "module":"commonjs",
        "strict": true
    }
}
```

기본 구성에 두가지 옵션을 추가해 봅시다.

```typescript
// tsconfig.json
{
    "compilerOptions": {
        "target": "es5",
        "module":"commonjs",
        "strict": true,
        "outDir": "dist",
        "sourceMap": true
    }
}
```

이를 통해 TypeScript 컴파일러가 출력하는 JavaScript 파일이 dist 폴더에 있고 sourcemap이 생성되었습니다.

## 컴파일링 (Compling)

tsconfig.json을 사용하면 TypeScript에서 App 코딩을 시작할 수 있습니다.

밑에 컨텐츠처럼 **src**폴더 안에 **index.ts**라는 파일을 생성해 봅시다.

```typescript
const world = "world";

export function hello(word: string = world): string {
  return `Hello ${world}! `;
}
```

이제 간단히 tsc를 실행하여 컴파일 할 수 있습니다.

```
// command line

$ tsc

# or, for local tsc:
$ npx tsc
```

그러고나면 bam, JavaScript 및 소스 맵 파일이 생성되었습니다.

컴파일 된 JavaScript의 내용은 다음과 같습니다.

```javascript
"use strict";
Object.defineProperty(exports, "__esModule", { value: true });
var world = "world";
function hello(word) {
  if (word === void 0) {
    word = world;
  }
  return "Hello" + world + "! ";
}
exports.hello = hello;
//# sourceMappingURL = index.js.map
```

### Watch mode

변경할 때마다 TypeScript 컴파일러를 실행하는 대신 TypeScript 파일이 변경될 때마다 다시 컴파일 되도록 컴파일러를 watch mode에서 시작할 수도 있습니다.

```
// command line

$ tsc -w

# or, for local tsc:
$ npx tsc -w
```

## tslint

코딩을 할 때 불일치, 구문 오류 및 누락에 대해 빠르게 알아야할 때 린터를 사용하세요.

실제로 TypeScript의 인터페이스는 tslint입니다.

계속해서 프로젝트에 tslint를 설치 / 구성 합시다.

npm을 사용하여 다음과 같이 명령줄을 실행하세요!

```
// command line

# for installing globally:
$ npm i tslint --g

# for installing locally:
$ npm i tslint --save-dev
```

혹은 Yarn을 사용한다면?

```
// command line

# global:
$ yarn global add tslint

# or local:
$ yarn add tslint --dev
```

**tslint** 설치하고, 여러분은 **--init** 플래그를 사용하여 초기화할 수 있습니다.

```
// command line

# if using global tslint:
$ tslint --init

# if using local tslint:
$ npx tslint --init
```

그러면 다음과 같은 기본 구성값이 있는 **tslint.json** 파일이 여러분의 프로젝트 안에 추가되어 있을 것입니다.

```typescript
// tslint.json
{
  "defaultSeverity": "error",
  "extends": [
    "tslint:recommended"
  ],
  "jsRules": {},
  "rules": {},
  "rulesDirectory": []
}
```

이제 코드 편집기에 tslint 확장을 설치하여 코딩할 때 보푸라기 오류를 즉시 확인할 수도 있습니다. 이 작업을 완료한 후 편집기를 다시 시작해야할 수도 있습니다.

tslint는 위의 간단한 예제코드를 사용하여 인용 부호가 큰 따옴표 (") 여야하고 파일이 줄 바꿈으로 끝나야 한다고 불평합니다.

작은 따옴표를 사용하고 파일 끝에 줄을 추가하지 않고 tslint 구성에 두 가지 규칙을 추가하여 이를 변경할 수도 있습니다.

```typescript
// tslint.json
{
    "defaultSeverity": "error",
    "extends": [
        "tslint:recommended"
    ],
    "jsRules": {},
    "rules": {
        "eofline": false,
        "quotemark": [
            true,
            "single"
        ]
    },
    "rulesDirectory": []
}
```

### tslint를 위한 Airbnb 스타일 가이드

규칙을 수동으로 추가하는 것은 확실히 재미가 없기 때문에 가장 널리 알려진 기본 구성을 사용하는 것이 가장 쉬운 방법입니다.

그 방법이 바로 airbnb 의 구성 중 하나 입니다.

그럼 바로 프로젝트에 설치해 보겠습니다.

```
// command line

$ npm install tslint-config-airbnb

# or, using Yarn:
$ yarn add tslint-config-airbnb
```

이제 tslint 구성을 변경하여 airbnb 구성을 대신 확장할 수 있습니다.

```typescript
// tslint.json
{
    "defaultSeverity": "error",
    "extends": "tslint-config-airbnb",
    "jsRules": {},
    "rules": {
        "eofline": false
    },
    "rulesDirectory": []
}
```

> airbnb는 이미 작은 따옴표에 대한 규칙을 가지고 있기 때문에 작은 따옴표 규칙을 어떻게 제거했는지 확인하여라!

## 더 쉽게 일 하기 : gts

이제 대부분의 빌딩 블록이 어떻게 결합되는지 이해 했으므로 바로 가기를 수행하고 linting 및 tsconfig.json 파일을 설정하지 않아도 된다.

**Google TypeScript Style(gts)**는 새로운 TypeScript 프로젝트를 보다 쉽게 bootstrap 하고, bikeshedding을 피하고, 기본 설정을 적용할 수 있는 프로젝트입니다.

새 프로젝트를 시작하려면 새 폴더에서 이 명령을 실행하기만 하면 끝!

```
// command line

$ npx gts init
```

> npm >= 5.3 버전 이어야 하며 npx와 자동으로 번들로 제공된다.

이 명령은 tsconfig.json 및 linting 설정을 시작하는 데에 필요한 모든 것을 생성합니다.

프로젝트의 package.json 파일이 없는 경우에도 생성합니다.

여러분은 종속성을 간단히 설치할 수 있습니다.

```
// command line

$ npm install

# or, using Yarn:
$ yarn
```

**gts**는 프로젝트의 package.json 파일에 편리한 npm 스크립트를 추가합니다.

예를 들어, 프로젝트를 컴파일 하려면 간단히 `npm run complie`을 실행하고 linting 오류를 확인하려면 `npm run check`를 실행하면 됩니다.

tslint를 편집기와 함께 사용하려면 gts의 tslint 구성을 확장하는 tslint.json 파일을 프로젝트에 수동으로 추가해야 한다.

```typescript
// tslint.json
{
  "defaultSeverity": "error",
  "extends": [
    "./node_modules/gts/tslint.json"
  ],
  "jsRules": {},
  "rules": {},
  "rulesDirectory": []
}

```

> **gts**는 아직 많이 개발 중이며 이 글을 쓰는 시점에 안정적인 버전에 도달하지 않았으므로 신중하게 스레드하면 좋을 것 같다!

이제 TypeScript를 쉽게 시작할 수 있습니다.

다음 포스트에서는 웹팩을 믹스에 넣는 방법을 살펴 보겠습니다!

## 마무리

이 포스팅을 번역하면서 typescript의 기본 구조? 어떻게 컴파일링이 이루어지는지 확인할 수 있었다.

빨리 내 개인 프로젝트에 typescript를 도입해보고 싶다.
