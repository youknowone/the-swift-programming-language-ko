## 기초

스위프트는 C/오브젝티브-C로 iOS/OS X 애플리케이션을 개발하던 것과 비슷하다.

C/오브젝티브-C의 기초 자료형을 모두 스위프트 버전으로 제공한다. Int, Double, Float, Bool, String. Array와 Dictionary도 지원한다.

C보다 강력한 상수 자료형으로 안전한 프로그래밍을 할 수 있다.

Objective-C에도 없는 더 나은 자료형도 있다. 투플은 여러 변수 값을 묶어 다룰 수 있다.

옮긴이: C, 오브젝티브-C만 해보았다면 투플은 선언 없이, 필드 이름도 없이 쓸 수 있는 익명 구조체 정도로 생각하면 비슷하다.

선택적 자료형이 있어서 nil을 가질 수 있는 값과 없는 값을 구분하여 Objective-C의 포인터 표현과 비슷하지만 더욱 많은 기능을 제공한다.

# 상수와 변수
상수(constant)와 변수(variable)는 특정 자료형의 특정 값을 나타내는 이름이다. 상수의 값은 바꿀 수 없고 변수의 값은 바뀔 수 있다.

# 상수와 변수 선언

상수는 let으로, 변수는 var로 선언한다.

    let maximumNumberOfLoginAttempts = 10
    var currentLoginAttempt = 0

여러 개는 다음과 같이 선언한다

    var x = 0.0, y = 0.0, z = 0.0

# 타입 표시(type annotation)

필요하면 자료형을 표시할 수도 있다.

    var welcomeMessage: String
    welcomeMessage = "Hello"

실제 사용 때 자료형을 표시할 일은 거의 없다. 보통은 처음 대입하는 값으로 추론이 된다.

# 변수와 상수 이름

유니코드 문자로 어떤 이름이든 넣을 수 있다.

    let π = 3.14159
    let 你好 = "你好世界"
    let 🐶🐮 = "dogcow”

단 수학기호, 화살표, private 영역, 올바르지 않은 영역, 선문자, 궤도문자는 쓸수 없다. 숫자로 시작할 수도 없다.

한번 이름을 지어주면 같은 이름으로 다른 변수를 선언하거나 다른 자료형을 넣을 수 없다.

스위프트 예약어와 같은 이름의 변수를 써야한다면 역따옴표(`)문자로 이름을 둘러싸 쓸 수 있다. 하지만 가능한 피해라.


# 출력

println으로 현재 값을 출력할 수 있다.

    println(friendlyWelcome)
    // prints "Bonjour!

코코아의 NSLog함수와 비슷한 용도로 쓸 수 있다.

문자열 보간으로 변수나 상수를 끼워넣을 수 있다.

    println("The current value of friendlyWelcome is \(friendlyWelcome)")
    // prints "The current value of friendlyWelcome is Bonjour!

# 주석

- 한 줄 주석

    // this is a comment

- 여러 줄 주석

    /* this is also a comment,
    but written over multiple lines */’

- 겹쳐 쓰는 주석: C와 달리 여는 기호를 쓴 횟수만큼 닫아주어야 한다.

    /* this is the start of the first multiline comment
    /* this is the second, nested multiline comment */
    this is the end of the first multiline comment */’

# 세미콜론

여러 줄을 한 줄에 쓰지 않는 한 세미콜론은 쓰지 않는다.

    let cat = "🐱"; println(cat)
    // prints "🐱"


# 정수

Integer는 정수형이고 소수부가 없다. signed(부호 있음)거나 unsigned(부호 없음, 항상 양수)이다.

스위프트에는 8, 16, 32, 64비트 꼴의 정수가 있다. c와 비슷하게 8비트 unsigned라면 UInt8, 32비트 signed라면 Int32 같은 식으로 쓴다.

# 정수 경계
`min`, `max` 프로퍼티로 경계값을 알 수 있다.

    let minValue = UInt8.min  // minValue is equal to 0, and is of type UInt8
    let maxValue = UInt8.max  // maxValue is equal to 255, and is of type UInt8

# Int/Uint
32비트 플랫폼에서는 Int32/UInt32, 64비트 플랫폼에서는 Int64/UInt64 이다.
특정 크기의 코드가 필요하지 않은 이상 항상 Int를 쓰기를 권장한다.

# 부동소수점 수
3.14159, 0.1, -273.15 같은 소수. Int보다 넓은 범위를 제공한다.

- `Double`: 64비트 부동소수점 수
- `Float`: 32비트 부동소수점 수

옮긴이: Int, UInt의 기본값을 제외하면 c와 똑같다. Int, UInt의 정책은 NSInteger, NSUInteger와 같다.

# 자료형 안전성과 추론
type-safe 언어로 쓸수 있는 자료형을 명확히 요구한다. String을 요구하는 자리에는 절대로 Int를 넣을 수 없다. 자료형이 다르면 오류이다.

자료형을 추론할 수 있는 경우 명시하지 않아도 된다. 넣은 값을 보고 추론한 자료형을 지정한다. 결과적으로 C나 오브젝티브-C보다 적은 타입 선언을 요구한다.

상수나 변수를 선언하며 값을 넣을 때 추론은 유용하다.

    let meaningOfLife = 42
    // meaningOfLife는 Int로 추론된다

    let pi = 3.14159
    // pi는 Double로 추론된다

부동소수점은 Float보다 Double을 우선 추론한다.

    let anotherPi = 3 + 0.14159
    // anotherPi도 Double로 추론된다

# 수 리터럴

- 10진수: 접두사 없음
- 2진수: 0b 접두사
- 8진수: 0o 접두사
- 16진수: 0x 접두사

    let decimalInteger = 17
    let binaryInteger = 0b10001       // 17 in binary notation
    let octalInteger = 0o21           // 17 in octal notation
    let hexadecimalInteger = 0x11     // 17 in hexadecimal notation

부동소수점도 10진수(접두사 없음)나 16진수(0x 접두사)로 쓸 수 있다. 10진수 지수는 e로, 16진수 지수는 p로 표현할 수 있다. 대소문자 구분은 없다.

    1.25e2 means 1.25 × 102, or 125.0.
    1.25e-2 means 1.25 × 10-2, or 0.0125.

    0xFp2 means 15 × 22, or 60.0.
    0xFp-2 means 15 × 2-2, or 3.75.

가독성을 위해 앞뒤로 0을 채워넣거나 밑줄을 넣을 수 있다.

    let paddedDouble = 000123.456
    let oneMillion = 1_000_000
    let justOverOneMillion = 1_000_000.000_000_1

#