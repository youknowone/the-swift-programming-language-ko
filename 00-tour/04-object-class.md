## 객체와 클래스

# 클래스 선언

`class`로 클래스를 만든다. 프로퍼티는 클래스 안에 있다는 점을 제외하면 상수나 변수 선언과 같다. 메서드는 함수와 같다.

    class Shape {
        var numberOfSides = 0
        func simpleDescription() -> String {
            return "A shape with \(numberOfSides) sides."
        }
    }

# 인스턴스 생성

클래스 명에 괄호를 붙여 인스턴스를 생성한다.

    var shape = Shape()
    shape.numberOfSides = 7
    var shapeDescription = shape.simpleDescription()’

# 초기화/종결화 함수

초기화 함수를 만들 수 있다.

    class NamedShape {
        var numberOfSides: Int = 0
        var name: String
        
        init(name: String) {
            self.name = name
        }
        
        func simpleDescription() -> String {
            return "A shape with \(numberOfSides) sides."
        }
    }

`self`로 name 프로퍼티와 실행인자를 구분한다. 모든 변수는 `init`이나 선언 중 하나에서 초기화가 되어야 한다.

옮긴이: `self`와 프로퍼티 정책은 오브젝티브C와 달라졌다. 이름 충돌이 없으면 name으로 멤버 변수에 접근할 것이다.

종결화 함수도 `deinit`으로 만들 수 있다.

# 서브클래스
이름 뒤에 콜론과 수퍼클래스를 쓴다. 루트 클래스는 없다. 수퍼클래스의 메서드를 덮어쓰는 메서드는 `override`로 표시해야한다. 표시하지 않으면 오류이다. 실제로 덮어쓰지 않는데 `override`가 표시된 경우도 오류이다.

옮긴이: NSObject, Object, TObject 등등 모든 객체가 상속해야 하는 표준 클래스가 없다는 뜻이다.

    class Square: NamedShape {
        var sideLength: Double
        
        init(sideLength: Double, name: String) {
            self.sideLength = sideLength
            super.init(name: name)
            numberOfSides = 4
        }
        
        func area() ->  Double {
            return sideLength * sideLength
        }
        
        override func simpleDescription() -> String {
            return "A square with sides of length \(sideLength)."
        }
    }
    let test = Square(sideLength: 5.2, name: "my test square")
    test.area()
    test.simpleDescription()

# 프로퍼티
단순한 값으로 된 프로퍼티뿐 아니라 getter와 setter를 만들 수도 있다.

    class EquilateralTriangle: NamedShape {
        var sideLength: Double = 0.0
        
        init(sideLength: Double, name: String) {
            self.sideLength = sideLength
            super.init(name: name)
            numberOfSides = 3
        }
        
        var perimeter: Double {
        get {
            return 3.0 * sideLength
        }
        set {
            sideLength = newValue / 3.0
        }
        }
        
        override func simpleDescription() -> String {
            return "An equilateral triagle with sides of length \(sideLength)."
        }
    }
    var triangle = EquilateralTriangle(sideLength: 3.1, name: "a triangle")
    triangle.perimeter
    triangle.perimeter = 9.9
    triangle.sideLength

perimeter의 setter에서 새 값은 묵시적으로 `newValue`라는 이름이 붙어있다. 바꾸고 싶으면 `set` 다음에 소괄호로 둘러싸고 이름을 넣어줄 수 있다.

init시 접근 순서에 주의:

1. 서브클래스 프로퍼티 설정
1. 수퍼클래스 초기화 실행
1. 이제 수퍼클래스에서 정의한 프로퍼티 사용 가능

옮긴이: 프로퍼티 정책은 C#이나 델파이의 정책과 거의 비슷하다. 명시적 getter, setter는 완전히 C#과 같다. 오브젝티브-C 2.0 이상에서 멤버 필드를 전혀 사용하지 않고 프로퍼티만으로 프로그래밍을 해왔다면 그와도 비슷할 것이다.

# 프로퍼티 이벤트

프로퍼티를 계산할 필요는 없지만 바뀌기 전이나 후에 할 일이 있을 경우 `willSet`, `didSet`을 이용한다. 

    class TriangleAndSquare {
        var triangle: EquilateralTriangle {
        willSet {
            square.sideLength = newValue.sideLength
        }
        }
        var square: Square {
        willSet {
            triangle.sideLength = newValue.sideLength
        }
        }
        init(size: Double, name: String) {
            square = Square(sideLength: size, name: name)
            triangle = EquilateralTriangle(sideLength: size, name: name)
        }
    }
    var triangleAndSquare = TriangleAndSquare(size: 10, name: "another test shape")
    triangleAndSquare.square.sideLength
    triangleAndSquare.triangle.sideLength
    triangleAndSquare.square = Square(sideLength: 50, name: "larger square")
    triangleAndSquare.triangle.sideLength

옮긴이: 오브젝티브-C KVO에서 익숙하게 쓰던 패턴이다

# 메서드 이름

함수는 함수 값만으로 호출할 수 있지만 메서드는 첫 매개변수를 제외하면 반드시 메서드 매개변수 이름을 함께 붙여서 호출해야 한다.

    class Counter {
        var count: Int = 0
        func incrementBy(amount: Int, numberOfTimes times: Int) {
            count += amount * times
        }
    }
    var counter = Counter()
    counter.incrementBy(2, numberOfTimes: 7)

옮긴이: numberOfTimes는 메서드 시그내처의 일부인 셈이다. 오브젝티브-C의 메서드 작명과 호환되게 하려는 의도인듯.

# 선택적 자료형

선택적 자료형을 쓸 때 이름 뒤에 ?를 붙이면 nil이 아닐 경우 ? 이후부터는 무시된다. nil이 아니라면 값을 풀어(unwrap) 쓴다.

    let optionalSquare: Square? = Square(sideLength: 2.5, name: "optional square")
    let sideLength = optionalSquare?.sideLength

