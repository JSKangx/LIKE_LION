# 08장 제어문
- 제어문은 조건에 따라 코드 블록을 실행(조건문)하거나 반복 실행(반복문)할 때 사용한다. 일반적으로 코드는 위에서 아래 방향으로 순차적으로 실행. 제어문을 활용하면 코드의 실행 흐름을 인위적으로 제어할 수 있다.
    - 하지만 제어문은 코드의 흐름을 이해하기 어렵게 만들어 가독성을 해친다.
    - 제어문을 바르게 이해하는 것은 코딩 스킬에 많은 영향을 준다. 특히 `for` 문은 매우 중요!

### 블록문
- 블록문은 0개 이상의 문을 `중괄호` 로 묶은 것으로, 코드 블록 또는 블록이라고 부르기도 한다. 
- 자바스크립트는 블록문을 ‘하나의 실행 단위’로 취급한다.
- 일반적으로 (1) 제어문 (2) 함수를 정의할 때 사용한다.

    ```js
    // 블록문
    { var foo = 10; }

    // 제어문
    var x = 1;
    
    // 함수 선언문
    function sum(a, b) {
        return a + b;
    }
    ```

### 조건문
- 조건문은 주어진 **조건식의 평가 결과에 따라 코드 블록의 실행을 결정**한다.
- 조건식은 **불리언 값**으로 평가될 수 있는 문이다.

#### if...else 문

    ```js
    if (조건식) {
        // 조건식이 true면 이 코드 블록이 실행.
    } else {
        // 조건식이 false면 이 코드 블록이 실행.
    }
    ```

- `if`문의 조건식이 **불리언 값이 아닌 값**으로 평가되면 자바스크립트 엔진에 의해 암묵적으로 불리언 값으로 **강제 변환**되어 실행할 코드 블록을 결정. (9.2절 - 암묵적 타입 변환)
- 조건을 추가하고 싶으면 `else if`문을 사용한다.

    ```js
    if (조건식1) {
        // 조건식1이 참이면 실행될 코드 블록
    } else if (조건식2) {
        // 조건식2가 참이면 실행될 코드 블록
    } else {
        // 조건식1, 2가 모두 거짓이면 실행될 코드 블록
    }
    ```

- 예시

    ```js
    var num = 2;
    var kind;

    // if문
    if (num > 0) {
        kind = '양수';
    } else if {
        kind = '음수';
    } else {
        kind = '영';
    }
    console.log(kind); // 양수
    // 코드 블록 내의 문이 하나뿐이라면 중괄호를 생략할 수 있다.
    if      (num > 0)  kind = '양수';
    else if (num < 0)  kind = '음수';
    else               kind = '영';

    // 위 조건문을 삼항 연산자로 표현하면
    var kind = num ? (num > 0 ? '양수' : '음수') : '영';

    // 홀수와 짝수를 판단하는 조건문을 삼항연산자로 표현
    var x = 2;
    var result;
    // 0은 false로 취급된다.
    var result = x % 2 ? '홀수' : '짝수'
    ```
- 조건에 따라 단순히 값을 결정하여 변수에 할당하는 경우 **삼항 조건 연산자**를 사용하는 편이 더 가독성이 좋다. 하지만 내용이 복잡하여 여러 줄의 문이 필요하다면 `if...else`문을 사용하는 편이 가독성이 좋다.

#### switch문

    ```js
    switch (표현식) {
        case 표현식1:
            switch 문의 표현식과 표현식1이 일치하면 실행될 문;
            break;
        case 표현식2:
            switch 문의 표현식과 표현식2가 일치하면 실행될 문;
            break;
        default:
            switch 문의 표현식과 일치하는 case 문이 없을 때 실행될 문;
    }
    ```
- `switch`문의 표현식은 불리언 값보다는 **문자열**이나 **숫자**값인 경우가 많다. 그래서 `switch`문은 논리적 참, 거짓보다는 **다양한 상황**에 따라 실행할 코드 블록을 결정할 때 사용한다.

    ```js
    var month = 11;
    var monthName;

    switch (month) {
        case 1: monthName = "January"; // month가 1이라면 monthName에 "January"를 할당.
        case 2: monthName = "February";
        case 3: monthName = "March";
        case 4: monthName = "April";
        case 5: monthName = "May";
        case 6: monthName = "June";
        case 7: monthName = "July";
        case 8: monthName = "August";
        case 9: monthName = "September";
        case 10: monthName = "October";
        case 11: monthName = "November";
        case 12: monthName = "December";
        default: monthName = "Invalid month";
    }
    console.log(monthName); // Invalid month

- `case`문을 실행한 후 `switch`문을 탈출하지 않고 끝날때까지 반복 실행했으므로 마지막에 'Invalid month'가 재할당된 것이다. (폴스루)

    ```js
    // 올바른 문
    switch (month) {
        case 1: monthName = "January";
            break;
        case 2: monthName = "February";
            break;
        // ... 계속
        default: monthName = "Invalid month"; // 실행이 종료되면 자동으로 탈출
    }
    ```

- 의도적으로 폴스루를 활용한 `switch`문

    ```js
    var year = 2000;
    var month = 2;
    var days = 0;

    switch (month) {
        // 아랫줄의 모든 경우에 대하여 days=31; 실행
        case 1: case 3: case 5: case 7: case 8: case 10: case 12:
            days = 31;
            break;
        // 아랫줄의 모든 경우에 대하여 days=30; 실행
        case 4: case 6: case 9: case 11:
            days = 30;
            break;
        case 2:
            // 윤년 계산 알고리즘
            // 1. 연도가 4로 나누어떨어지는 해(2000, 2004, 2008, ...)는 윤년이다.
            // 2. 연도가 4로 나누어떨어지더라도 연도가 100으로 나누어떨어지는 해 (2000, 2100, 2200, ...)는 평년이다.
            // 3. 연도가 400으로 나누어떨어지는 해(2000, 2400, 2800, ...)는 윤년이다.
            // 즉, 1, 2를 동시에 만족 시키거나 3을 만족시키면 29를, 아니면 28을 할당.
            days = ((year % 4 === 0 && year % 100 !== 0) || (year % 400 === 0)) ? 29 : 28;
            break;
        default:
            console.log('Invalid month');
    }
    ```

### 반복문
- 조건식의 평가 결과가 거짓일 때까지 코드 블록을 계속하여 실행하는 문.
- 세 가지 반복문: `for`, `while`, `do...while`

#### for문

    ```js
    for (변수 선언문 또는 할당문; 조건식; 증감식) {
        조건식이 참인 경우 반복 실행할 문;
    }

    // i가 0부터 시작해서 2보다 작을 때까지 코드 블록을 2번 반복 실행한다.
    // 변수 선언문은 단 한번만 실행된다.
    for (var i = 0; i < 2; i++) {
        console.log(i);
    }
    // 0 1

    // 어떤 식도 선언하지 않으면 무한루프가 된다.
    for (;;) { ... }
    ```

- `for`문 내에 `for`문을 중첩해 사용할 수 있다. 

    ```js
    // 주사위 2개를 던졌을 때 두 눈의 합이 6이 되는 모든 경우의 수 구하기
    for (var i = 1; i <= 6; i++) {
        for (var j = 1; j <= 6; j++) {
            if (i + j === 6) console.log(`[${i}, ${j}]`);
        }
    }
    // [1, 5] [2, 4] [3, 3] [4, 2] [5, 1]
    ```

#### while문
- `for`문은 반복 횟수가 명확할 때 주로 사용, `while`문은 반복 횟수가 불명확할 때 주로 사용.
-`while`문은 조건문의 평가 결과가 거짓이 되면 코드 블록을 실행하지 않고 종료한다.

    ```js
    var count = 0;

    // count가 3보다 작을 때까지 코드 블록을 계속 반복 실행.
    while (count < 3) {
        console.log(count); // 0 1 2
        count++;
    }

    // 무한 루프
    while (true) { ... }

    // 탈출하기 위해서는 if문으로 탈출 조건을 만들고 break 문으로 탈출
    var count = 0;

    // 무한루프
    while (true) {
        console.log(count);
        count++;
        // count가 3이면 탈출
        if (count === 3) break;
    } // 0 1 2
    ```
#### do...while문
- 코드 블록을 먼저 실행하고 조건식을 평가한다. 따라서, 코드 블록은 무조건 한 번 이상 실행된다.

    ```js
    var count = 0;

    //count가 3보다 작을 때까지 코드 블록을 계속 반복 실행
    do {
        console.log(count); // 0 1 2
        count++; // 이 줄이 위로 올라가면 1 2 3이 결과로 도출
    } while (count < 3);
    ```
### break 문
- 정확히 표현하자면 코드 블록을 탈출하는 것이 아니라 레이블 문, 반복문 또는 `switch`문의 코드 블록을 탈출한다. 이것 외에 `break`문을 사용하면 문법 에러가 발생한다.
- 레이블 문이란 식별자가 붙은 문을 말한다. 프로그램의 실행 순서를 제어하는 데 사용한다. 
- `swtich`문의 `case`문과 `default`문도 레이블문이다.
- 레이블 문을 탈출하려면 `break`문에 레이블 식별자를 지정한다.

    ```js
    // foo라는 레이블이 붙은 레이블 문
    foo: console.log('foo');

    // foo라는 식별자가 붙은 레이블 블록문
    foo: {
        console.log(1);
        break foo; // foo 레이블 블록문을 탈출한다.
        console.log(2);
    }
    ```
- 중첩된 `for`문의 내부 `for`문에서 `break`문을 실행하면 내부 `for`문을 탈출하여 외부 `for`문으로 진입한다. 이때 내부 `for`문이 아닌 외부 `for`문을 탈출하려면 레이블 문을 사용한다.

    ```js
    // outer라는 식별자가 붙은 레이블 for문
    outer: for (var i = 0; i < 3; i++) {
        for (var j = 0; j < 3; j++) {
            // i + j === 3이면 outer라는 식별자가 붙은 레이블 for문을 탈출
            if (i + j === 3) break outer;
            console.log(`inner [${i}, ${j}]`);
        }
    }
    ```
- 레이블 문은 중접된 for문 외부로 탈출할 때 유용하지만 그 밖의 경우에는 일반적으로 권장하지 않는다. 가독성이 나빠지고 오류를 발생시킬 가능성이 높아진다.

### continue 문
- 반복문의 코드 블록 실행을 현 시점에서 중단하고 반복문의 증감식으로 실행 흐름을 이동시킨다. break문처럼 반복문을 탈출하지는 않는다.

    ```js
    var string = 'Hello World.';
    var search = 'l';
    var count = 0;

    // 문자열은 유사 배열이므로 for 문으로 순회할 수 있다.
    for (var i = 0; i < string.length; i++) {
        // 'l'이 아니면 현 시점에서 실행을 중단하고 반복문의 증감식으로 이동
        if (string[i] !== search) continue;
        count++; // continue문이 실행되면 이 문은 실행되지 않는다.
        // 'l' 일 때만 count를 증가시키기 때문에 'l'의 개수를 셀 수 있다.
    }

    console.log(count); // 3

    // 위 for문과 같은 기능을 하는 문은 다음과 같다.
    for (var i = 0; i < string.length; i++) {
        // 'l'이면 카운트 증가.
        if (string[i] === search) count++;
    }

    // 같은 기능을 가진 메서드
    const regexp = new RegExp(search, 'g');
    console.log(string.match(regexp).length); // 3
    ```

- if문 내에서 실행해야 할 코드가 한줄이라면 continue 문을 사용했을 때보다 간편하고 가독성도 좋다. 그런데 if 문 내에서 실행해야 할 코드가 길다면 들여쓰기가 한 단계 더 깊어지므로 continue 문을 사용하는 편이 가독성이 더 좋다.

    ```js
    // continue 문을 사용하지 않으면 if 문 내에 코드를 작성해야 한다.
    for (var = i; i < string.length; i++) {
        // 'l'이면 카운트 증가
        if (string[i] === search) {
            count++;
            // code
            // code
            // code
        }
    }

    // continue 문을 사용하면 if 문 밖에 코드 작성 가능
    for (var = i; i < string.length; i++) {
        // 'l'이 아니면 카운트 증가 안 함.
        if (string[i] !== search) continue;
        count++;
        // code
        // code
        // code
    }
    ```

* * *
# 09장 타입 변환과 단축 평가
### 타입 변환이란?
- 개발자가 의도적으로 값의 타입을 변환하는 것을 **명시적 타입 변환** 또는 **타입 캐스팅**이라 한다.

    ```js
    var x = 10;

    // x를 string으로 변환하는 메서드 (명시적 타입 변환)
    var str = x.toString(); 
    console.log(typeof str, str); // string 10

    // x의 값이 변경된 것은 아니다.
    console.log(typeof x); // number

    // 암묵적 타입 변환을 이용하여 x를 string으로 바꾸는 표현식
    // 암묵적 타입 변환은 개발자의 의도가 드러나진 않지만, 때로는 간결하여 가독성이 더 좋을 때도 있다. 그러나 자신이 작성한 코드를 동료가 쉽게 이해할 수 있어야 하기 때문에, 타입 변환이 어떻게 동작하는지 정확히 이해하고 사용해야 한다.
    var str = x + ''; 
    ```

- 개발자의 의도와는 상관없이 표현식을 평가하는 도중에 자바스크립트 엔진에 의해 암묵적으로 타입이 자동 변환되는 것을 **암묵적 타입 변환** 혹은 **타입 강제 변환**이라 한다.
- 암묵적 타입 변환은 기존 변수 값을 재할당하여 변경하는 것이 아니다. 

### 암묵적 타입 변환
#### 문자열 타입으로 변환
- 문자열 연결 연산자 (+), 템플릿 리터럴, 문자열 변환 표현식에서 일어남

    ```js
    // 문자열 연결 연산자 + 의 모든 피연산자는 문자열 타입으로 암묵적 변환.
    '10' + 2 // '102'

    // 템플릿 리터럴의 표현식 삽입도 문자열 타입으로 암묵적 변환
    `1 + 1 = ${1 + 1}` // "1 + 1 = 2"

    // 숫자, 불리언, null, undefined, 객체 타입은 문자열 변환 표현식으로 암묵적 변환 가능.
    // 그러나 심벌 타입은 불가능
    (Symbol()) + '' // TypeError: Cannot convert a Symbol value to a string
    ```
#### 숫자 타입으로 변환
- (1) 산술 연산자(-, *, /), 의 모든 피연산자에게서 일어남
- 피연산자를 숫자 타입으로 변환할 수 없는 경우는 산술 연산을 수행할 수 없으므로 표현식의 평과결과는 NaN이 된다.
- (2) 비교 연산자의 피연산자에게서 일어남
- (3) + 단항 연산자의 피연산자에게서 일어남

    ```js
    +'' // 0
    +'0' // 0
    +'string' // Nan

    // 객체와 빈 배열이 아닌 배열, undefined는 변환되지 않는다.
    +{}             // Nan
    +[10, 20]       // NaN
    +(function(){}) // NaN
    ```

#### 불리언 타입으로 변환
- 자바스크립트 엔진은 조건식의 평가 결과를 불리언 타입으로 암묵적 타입 변환한다.
- 이 때 불리언 타입이 아닌 값을 Truthy(참으로 평가되는 값) 또는 Falsy(거짓으로 평가되는 값)으로 구분한다. Truthy값은 true로, Falsy값은 false로 암묵적 타입 변환한다.

    > false로 평가되는 값
    > false
    > undefined
    > null
    > 0, -0
    > NaN
    > '' (빈 문자열)




* * *
### 질문할 내용
- [ ] 제어문을 활용하여 코드의 실행을 인위적으로 제어하는 예시가 무엇인가?
- [ ] 레이블문이 정확히 뭐지? (예제 08-20, 21)
- [ ] String.prototype.match 메서드 (예제 08-23)
- [ ] 예제 08-25 해석

### 중요한 내용
- [ ] `for`문의 실행 순서
- [ ] `swtich` 문에서의 `break`의 중요성과 의도적인 폴스루 활용
- [ ] 암묵적 타입 변환이 필요한 때