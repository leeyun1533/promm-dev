---
title: Typescript Class
date: 2021-03-13 14:03:75
category: typescript
description: typescript의 class부분을 공부하고 작성한 글이다.
thumbnail: { thumbnailSrc }
draft: false
---

![typescript-in-react](../assets/typescript-in-react.png)

## 개요

Typescript 스터디에서 Class 부분을 담당하게 되었다.
객체지향 패턴에서 Class 대한 개념을 정리하고 Typescript의 Class를 알아본다.

## Class 란?

Typescript Class를 들어가기 앞서 한번 Class 개념 자체에 대해 짚어보는 시간을 가지자.
굳이 넣을 필요가 없긴한데. 공부삼아 한번 정리 해보았다.
Class란 무엇일까? CS 전공하신분들이라면 오히려 잘 아실 것 같다.. Java, C++등 객체지향언어에서 주구장창 나오는 개념이다.

위키 백과에서 정의하는 Class는 OOP(객체 지향 프로그래밍)에서 특정 객체를 생성하기 위해 변수와 메소드를 정의하는 틀이라고 한다.
그럼 OOP는 뭘까?

## OOP란?

OOP란 Object Oriented Programming … Node의 정의를 두고 사람들이 다 말하는게 다르지만, 홈페이지에 써있듯 Node는 Javascript 런타임이다.

OOP도 비슷하게 여러 사람들이 각자의 정의를 내리지만, 원래 정확한말은 캡슐화, 다형성, 상속을 이용하여 코드 재사용을 증가시키고, 유지보수를 감소시키는 장점을 얻기위해 객체들을 연결 시켜 프로그래밍 하는 것이다.

이 때 객체들의 기본 형태를 잡아주는게 Class이다.

<bold> Class란 객체를 정의하는 틀 또는 설계도 </bold>

그래서 이 말이 Class에 가장 잘 어울리는 말이라 생각한다.

![class](../assets/class.png)

예를 들면, 사람 Class를 인스턴스화해서 박보영이라는 인물로 실체화하는 것이다. (코딩을 잘하면 멋있는 결과물을!)

## Typescript Class

본론으로 돌아와서, 진짜 Typescript Class이다. 핸드북에 있는 내용을 기본으로 했고, 부록정도를 설명하려한다.
현엽에서는 생각보다 Class를 사용할 일이 없었는데, 함수형 프로그래밍을 추구해서 그랬던 것 같기도하다.
이번 기회에 Class에 대해 확실히 알고 조금 더 유틸등을 만들 때 활용하는 계기가 되면 좋겠다.

## Class

```javascript
class Greeter {
  greeting: string
  constructor(message: string) {
    this.greeting = message
  }
  greet() {
    return 'Hello, ' + this.greeting
  }
}

let greeter = new Greeter('world')
```

C# 이나 Java를 사용해봤다면, 익숙한 구문일 것이다. 새로운 클래스 Greeter를 선언했다. 이 클래스는 3개의 멤버를 가지고 있다 greeting 프로퍼티, 생성자 그리고 greet 메서드 이다.

클래스 안에서 클래스의 멤버를 참조할 때 this.를 앞에 덧붙이는 것을 알 수 있다. 이것은 멤버에 접근하는 것을 의미한다.

마지막 줄에서, new를 사용하여 Greeter클래스의 인스턴스를 생성한다. 이 코드는 이전에 정의한 생성자를 호출하여 Greeter 형태의 새로운 객체를 만들고, 생성자를 실행해 초기화한다.

## Inheritance

```javascript
class Animal {
  move(distanceInMeters: number = 0) {
    console.log(`Animal moved ${distanceInMeters}m.`)
  }
}

class Dog extends Animal {
  bark() {
    console.log('Woof! Woof!')
  }
}

const dog = new Dog()
dog.bark()
dog.move(10)
dog.bark()
```

TypeScript에서는, 일반적인 객체-지향 패턴을 사용할 수 있다. 클래스-기반 프로그래밍의 가장 기본적인 패턴 중 하나는 상속을 이용하여 이미 존재하는 클래스를 확장해 새로운 클래스를 만들 수 있다는 것이다.
`dog`는 `bark`라는 메소드 밖에 가지고 있지 않지만, `Animal`을 상속했기에 움직일 수 있다. 동물 -> 강아지

## Private

접근제어자가 private으로 설정되었다면 private 이 붙은 변수, 메소드는 해당 클래스에서만 접근이 가능하다.

```javascript
class Person {
    private ssn: string;
    private firstName: string;
    private lastName: string;
    // ...
}
```

오직 Person 클래스에서만 접근이 가능하고 다른 클래스에서는 접근이 불가능하다.

더 상세한 예제를 알아보자. Person Class를 구체화한다.

```javascript
class Person {
    private ssn: string;
    private firstName: string;
    private lastName: string;

    constructor(ssn: string, firstName: string, lastName: string) {
        this.ssn = ssn;
        this.firstName = firstName;
        this.lastName = lastName;
    }

    getFullName(): string {
        return `${this.firstName} ${this.lastName}`;
    }
}
```

ssn을 외부에서 사용하려 하면 아래와 같이 `compile error`가 발생한다.
만약 정상적으로 사용한다면, `ssn`에 대한 `getter`를 생성해줘야 할 것 이다.

```javascript
let person = new Person('153-07-3130', 'John', 'Doe')
console.log(person.ssn) // compile error
```

아래 `Accessors`에서 조금 더 이야기하겠지만, private을 활용해 캡슐화 한다면, 다음과 같은 장점이 있다.

- 외부에 불필요한 정보 제공 X
- 유지보수의 편리
- 자료 보호

외부에 불필요한 정보를 제공하지 않는다는 것은 왜 중요할까?
간단히 설명하면, 우리가 만약 애플스토어에 간다면, 원하는 제품을 고르고 돈을 건낸다. 그리고 원하는 제품을 받는다.

우리가 그 제품이 어디서오고 만들어지는 공급망에대해 알 필요는 없는 것이다. 제품이 잘 동작하는지만 중요하기 때문이다.
이럴 경우에 private 접근제어를 사용하는 것이다. 위의 `getFullName`이 한글이나 영어로 번역되는 메소드라고 하면, 어떻게 변화할지는 상관없이
사용자 입장에선 번역만 잘 되어서 나오면 된다는 것 과 같다.

우리가 외부에서 값을 필요로 할 순 있지만, 그 내부 사정이 어떻게 돌아가는지 알 필요 없을 경우에 private 접근제어자를 사용한다고 생각한다.
복잡한 시스템일수록 더더욱 이런 경우가 많아지고, 뒤에 유지보수하게 되는 이용자를 배려하는 프로그래밍이라고 할 수 있다.

## Accessors

```javascript
const fullNameMaxLength = 10;

class Employee {
    private _fullName: string;

    get fullName(): string {
        return this._fullName;
    }

    set fullName(newName: string) {
        if (newName && newName.length > fullNameMaxLength) {
            throw new Error("fullName has a max length of " + fullNameMaxLength);
        }

        this._fullName = newName;
    }
}

let employee = new Employee();
employee.fullName = "Bob Smith";
if (employee.fullName) {
    console.log(employee.fullName);
}

```

TypeScript는 객체의 멤버에 대한 접근을 가로채는 방식으로 getters/setters를 지원한다. 이를 통해 각 객체의 멤버에 접근하는 방법을 세밀하게 제어할 수 있다.

간단한 getter, setter 예제이다.
Getter, setter를 사용한다면, 코드를 캡슐화하여 다른 곳에서 해당 코드를 변형할 때 getter,setter만을 사용해서 보호할 수 있다.

이렇게하면 공용 인터페이스(클래스)의 코드만 수정하여 무결성을 유지할 수 있다.
추후에 관련 필드가 계속 늘어나더라도 접근에 대한 것은 getter, setter만으로 쉽게 유지보수 할 수 있다.

지금까지 javascript에선 이런 특성이 잘 안나타났지만, recoil의 selector도 비슷한개념이라고 볼 수 있겠다.

## Static Properties

```javascript
class Grid {
    static origin = {x: 0, y: 0};
    calculateDistanceFromOrigin(point: {x: number; y: number;}) {
        let xDist = (point.x - Grid.origin.x);
        let yDist = (point.y - Grid.origin.y);
        return Math.sqrt(xDist * xDist + yDist * yDist) / this.scale;
    }
    constructor (public scale: number) { }
}

let grid1 = new Grid(1.0);  // 1x scale
let grid2 = new Grid(5.0);  // 5x scale

console.log(grid1.calculateDistanceFromOrigin({x: 10, y: 10}));
console.log(grid2.calculateDistanceFromOrigin({x: 10, y: 10}));

```

정적 속성 및 메서드는 클래스의 모든 인스턴스에서 공유되고, static 속성이나 메서드 앞에 키워드를 사용하여 정적으로 만든다.

## React Class Component

React에서 Class를 사용하는 예시를 찾아보다가, 가장 많이 접할 Class Component를 가져와보았다.
React Class Component는 Hook의 등장과함께 Function에 밀려난 친구지만, 아직 유지보수 하는 회사들이 많다.

첫 번째는 React Core에 구현되어있는 Class Component이고, 두 번째는 이 React Class를 상속해서 구현한 실사용 예제이다.
지금까지 보았던 Class와 비슷하지 않은가? 이렇게 core에서 구현한 class를 실체화시켜 서비스에서 구동하는 훌륭한 코드로 변모하는 것이다.

```javascript
    class Component<P, S> {
        static contextType?: Context<any>;

        context: any;

        constructor(props: Readonly<P> | P);

        constructor(props: P, context: any);

        setState<K extends keyof S>(
            state: ((prevState: Readonly<S>, props: Readonly<P>) => (Pick<S, K> | S | null)) | (Pick<S, K> | S | null),
            callback?: () => void
        ): void;

        forceUpdate(callback?: () => void): void;
        render(): ReactNode;

        readonly props: Readonly<P> & Readonly<{ children?: ReactNode }>;
        state: Readonly<S>;

        refs: {
            [key: string]: ReactInstance
        };
    }
```

Constructor는 Component가 마운트 되기전에 호출된다. 현재 컴포넌트의 상태를 정의해주는 곳이라고 볼 수 있다.
State, props등이 이곳에서 정의된다.
첫번째 보시면 자주 사용하는 method들인 setState, render등이 보인다.

```javascript
class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = {
        counter: 0;
    };
  }
  handleIncrease = () => {
      console.log('increse')
  }
  render() {
      return (
          <div>
          <h1>{this.state.counter}</h1>
          <button onClick={this.handleIncrease}></button>
          </div>
      )
  }
}
```

## Reference

https://typescript-kr.github.io
https://www.typescripttutorial.net/typescript-tutorial/typescript-access-modifiers/
https://ionicframework.com/blog/how-to-use-typescript-in-react
