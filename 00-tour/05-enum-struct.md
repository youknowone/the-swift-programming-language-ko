## 열거형와 구조체

# 열거형

`enum`으로 열거 자료형을 만든다. 열거형에도 메서드를 만들 수 있다.

옮긴이: 비슷한걸 제공하는 주류 언어는 생각나지 않습니다… Rust..?

    enum Rank: Int {
        case Ace = 1
        case Two, Three, Four, Five, Six, Seven, Eight, Nine, Ten
        case Jack, Queen, King
        func simpleDescription() -> String {
            switch self {
            case .Ace:
                return "ace"
            case .Jack:
                return "jack"
            case .Queen:
                return "queen"
            case .King:
                return "king"
            default:
                return String(self.toRaw())
            }
        }
    }
    let ace = Rank.Ace
    let aceRawValue = ace.toRaw()

열거할 원래의 자료형과 첫 값은 명시해야한다. 이후의 값부터는 자동으로 순서대로 매겨진다. 문자열이나 부동소수점 열거형도 만들 수 있다.

`toRaw`와 `fromRaw`로 변환할 수 있다.

열거형의 멤버 값은 단순한 다른 이름이 아니라 실제의 값이다. 없는 값은 switch에서 다룰 필요가 없다.

    enum Suit {
        case Spades, Hearts, Diamonds, Clubs
        func simpleDescription() -> String {
            switch self {
            case .Spades:
                return "spades"
            case .Hearts:
                return "hearts"
            case .Diamonds:
                return "diamonds"
            case .Clubs:
                return "clubs"
            }
        }
    }
    let hearts = Suit.Hearts
    let heartsDescription = hearts.simpleDescription()

예제에서 let hearts에서는 자료형을 추론할 수 없으므로 Suit를 포함한 전체 이름을 써야하지만 switch에서는 이미 자료형을 알고 있으므로 Suit는 쓸 필요가 없다.

# 구조체

`struct`로 구조체를 만든다. 메서드와 초기화를 포함해 클래스와 비슷한 동작을 지원한다. 구조체는 항상 값이 복사되고 클래스는 항상 참조만 전달된다는 것이 다르다.

옮긴이: 델파이의 record/class와 같은 정책이다.

    struct Card {
        var rank: Rank
        var suit: Suit
        func simpleDescription() -> String {
            return "The \(rank.simpleDescription()) of \(suit.simpleDescription())"
        }
    }
    let threeOfSpades = Card(rank: .Three, suit: .Spades)
    let threeOfSpadesDescription = threeOfSpades.simpleDescription()’

# 값이 있는 열거형
    
열거형은 연관된 값을 가질 수도 있다.

    enum ServerResponse {
        case Result(String, String)
        case Error(String)
    }
     
    let success = ServerResponse.Result("6:00 am", "8:09 pm")
    let failure = ServerResponse.Error("Out of cheese.")
     
    switch success {
    case let .Result(sunrise, sunset):
        let serverResponse = "Sunrise is at \(sunrise) and sunset is at \(sunset)."
    case let .Error(error):
        let serverResponse = "Failure...  \(error)"
    }
    
`switch`에서 각 enum 값에 연관된 값을 뽑아올 수 있다.
