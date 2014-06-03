
## 단순 값 (Simple value)

# 상수, 변수, 자료형 추론

`let`으로 상수를 만들고 `var`로 변수를 만든다.

    var myVariable = 42
    myVariable = 50
    let myConstant = 42

자료형(type)을 항상 명시할 필요는 없다. 컴파일러는 `myVariable` 변수를 보고 첫 값인 integer로 변수 자료형을 추론(infer)한다.

# 명시적 자료형 선언

추론이 불가능한 경우 명시할 수 있다.

    let implicitInteger = 70
    let implicitDouble = 70.0
    let explicitDouble: Double = 70

# 명시적 자료형 변환

값은 묵시적으로 다른 자료형으로 변환할 수 없다. 반드시 새 자료형의 새 인스턴스(instance)를 만들어야 한다.

    let label = “The width is “
    let width = 94
    let widthLabel = label + String(width)

# 문자열 포맷 문법

문자열에 다른 값을 넣는 포맷 문법이 있다.

    let apples = 3
    let oranges = 5
    let appleSummary = “I have \(apples) apples.”
    let fruitSummary = “i have \(apples + oranges) pieces of fruit.”


# 배열, 딕셔너리

배열과 딕셔너리는 대괄호([])로 만든다. 접근할 때도 대괄호([])에 인덱스나 키를 써서 넣는다.

    var shoppingList = ["catfish", "water", "tulips", "blue paint"]
    shoppingList[1] = "bottle of water"
     
    var occupations = [
        "Malcolm": "Captain",
        "Kaylee": "Mechanic",
    ]
    occupations["Jayne"] = "Public Relations”


옮긴이: 오브젝티브-C 3의 배열, 딕셔너리 단축표현이나 파이썬/루비/php5.4의 배열/딕셔너리를 연상할 수 있다. 

빈 배열이나 딕셔너리는 초기화 문법으로 만듭니다.

    let emptyArray = String[]()
    let emptyDictionary = Dictionary<String, Float>()


자료형 추론이 가능한 경우 []나 [:]로도 가능하다.

    shoppingList = [] // 장보러 가서 뭐든지 담는다

