
## 제어 흐름 (control flow)

조건문: `if` `switch`
순환문: `for-in` `for` `while` `do-while`

# 개괄

조건/순환 변수에는 소괄호를 쓰지 않아도 된다. 코드 몸통은 반드시 중괄호 안에 들어간다.

    let individualScores = [75, 43, 103, 87, 12]
    var teamScore = 0
    for score in individualScores {
        if score > 50 {
            teamScore += 3
        } else {
            teamScore += 1
        }
    }
    teamScore

# if, if로 선택적 자료형 풀기

`if`문의 조건은 반드시 불린 표현식이다. `if score { ... }`는 오류.

선택적(optional)자료형의 경우 if와 let을 함께 쓸 수 있다.

※ 선택적 자료형이란? 어떤 값을 가질 수도 있고 가지지 않을(nil) 수도 있을 경우 자료형에 물음표(?)를 붙여 선택적 자료형을 표현할 수 있다.

옮긴이: Objective-C를 포함해 C계열 언어에서 널 접근 오류는 고질적인 런타임 오류였다. `nil`을 가질 수 있는 변수와 아닌 변수를 자료형 수준에서 엄밀히 나누어 명시적으로 변환하여 쓰도록 하여 논리 오류로 인해 널 접근을 하지 않도록 언어 수준에서 방어해 주고 있다.

    var optionalString: String? = "Hello"
    optionalString == nil
     
    var optionalName: String? = "John Appleseed"
    var greeting = "Hello!"
    if let name = optionalName {
        greeting = "Hello, \(name)"
    }

선택적 자료형의 값이 `nil`이면 조건은 `false`로 평가해 건너뛴다. 값이 있다면 풀어내서(unwrap) `let`의 변수에 대입한다. 이 변수는 코드 블럭에서 쓸 수 있다.

# switch

`switch`는 모든 자료형과 다양한 비교를 지원한다. 

    let vegetable = "red pepper"
    switch vegetable {
    case "celery":
        let vegetableComment = "Add some raisins and make ants on a log."
    case "cucumber", "watercress":
        let vegetableComment = "That would make a good tea sandwich."
    case let x where x.hasSuffix("pepper"):
        let vegetableComment = "Is it a spicy \(x)?"
    default:
        let vegetableComment = "Everything tastes good in soup."
    }

switch 안의 코드를 실행하고 나면 밖으로 빠져나온다. 다음 case로 진행하지 않으므로 명시적으로 break할 필요가 없다.

옮긴이: c 형식 switch에서 끔찍한 문제였던 명시적 break가 사라진다. let x where x.hasSuffix(“pepper”)에 주목해야 한다. case 안에서 다시 if문을 쓰는 식으로 처리하는 대신 보다 편리한 문법을 제공하여 명시적 break를 유용하게 사용하던 사례를 제거하고 있다.

`for-in`으로 딕셔너리에서 키-값 쌍을 순회할 수 있다.

    let interestingNumbers = [
        "Prime": [2, 3, 5, 7, 11, 13],
        "Fibonacci": [1, 1, 2, 3, 5, 8],
        "Square": [1, 4, 9, 16, 25],
    ]
    var largest = 0
    for (kind, numbers) in interestingNumbers {
        for number in numbers {
            if number > largest {
                largest = number
            }
        }
    }
    largest

# while, do-while

`while`로 특정 조건이 될 때까지 반복할 수 있다. 반드시 한 번은 실행하도록 할 수도 있다.

옮긴이: C계열 언어와 상동

    var n = 2
    while n < 100 {
        n = n * 2
    }
    n
 
    var m = 2
    do {
        m = m * 2
    } while m < 100
    m

# for, for in

인덱스가 있는 순환문도 만들 수 있다. `..`로 범위 를 만들수 있다. 다음 두 순환문은 동등하다.

    var firstForLoop = 0
    for i in 0..3 {
        firstForLoop += i
    }
    firstForLoop
 
    var secondForLoop = 0
    for var i = 0; i < 3; ++i {
        secondForLoop += 1
    }
    secondForLoop

`..`로 범위를 만들면 마지막 값이 빠지고 `...`로 범위를 만들면 마지막 값도 포함된다.