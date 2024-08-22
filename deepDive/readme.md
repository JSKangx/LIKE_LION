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


---
### 질문할 내용
- [ ] 제어문을 활용하여 코드의 실행을 인위적으로 제어하는 예시가 무엇인가?

### 중요한 내용
- [ ] `for`문
- [ ] `swtich` 문에서의 `break`의 중요성과 의도적인 폴스루 활용