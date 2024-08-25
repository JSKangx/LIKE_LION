# 08장 제어문
- 제어문은 조건에 따라 코드 블록을 실행(조건문)하거나 반복 실행(반복문)할 때 사용한다. 일반적으로 코드는 위에서 아래 방향으로 순차적으로 실행. 제어문을 활용하면 코드의 실행 흐름을 인위적으로 제어할 수 있다.
    - 하지만 제어문은 코드의 흐름을 이해하기 어렵게 만들어 가독성을 해친다.
    - 제어문을 바르게 이해하는 것은 코딩 스킬에 많은 영향을 준다. 특히 `for` 문은 매우 중요!

### 1. 블록문
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

### 2. 조건문
- 조건문은 주어진 **조건식의 평가 결과에 따라 코드 블록의 실행을 결정**한다.
- 조건식은 **불리언 값**으로 평가될 수 있는 문이다.

#### 2-1. if...else 문
- 주어진 조건식의 평가 결과에 따라 실행할 코드 블록을 결정한다.

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

#### 2-2. switch문
- 주어진 표현식을 평가하여 그 값과 일치하는 표현식을 갖는 case 문으로 실행 흐름을 옮김.

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

### 3. 반복문
- 조건식의 평가 결과가 거짓일 때까지 코드 블록을 계속하여 실행하는 문.
- 세 가지 반복문: `for`, `while`, `do...while`

#### 3-1. for문
- 조건식이 거짓으로 평가될 때까지 코드 블록을 반복 실행.

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

#### 3-2. while문
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
#### 3-3. do...while문
- 코드 블록을 먼저 실행하고 조건식을 평가한다. 따라서, 코드 블록은 무조건 한 번 이상 실행된다.

    ```js
    var count = 0;

    //count가 3보다 작을 때까지 코드 블록을 계속 반복 실행
    do {
        console.log(count); // 0 1 2
        count++; // 이 줄이 위로 올라가면 1 2 3이 결과로 도출
    } while (count < 3);
    ```
### 4. break 문
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

### 5. continue 문
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
### 1. 타입 변환이란?
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

### 2. 암묵적 타입 변환
#### 2-1. 문자열 타입으로 변환
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
#### 2-2. 숫자 타입으로 변환
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

#### 2-3. 불리언 타입으로 변환
- 자바스크립트 엔진은 조건식의 평가 결과를 불리언 타입으로 암묵적 타입 변환한다.
- 이 때 불리언 타입이 아닌 값을 Truthy(참으로 평가되는 값) 또는 Falsy(거짓으로 평가되는 값)으로 구분한다. Truthy값은 true로, Falsy값은 false로 암묵적 타입 변환한다.

    > false로 평가되는 값 : false, undefined, null, 0, -0, NaN, '' (빈 문자열)

    ```js
    // 전달받은 인수가 Falsy 값이면 true, Truthy 값이면 false를 반환
    function (v) {
        return !v;
    }
    // 전달받은 인수가 Falsy 값이면 false, Truthy 값이면 true를 반환
    function (v) {
        return !!v;
    }
    ```

### 3. 명시적 타입 변환
#### 3-1. 문자열 타입으로 변환
- (1) String 생성자 함수를 new 연산자 없이 호출하는 방법

    ```js
    String(변환하고 싶은 숫자, 불리언 타입); // "..."
    ```

- (2) Object.prototype.toSrting 메서드를 이용하는 방법

    ```js
    (1).toString(); // "1"
    ```

- (3) 문자열 연결 연산자를 이용하는 방법 (앞에서 설명)

#### 3-2. 숫자 타입으로 변환
- (1) Number 생성자 함수를 new 연산자 없이 호출하는 방법

    ```js
    Number("10.53"); // 10.53
    ```

- (2) parseInt, parseFloat 함수를 사용하는 방법 (문자열에만 가능)

    ```js
    parseInt('10.53'); // 10 -> 문자열을 정수(소수점 이하 무시)로 변환
    parseFloat('10.53'); // 10.53 -> 문자열을 부동 소수점 숫자로 변환

- (3) 단항 산술 연산자를 이용 (앞에서 설명)
- (4) * 산술 연산자를 이용 (앞에서 설명)

#### 3-3. 불리언 타입으로 변환
- (1) Boolean 생성자를 new 연산자 없이 호출하는 방법
    - false로 평가되는 값 : false, undefined, null, 0, -0, NaN, '' (빈 문자열)
- (2) ! 부정 논리 연산자를 두 번 사용하는 방법

### 4. 단축 평가
#### 4-1. 논리 연산자를 사용한 단축 평가
- 논리합 또는 논리곱 연산자 표현식은 언제나 2개의 피연산자 중 어느 한쪽으로 평가된다.
- 논리곱(&&) 연산자는 두 개의 피연산자가 모두 true로 평가될 때 true를 반환한다. 

    ```js
    'Cat' && 'Dog' // "Dog"
    ```

    - 첫 번째 피연산자 'Cat'은 Truthy 값이므로 true로 평가.
    - 두 번째 피연산자가 위 논리곱 연산자 표현식의 평가 결과를 결정
    - 따라서, 논리 연산의 결과를 결정하는 두 번째 피연산자를 그대로 반환.

- 논리합(||) 연산자는 두 개의 피 연산자 중 하나만 true로 평가되어도 true를 반환.

    ```js
    'Cat' || 'Dog' // "Cat"
    ```

    - 'Cat'이 Truthy 값이기 때문에, 두 번째 피연산자까지 평가해보지 않아도 표현식을 평가할 수 있다.
    - 논리 연산의 결과를 결정한 첫 번째 피연산자인 'Cat'을 그대로 반환.

- 논리곱 연산자와 논리합 연산자는 피연산자를 **타입 변환하지 않고 그대로 반환**한다. 이를 **단축 평가**라 한다.
- **단축 평가는 표현식을 평가하는 도중에 평가 결과가 확정된 경우 나머지 평가 과정을 생략하는 것**을 말한다.
- 단축 평가를 사용하면 if문을 대체할 수 있다. 
- 어떤 조건이 Truthy값일 때 무언가를 해야 한다면 논리곱 연산자 표현식을 쓰자.

    ```js
    var done = true;
    var message = '';

    // 주어진 조건이 true일 때
    if (done) message = '완료';

    // 단축 평가로 대체해보자.
    message = done && '완료'; // 논리곱의 결과를 결정하는 '완료'를 그대로 반환, 할당
    ```

- 어떤 조건이 Falsy값일 때 무언가를 해야 한다면 논리합 연산자를 쓰자.

    ```js
    var done = false;
    var message = '';

    // 주어진 조건이 false 일 때 if 문
    if(done) message = '미완료';

    // 단축평가로 대체해보자.
    message = done || '미완료'; // 논리합의 결과를 결정하는 '미완료'
    ```

- 위 두가지 내용을 삼항 조건 연산자로 대체해 보자.

    ```js
    var done = true;
    var message = '';

    message = done ? '완료' : '미완료';
    ```

- 단축 평가는 다음과 같은 상황에서 유용하게 사용됨 (나중에 배울 개념)
    - (1) 객체를 가리키기를 기대하는 변수가 null 또는 undefined가 아닌지 확인하고 프로퍼티를 참조할 때.
        
        ```js
        // 객체를 가리키기를 기대하는 변수의 값이 객체가 아니라 null 또는 undefined인 경우 객체의 프로퍼티를 참조하면 타입 에러가 발생하고 프로그램이 강제 종료된다.
        var elem = null;
        // 아무것도 아닌(null) 객체의 프로퍼티를 참조할 수 없다.
        var value = elem.value; // TypeError: Cannot read

        // 단축 평가를 사용하면 에러를 발생시키지 않는다.
        var elem = null;
        // elem이 null이나 undefined와 같은 Falsy 값이면 elem으로 평가되고
        // elem이 Truthy 값이면 elem.value로 평가된다.
        var value = elem && elem.value; // 논리곱 표현식의 결과를 결정하는 elem이 그대로 반환, 할당
        ```

    - (2) 함수 매개변수에 기본값을 설정할 때
        - 함수를 호출할 때 인수를 전달하지 않으면 매개변수에는 undefined가 할당된다. 이 때 단축 평가를 사용해 매개변수의 기본값을 설정하면 undefined로 인해 발생할 수 있는 에러를 방지할 수 있다.

        ```js
        // 단축 평가를 사용한 매개변수의 기본값 설정
        function getStringLength(str) {
            // 빈 문자열은 Falsy값. 
            str = str || ''; // str이 Truthy면 str을, 아니면 ''을 반환.
            return str.length;
        }

        getStringLength();      // str = ''; -> str.length; 0
        getStringLength('hi')   // str = 'hi'; -> str.length; 2

        // 아래의 함수로 단축 표현 가능
        // str = ''; 명시적 타입 변환(문자열) 표현식임.
        function getStringLength(str = '') {
            return str.length;
        }
        ```

#### 4-2. 옵셔널 체이닝 연산자
- ES11에서 도입된 옵셔널 체이닝 연산자 `?.`는 좌항의 피연산자가 null 또는 undefined인 경우 undefined를 반환하고, 그렇지 않으면 **우항의 프로퍼티 참조**를 이어간다.

    ```js
    var elem = null;

    var value = elem?.value;
    // elem이 null 이기 때문에 undefined를 반환.
    // 만약 elem이 null이나 undefined가 아니었다면 elem.value를 반환했을 것.
    ```

- 객체를 가리키기를 기대하는 변수가 null 또는 undefined가 아닌지 확인하고 프로퍼티를 참조할 때 유용하다. (옵셔널 체이닝 연산자가 도입되기 전에는 논리 연산자를 사용한 단축 평가를 통해 확인했다)
- 논리 연산자는 좌항 피연산자가 Falsy값이면 좌항 피연산자를 그대로 반환한다. 하지만 0이나 ''(빈 문자열)은 객체로 평가될 때도 있다.

    ```js
    var str = '';

    // 문자열의 길이를 참조하기 위한 표현식
    var length = str && str.length; // str이 Falsy 값이기에 str을 반환
    console.log(length); // ''

    // 하지만 옵셔널 체이닝 연산자는 좌항 피연산자가 Falsy값이라도 null 또는 undefined가 아니면 우항의 프로퍼티 참조를 이어나간다.
    var length = str?.length;
    // str이 null이나 undefined가 아니기 때문에 str.length를 반환
    console.log(length); // 0
    ```

#### 4-3. null 병합 연산자
- 좌항의 피연산자가 null 또는 undefined인 경우 **우항의 피연산자를 반환**, 그렇지 않으면 **좌항의 피연산자를 반환**
- 변수에 기본값을 설정할 때 유용하다.

    ```js
    var foo = null ?? 'default string'; // null이기 때문에 우항의 피연산자를 반환
    console.log(foo); // 'default string'
    ```

- null 병합 연산자가 도입되기 이전에는 논리합 연산자를 사용한 단축 평가를 통해 변수에 기본값을 설정했다.
    - 좌항의 피연산자가 Falsy값이면 우항의 피연산자를 반환한다.그런데 0이나 ''(빈문자열)도 기본값으로서 유효하다면 예기치 않은 동작이 발생할 수 있다.

    ```js
    // ''(빈 문자열)도 기본값으로 유효하지만 'default string'을 반환
    var foo = '' || 'default string'; 
    console.log(foo); // "default string"

    // 하지만 null 병합 연산자는 좌항의 피연산자가 null 또는 undefined가 아니면 좌항의 피연산자를 그대로 반환
    var foo = '' ?? 'default string';
    console.log(foo); // ""
    ```

* * *
## 질문할 내용
- [ ] 제어문을 활용하여 코드의 실행을 인위적으로 제어하는 예시가 무엇인가?
- [ ] 레이블문이 정확히 뭐지? (예제 08-20, 21)
- [ ] String.prototype.match 메서드 (예제 08-23)
- [ ] 예제 08-25 해석
- [ ] Object.prototype에서 prototype이 무엇인지?

* * *
## 중요한 내용
### 1. `for`문의 실행 순서
### 2. `swtich` 문에서의 `break`의 중요성과 의도적인 폴스루 활용
### 3. 암묵적 타입 변환이 필요한 때
### 4. 단축 평가로 if문을 대체할 수 있다?

* * *
## 찾아본 내용
### `new` 연산자의 역할
- 새로운 빈 객체 생성
- 프로토타입 연결
- 'this' 바인딩
- 함수의 반환 

    ```js
    function Person(name, age) {
        this.name = name;
        this.age = age;
        this.sayHello = function() {
            console.log("Hello, my name is " + this.name);
        };
    }

    let person1 = new Person("Alice", 30);
    person1.sayHello(); // "Hello, my name is Alice"
    ```

### prototype이란?
- prototype은 JavaScript의 함수(생성자 함수 포함)가 가지는 특수한 속성입니다. 이는 해당 함수로 생성된 객체들이 공통으로 사용할 수 있는 메서드나 속성을 정의하는 데 사용됩니다.
- 프로토타입 체인: JavaScript에서 모든 객체는 [[Prototype]]이라는 숨겨진 링크를 가지고 있는데, 이는 해당 객체를 생성한 생성자 함수의 prototype 속성을 가리킵니다. 이렇게 객체가 [[Prototype]] 링크를 통해 다른 객체(프로토타입 객체)와 연결되는 체계를 "프로토타입 체인"이라고 합니다.
- Object.prototype: 모든 객체의 최상위 프로토타입 객체는 Object.prototype입니다. 즉, 모든 객체는 기본적으로 Object.prototype에 정의된 속성과 메서드를 상속받습니다. 예를 들어, toString, hasOwnProperty 같은 메서드들은 Object.prototype에 정의되어 있어서 모든 객체가 사용할 수 있습니다.

    ```js
    function Person(name) {
    this.name = name;
    }

    Person.prototype.sayHello = function() {
        console.log("Hello, my name is " + this.name);
    };

    let person1 = new Person("Alice");
    person1.sayHello(); // "Hello, my name is Alice"
    ```
    - 위 코드에서 Person 생성자 함수의 prototype 객체에 sayHello 메서드를 정의했습니다. 이렇게 하면 Person 생성자 함수를 사용하여 생성된 모든 객체는 sayHello 메서드를 사용할 수 있게 됩니다. 이는 프로토타입 체인을 통해 person1 객체가 sayHello 메서드를 찾을 수 있기 때문입니다.
- 정리하면, prototype은 JavaScript에서 객체가 다른 객체로부터 메서드와 속성을 상속받도록 하는 메커니즘의 핵심입니다.