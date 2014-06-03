## 프로토콜과 확장

# 프로토콜

`protocol`로 프로토콜을 선언할 수 있다.

    protocol ExampleProtocol {
        var simpleDescription: String { get }
        mutating func adjust()
    }

클래스, 열거헝, 구조체 모두 프로토콜을 적용할 수 있다.

    class SimpleClass: ExampleProtocol {
        var simpleDescription: String = "A very simple class."
        var anotherProperty: Int = 69105
        func adjust() {
            simpleDescription += "  Now 100% adjusted."
        }
    }
    var a = SimpleClass()
    a.adjust()
    let aDescription = a.simpleDescription
     
    struct SimpleStructure: ExampleProtocol {
        var simpleDescription: String = "A simple structure"
        mutating func adjust() {
            simpleDescription += " (adjusted)"
        }
    }
    var b = SimpleStructure()
    b.adjust()
    let bDescription = b.simpleDescription’
    
SimpleStructure에는 구조체를 고친다는 표시로 `mutating` 예약어를 사용했다. 클래스는 항상 고칠 수 있으므로 SimpleClass에는 쓰지 않았다.

옮긴이: 오브젝티브-C의 프로토콜과도 비슷하고, 자바의 인터페이스나 C++의 순수 추상클래스의 개념과도 한층 더 가까워졌다. 오브젝티브-C에서 프로토콜은 2.0까지는 거의 카테고리 확장에 힌트를 주는 정도였다. (런타임에서 어떤 프로토콜을 구현했나 정보는 갖고 있지만 런타임에 구현되었다고 표시되어 있다고 꼭 구현되어 있다는 보장도 없었고, 역엔지니어링 밖에는 어떤 경우에도 쓰는 걸 본 적이 없다) 스위프트에서는 오브젝티브-C 3.0의 프로토콜 개념을 거의 그대로 가져가고 있다.

# 확장

`extension`으로 기존의 자료형에 기능을 확장할 수 있다. 다른 데 선언한 자료형은 물론이고 라이브러리나 프레임워크에 있는 자료형도 변경할 수 있다.

    extension Int: ExampleProtocol {
        var simpleDescription: String {
        return "The number \(self)"
        }
        mutating func adjust() {
            self += 42
        }
    }
    7.simpleDescription

옮긴이: 오브젝티브-C의 카테고리 확장과 같은 개념이다. 하지만 역시 모든 타입을 확장할 수 있다.
    
# 프로토콜과 자료형
프로토콜을 자료형 이름처럼 쓸 수 있다. 이 경우 프로토콜 밖에 선언된 메서드는 사용할 수 없다.

    let protocolValue: ExampleProtocol = a
    protocolValue.simpleDescription
    // protocolValue.anotherProperty  // Uncomment to see the error’

