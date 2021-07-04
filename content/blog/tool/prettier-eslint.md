---
title: Prettier + Eslint
date: 2021-03-13 14:41:75
category: tool
description: prettier와 eslint를 사용해야하는 이유와 적용 방법을 알아보자
thumbnail: { thumbnailSrc }
draft: false
---

## 개요

Prettier와 Eslint를 도입해야하는 배경은 아래와 같다.

프로젝트를 유지보수하는데 투자되는 비용을 최소화하기 위해 통일된 코드 작성법을 제시한다.

포멧팅 관련된 부분에 대한 논쟁을 없애어 각 프로젝트들의 개발 생산성을 높히도록 한다.
인계자 또는 최초 개발자가 아닌 사람도 코드를 빠르고 정확하게 이해할 수 있도록 한다.

## Eslint 란?

ESLint는 ES + Lint의 합성어로 EsmaScript문법에 에러가 있는 코드에 표시를 달아 놓는 것을 의미한다.

즉 ESLint는 JavaScript의 스타일 가이드를 따르지 않거나 문제가 있는 안티 패턴들을 찾아주고 일관된 코드 스타일로 작성하도록 도와준다.

코딩 컨벤션 및 안티 패턴을 자동 검출 하므로 휴먼 에러를 방지할 수 있고, 코드 일관성을 지킬 수 있다. 또한 코드 리뷰에도 큰 도움이 된다.

## Prettier 란?

Prettier는 Code Formatter이다. 개발자들에게 일관적인 코딩 스타일을 유지할 수 있게 도와주는 툴이다.

예를 들면, 아래와 같은 코드를

```javascript
// prettier-ignore
foo(gatsbyLongArg(),soManyParameters(),gatsbyInit(),gatsbyMustUsedIt(), gatsbyPrettierConfigThis())
```

다음과 같이 변경시킨다.

```javascript
foo(
  gatsbyLongArg(),
  soManyParameters(),
  gatsbyInit(),
  gatsbyMustUsedIt(),
  gatsbyPrettierConfigThis()
)
```

EsLint와 다른점은 Eslint는 문법에러를 잡아주거나, 더 좋은 문법을 사용하게 에러표기를 강제해주는 툴이지만, Prettier는 코드의 퀄리티가 아닌 스타일을 교정해준다.

자간, `""` 를 `''`으로 바꿔주거나, 길이가 너무 긴 코드를 자동으로 줄넘김 해주는등의 기능을 한다.

`Eslint`는 적용한다면 코딩의 결과가 바뀌기도 하지만, `Prettier`는 단순히 스타일을 교정해주기 때문에 결과에는 영향이 없다.

단순히 저장만 하면 코드가 자동으로 포맷팅이 되는 간단한 사용법을 가지고 있다.

## 적용

프로젝트 디렉토리의 터미널에서 다음 명령어를 입력한다.

## eslint 모듈 설치

`npm i eslint --save-dev`

## prettier 모듈 설치

`npm i prettier --save-dev`

## eslint 설정을 생성해보자

eslint 설치가 끝났다면 설정을 해야한다. 아래 명령어는 eslint 설정을 보다 쉽게 해준다.

`node_modules/.bin/eslint --init`

명령어를 입력했다면 차례로 질문이 나온다. `react + typescript`를 가정하고 설정해보겠다.

### 질문리스트

#### ✔ Q: How would you like to use ESLint? · A: To check syntax and find problems

#### ✔ Q: What type of modules does your project use? · A: JavaScript modules (import/export)

#### ✔ Q: Which framework does your project use? · A: react

#### ✔ Q: Does your project use TypeScript? · A: No / Yes

#### ✔ Q: Where does your code run? · A: node

#### ✔ Q: How would you like to define a style for your project? · A: guide

#### ✔ Q: Which style guide do you want to follow? · A: airbnb

#### ✔ Q: What format do you want your config file to be in? · A: JavaScript

설정을 완료하면 `.eslintrc.js`가 생성되며, 수정 및 추가할 수 있다.

```javascript
module.exports = {
  env: {
    // 사용환경
    es2021: true,
  },
  extends: ['plugin:react/recommended', 'airbnb'], // eslint rule airbnb가 가장 대중적
  parser: '@typescript-eslint/parser', // typescript 및 jsx(react)지원을 위한 옵션
  parserOptions: {
    ecmaFeatures: {
      jsx: true,
    },
    ecmaVersion: 12,
    sourceType: 'module',
  },
  plugins: ['react', '@typescript-eslint'],
  rules: {}, // rule을 off 하고 싶은 예외 경우
}
```

## Prettier 옵션

prttier은 비교적 setting이 간단하기에 project root에 `pretteir.config.js` 를 생성해서 사용하면 되겠다.

아래는 추천하는 prettier 옵션이다.

```
module.exports = {
  printWidth: 100,
  tabWidth: 2,
  useTabs: false,
  semi: true,
  singleQuote: true,
  jsxSingleQuote: true,
  trailingComma: 'all',
  bracketSpacing: true,
  arrowParens: 'always',
};
```

## Prettier + Eslint 같이 사용하기

이 둘을 함께 사용하려면 두가지 모듈을 설치 해야한다.

#### `eslint-config-prettier`: eslint와 prettier가 충돌할 설정들을 비활성화한다. </li>

#### `eslint-plugin-prettier`: 코드 코맷할 때 Prettier를 사용하게 만드는 규칙을 추가한다. </li>

`$ npm i eslint-plugin-prettier eslint-config-prettier -D`

아까 만들었던 `eslintrc.js`에 prettier 관련 설정을 추가한다.

```javascript
module.exports = {
  env: {
    es2021: true,
  },
  extends: [
    'plugin:react/recommended',
    'airbnb',
    'prettier', // new
    'prettier/@typescript-eslint', // new
    'prettier/react', // new
  ],
  parser: '@typescript-eslint/parser',
  parserOptions: {
    ecmaFeatures: {
      jsx: true,
    },
    ecmaVersion: 12,
    sourceType: 'module',
  },
  plugins: ['react', '@typescript-eslint'],
  rules: {
    'prettier/prettier': ['error'], // new
  },
}
```

## extension 설치

vscode, web storm 등 사용하는 ide에서 prettier 및 eslint를 설치한다.

## Husky & lint-staged

lint-staged는 현재 git 상태에서 commit을 대기 중인 staged상태만 lint를 check해주는 도구이다.

현재 작업중인 무수히 많은 파일이 있는데, lint를 모두 체크한다면, 현재 작업중인 파일과 상관없는 파일도 lint rule대로 변경될 것이다.

이런 것을 방지하기 위해 나온툴이며, git hook을 손쉽게 제어하기 위한 husky와 같이 사용하면 좋다.

husky+lint-staged를 활용한다면, commit과 push 단계에서 lint검사를 하게 되며, lint rule을 검증한 코드만 github, gitlab등 remote 저장소에 올라갈 수 있다.

프로젝트에서 사용하고 있는 hook은 다음과 같다.

```javascript
"husky": {
 "hooks": {
 "pre-commit": "lint-staged",
 "pre-push": "yarn lint"
 }
},
```

## Reference

https://pravusid.kr/javascript/2019/03/10/eslint-prettier.html
https://prettier.io/
https://www.huskyhoochu.com/npm-husky-the-git-hook-manager/
