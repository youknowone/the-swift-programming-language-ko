## 제너릭

제너릭 함수나 자료형을 만들 수 있다.

    func repeat<ItemType>(item: ItemType, times: Int) -> ItemType[] {
        var result = ItemType[]()
        for i in 0..times {
            result += item
        }
        return result
    }
    repeat("knock", 4)

다른 예제

    // Reimplement the Swift standard library's optional type
    enum OptionalValue<T> {
        case None
        case Some(T)
    }
    var possibleInteger: OptionalValue<Int> = .None
    possibleInteger = .Some(100)

옮긴이: 오브젝티브-C의 <del>고대</del>전근대적 자료형 지옥에서 헤어나오신 것을 축하드립니다. 만세!

`where`로 프로토콜 구현 여부, 두 타입이 같을 것, 특정 수퍼클래스를 가질 것 등 조건을 지정할 수 있습니다.

    func anyCommonElements <T, U where T: Sequence, U: Sequence, T.GeneratorType.Element: Equatable, T.GeneratorType.Element == U.GeneratorType.Element> (lhs: T, rhs: U) -> Bool {
        for lhsItem in lhs {
            for rhsItem in rhs {
                if lhsItem == rhsItem {
                    return true
                }
            }
        }
        return false
    }
    anyCommonElements([1, 2, 3], [3])

단순한 경우에는 where 없이 `<T where T: Equatable>` 대신 `<T: Equatable>`으로 쓸 수 있습니다.

