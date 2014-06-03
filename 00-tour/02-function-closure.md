## 함수, 클로저

# 기본 함수

`func`, 함수 이름, 괄호 안에 매개변수를 순서대로 써 로 함수를 선언한다. `->`로 반환값 자료형을 선언한다.

    func greet(name: String, day: String) -> String {
        return "Hello \(name), today is \(day)."
    }
    greet("Bob", "Tuesday")

# 투플 반환값

투플로 여러 값을 반환할 수도 있다

    func getGasPrices() -> (Double, Double, Double) {
        return (3.59, 3.69, 3.79)
    }
    getGasPrices()

# 동적 인자

여러 값을 배열 꼴로 받을 수도 있다.

    func sumOf(numbers: Int...) -> Int {
        var sum = 0
        for number in numbers {
            sum += number
        }
        return sum
    }
    sumOf()
    sumOf(42, 597, 12)

# 내부 함수

함수 안에 함수를 겹쳐 만들 수 있다. 겹쳐 만든(nested) 함수는 바깥 함수의 변수에 접근할 수 있다.

    func returnFifteen() -> Int {
        var y = 10
        func add() {
            y += 5
        }
        add()
        return y
    }
    returnFifteen()

옮긴이: 파스칼/에이다의 내부 함수와 동등하다. 일반 함수이므로 값을 캡처하지 않는다. 

# 함수 자료형

함수는 일급 자료형이다. 다른 함수를 반환하거나 실행인자로 받을 수 있다.

    func makeIncrementer() -> (Int -> Int) {
        func addOne(number: Int) -> Int {
            return 1 + number
        }
        return addOne
    }
    var increment = makeIncrementer()
    increment(7)

    func hasAnyMatches(list: Int[], condition: Int -> Bool) -> Bool {
        for item in list {
            if condition(item) {
                return true
            }
        }
        return false
    }
    func lessThanTen(number: Int) -> Bool {
        return number < 10
    }
    var numbers = [20, 19, 7, 12]
    hasAnyMatches(numbers, lessThanTen)

# 클로저

함수는 클로저의 특수 사례이다.  중괄호({})로 감싸 이름 없이 클로저를 만들수 있다. `in` 으로 함수형과 코드를 분리한다.

    numbers.map({
        (number: Int) -> Int in
        let result = 3 * number
        return result
        })

자료형을 추론할 수 있는 경우 더 간편하게 쓸 수도 있다.

    numbers.map({ number in 3 * number })

실행인자를 이름 대신 숫자로 접근할 수 있다.

    sort([1, 5, 3, 12, 2]) { $0 > $1 }
