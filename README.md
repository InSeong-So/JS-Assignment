## Vanilla-Javascript

브랜치 따서 연습하기

## 프로젝트에 들어가기 앞서
1. **덕 타이핑(Duck Typing)** 을 활용하자. "오리처럼 생겼고, 오리처럼 걷고, 오리처럼 소리를 낸다면 그건 오리다". 이해가 안 된다면 예를 보여드리겠다.
    ```js
    function duck(face, work, voice){
      // 오리처럼 생겼다.
      this.face = face;
      // 오리처럼 걷는다.
      this.work = work;
      // 오리처럼 소리를 낸다.
      this.voise = voice;
    }

    const animal = [
      new duck('젊은 오리 얼굴', '힘찬 오리 걸음', '성난 오리 소리'),
      new duck('늙은 오리 얼굴', '힘 없는 오리 걸음', '힘 없는 오리 소리'),
      new duck('아기 오리 얼굴', '아장아장 오리 걸음', '앳된 오리 소리'),
      new duck('엄마 오리 얼굴', '사뿐한 오리 걸음', '달래는 오리 소리'),
    ]
    ```
  - 물론 지저분해 보일 수 있지만, 우리는 오리인지의 여부를 *특정 프로퍼티의 존재 여부만 체크*하면 되는 것이다. 이처럼덕 타이핑은 **적은 코드로도 객체를 폭 넓게 다루며**, **컴포넌트를 효율적으로 이해하게 하는 좋은 수단**이다.

2. **클로저**를 이해하자. 클로저는 매우 강력한 자바스크립트의 요소이며, 모든 함수는 클로저이다.

3. **this**를 어떻게 활용하느냐에 따라 설계 관점에 큰 영향을 미친다.

4. 자바스크립트는 **싱글 스레드**이다. 타 언어와는 완전히 다른 식으로 비동기 프로그래밍을 해야 한다. 자바스크립트는 실행 함수를 큐에 넣고 꺼내어 사용하며 동작한다. 이를 해결하기 위해 자바스크립트 엔진은 **이벤트 루프**에서 한 번에 하나씩 함수를 꺼내 실행한다. 이를 효율적으로, 좀 더 아름답게 작성하는 것은 자바스크립트 개발자들의 영원한 숙제이다.

5. 모든 언어, 생활에 포함되는 항목이다. **규약을 지켜 코딩하라.** 자바스크립트의 기상천외한 유연성은 최소의 코드로 최대의 일을 할 수 있다. 물론 그 코드에 누가 어떤 것을 어떻게 실행시킬 지는 알 수 없다. 유연성이 독이 될 수 있는 경우의 수를 줄이는 수단으로, **규약 레지스트리(contract registry)** 를 활용하여 **에스팩트 지향 프로그래밍(Aspect-Oriented Programming, 관점 지향 프로그래밍)** 을 해보자.

6. 소프트웨어 공학 원칙을 적용하라. 편하고 빠르게, 그러나 빈틈 없는 코드를 작성할 수 있다. 가장 유명한 **SOLID** 원칙과 **DRY** 원칙을 소개한다.
    - SOLID : **S**ingle Responsiblity Principle, 단일 책임 원칙
      > 모든 클래스(함수)는 반드시 한 가지 변경 사유가 존재해야 한다.
      - ? 이게 무슨 무리한 소리란 말인가. 우리가 작성하는 코드는 한 줄, 한 단어가 모두 그 의미를 내포하고 있는데? 걱정하지 말고 아래를 보자.
      ```js
      function sum(a, b){
        return a + b
      }
      ```
      - sum 함수의 유일한 관심사는 입력 받은 인자를 더하는 것이다. 이를 어떻게 이행할지는 철저히 외부 수단에 달려 있으니 외부 인자 a + b를 이행하기 위해 함수 자체를 변경할 필요는 없다!
    - SOLID : **O**pen-Closed Principle, 개방-패쇄 원칙
      > 모든 소프트웨어 개체는 확장 가능성은 열고, 수정 가능성은 닫아야 한다.
      - 어떤 경우에도 실행하는 핵심 코드를 변경하지 말고, 어떻게든 재사용하고 확장하라는 뜻이다. 쉽게 이해하기 위해 웹 프레임워크를 사용한다 치자. 개발자는 웹 프레임워크에서 개방된 몇몇 설정 방버을 제외하고는 핵심 기능을 변경할 수 없다!
    - SOLID : **L**iskov Substitution Principle, 리스코프 치환 원칙
      > 어떤 타입에서 파생된 타입의 객체가 있다면, 이 타입을 사용하는 코드는 변경되면 안 된다.
      - 인터페이스와 관련이 있는 원칙이다. 예를 들어 부모 객체에서 자식 객체로 파생하더라도 그 기본 로직이 변경되어선 안 된다는 것이다. 다시 말해, 작성 중인 함수가 기반 클래스로 하는 일과 서브 클래스로 하는 일이 다르면 이 원칙에 맞지 않는 것이다.
    - SOLID : **I**nterface Segregation Principle, 인터페이스 분리 원칙
      > 기능이 많은 인터페이스는 더 작게 응축시킨 조각으로 나누어야 한다.
      - 인터페이스 사용부(consumer)는 아주 작은 인터페이스 하나만 바라보면 된다. 자바스크립트에는 인터페이스도, 클래스도 없는데? 아니다. 함수가 기대하는 인자를 명확히 하고, 그 기대치를 최소화 해야 한다. 특정 타입의 인자를 바라는게 아닌 이 타입에 실제로 필요한 프로퍼티가 더 있을 것이라 기대하는 것이다.
    - SOLID : **D**ependency Inversion Principle, 의존성 역전 원칙
      > 상위 수준 모듈은 하위 수준 모듈에 의존해서는 안 되며, 둘은 추상화에 의존해야 한다.
      - 보통 **의존성 주입**이라는 연관된 개념으로 표현하며 인터페이스와 관련이 있다. 조금 복잡한 내용이니 인터페이스를 잘 이해하고 있어야 한다. 클래스 A가 클래스 B의 서비스가 필요한 경우, A는 B를 생성하지 않는 대신 A 생성자의 파라미터 하나가 B를 서술하는 인터페이스 역할을 한다. 그러면 A는 B가 아닌 자신의 인터페이스만 바라보며, A가 생성되면 구체화한 B를 넘겨받으므로 B 역시 인터페이스에 의존되는 것이다.
      - 상술했던 리스코프 치환 원칙으로 인터페이스를 만족하는 B의 파생형 버전을 제공할 수 있는 이점이 있으며, B를 고쳐야 할 경우 하위 버전 호환성을 유지하기 위해 어떤 로직을 계속 지녀야 하는지 일목요연하게 나타낼 수 있다.
    - DRY 원칙
      > 잘 말라 건조한 코드로, 모든 지식 조각이 반복하지 않고 딱 한 번만 나오는 형태이다.
      - SOLID 원칙의 개방-폐쇄 원칙이 DRY 원칙의 필연적 산물이다. 예를 들어 A, B를 함께 하는 모듈이 있다면 A의 기능이 필요할 때 B의 기능을 들어내지 않는 한 모듈을 재사용할 수 없으므로 A를 다시 코딩하는 사태가 일어난다. 이는 DRY 원칙과 맞지 않으며 A와 B를 하는 함수 2개를 모듈에 주입하여 하나의 책임으로 묶어두면 문제를 간단히 해결할 수 있다.
      - 즉, DRY한 코드는 그 과정에 의존성 주입과 단일 책임 문제가 개입되는 것이다.

## 바르게 유지되는 코드란 무엇인가?
> "와, 이건 새로 만드는게 정신 건강에 좋고... 미래를 위해서도 나을 것 같아요ㅠ"

방대한 레거시 코드를 보면 한숨이 나오고, 욕지거리가 목에 맴돈다. 아무리 완벽한 프로그램이라도 유지보수를 몇 년 거치면 괴물이 탄생한다. 이를 해결하기 위해서 어떻게 해야 할까?

### 단위 테스트를 실천하자
가장 호쾌한 해결책이 여기 있다! **단위 테스트(unit test)** 는 시간이 흐르고 어떤 변화가 닥쳐와도 완벽한 프로그램을 만들 수 있게 한다. 자세히 알아보자.<br>
단위란 특정 조건에서 어떻게 작동해야 할지 정의한 것이다. 단위 테스트 본체에서 작성한 코드는 준비(arrange), 실행(act), 단언(assert)의 패턴을 따른다.
1. 테스트 준비 : 단위를 실행할 조건을 확실히 정하고, 의존성 및 함수 입력 데이터를 설정한다.
2. 테스트 실행 : 준비 단계에서 미리 설정한 입력을 기능에 넘겨 실행한다.
3. 테스트 단언 : 미리 정한 조건에 따라 예상대로 단위가 작동하는지 확인한다.

### TDD(Test-Driven Development, 테스트 주도 개발)를 적용하라
> 애플리케이션 코드를 짜기 **전에**, 해당 코드가 통과해야 할 단위 테스트를 **먼저** 작성하는 개발 방법이다.

전체 단위 테스트 꾸러미를 만들어가는 TDD 방식을 따르면, **단위 정의**와 **인터페이스 설계**에 도움이 많이 된다. TDD를 실천할 때, 애플리케이션에 변화가 생기면 다음 단계를 밟게 된다.<br>
이 단계를 적색(실패)-녹색(성공)-리팩터링(중복 제거) 과정이라고 한다.

1. 완벽히 변경하면 성공, 그 전까지는 **반드시 실패**하는 단위 테스트 작성
2. 테스트가 성공할 수 있을 만큼의 **최소한**의 코딩
3. 애플리케이션 코드를 리팩토링하며 **중복을 제거**한다.

### 테스트하기 쉬운 코드로 다듬자
> 가장 중요한 단계는 관심사를 적절히 분리하는 **단일 책임 원칙**을 적용하는 것이다.

다음 함수를 확인하자.
```js
// validateAndRegisterUser, 변경 전

let User = Users || {};
Users.registration = () => {
  return {
    validateAndResisterUser: function validateAndDisplayUser(user){
      if (!user || user.name === "" || user.password === || user.password.length < 6){
        throw new Error('사용자 인증이 실패했습니다.');
      }

      // 사용자 정보 전송
      fetch("http://myapp.com/user", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(user),
      }).then((response) => {
        // 메세지 출력
        document.getElementById('user-message').innerText(`가입을 환영해요, ${response.data.name}님!!`);
      });
    }
  }
}
```
이 함수는 세 가지 일을 담당하며, 관심사를 요약하면 아래와 같다.
1. user 객체가 올바른지 검증한다. → **사용자 검증**
2. 검증이 완료된 user 객체를 서버로 전송한다. → **서버와 통신**
3. UI에 메세지를 출력한다. → **UI 제어**


그럼 validateAndRegisterUser 함수를 테스트할 조건을 나열해보자.
1. user가 null이면 에러를 낸다.
2. null인 user는 서버로 전송하지 않는다.
3. user가 null이면 UI를 업데이트하지 않는다.
4. user가 undefined이면 에러를 낸다.
5. undefined인 user는 서버로 전송하지 않는다.
6. user가 undefined이면 UI를 업데이트하지 않는다.
7. user의 name 프로퍼티가 빈 상태면 에러를 낸다.
8. name 프로퍼티가 빈 user는 서버로 전송하지 않는다.
9. user의 name 프로퍼티가 비어 있으면 UI를 업데이트 하지 않는다.

와, 이렇게나 많음에도 오류 조건은 끝이 아니다. UI가 제대로 업데이트 되는지, 유효성 검사가 올바른지도 테스트해야 한다.<br>
이 코드는 테스트할 수 있지만 조건이 매우 다양하게 조합되며, 모두를 보완하는 것은 불가능에 가깝다.<br>
그렇다면 상술한 세 가지 관심사를 각각 추출하여 단일 책임을 부여하면 어떨까?<br>
```js
// validateAndRegisterUser, 변경 후

let User = Users || {};
Users.registration = () => {
  return {
    validateAndResisterUser: function validateAndDisplayUser(user){
      if (!userValidator.userIsValid(user)){
        throw new Error('사용자 인증이 실패했습니다.');
      }

      // 사용자 정보 전송
      userRegister.registerUser(user);
      // 메세지 출력
      userDisplay.showRegistrationThankYou(user);
    }
  }
}
```
새로 고친 registration 모듈은 개별 객체 인스턴스를 의존성 주입으로 제공한다. 다른 관심사에 직접 영향을 미쳤던 코드 대신 주입된 객체를 사용하는 것이다. 그렇다면 테스트 케이스는 어떨까?
1. user가 잘못 넘어오면 에러가 난다.
2. 잘못된 user는 등록하지 않는다.
3. 잘못된 user는 표시하지 않는다.
4. 올바른 user를 인자로 userRegister.registerUser 함수를 실행한다.
5. userRegister.registerUser에서 에러가 나면 userDisplay.showRegistrationThankYou 함수는 실행하지 않는다.
6. user가 성공적으로 등록되면 user를 인자로 userDisplay.showRegistrationThankYou 함수를 실행한다.

오, 전체 테스트가 6개로 줄었다! 이렇게 별개의 객체로 관심사를 추출하여 단일 책임을 부여하면 독립적인 객체는 각자 완전한 테스트 꾸러미를 가지므로 코드의 작성, 테스트, 이해가 쉬워진다.<br>
TDD를 실천하면 첫째, 작은 코드는 대개 간단하고 실수할 가능성이 작아 디버깅 시간을 상당히 줄일 수 있다.<br>
둘째, 테스트로 코드를 완전히 커버하니 리팩토링을 하더라도 무섭지 않다. 결국<br>
코드를 DRY하게 유지하여 코드베이스에 오류 발생 여지를 줄이고 규모를 작게 가져갈 수 있는 것이다.<br>

<br>

여기까지 길고 지루했던 당부의 말이었다. 이제부터 진짜 **애플리케이션**을 작성해보자.

<br>

## 참조
- 자바스크립트 : 자바스크립트 패턴과 디자인
