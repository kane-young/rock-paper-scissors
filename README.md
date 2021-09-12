# 묵찌빠 게임 프로젝트

with [kangkyung](https://github.com/KangKyung) , [kio](https://github.com/Kioding)

📅 과제 진행 기간 : 2021-03-01 ~ 2021-03-05

<br>

## Overview

Console 을 통해서 랜덤 값을 주는 컴퓨터와 진행하는 묵찌빠 게임

<br>

**해당 프로젝트를 진행하면서 학습한 개념**

- commit 템플릿 생성, commit 메시지

- 일반화 추상화 개념 학습
- mutating 키워드 학습
- CaseIterable Protocol
- Comparable Protocol

<br>
<br>

### Flow Chart

<img width="296" alt="스크린샷 2021-09-12 오후 1 43 26" src="https://user-images.githubusercontent.com/64566207/132978112-0f172f47-cf0e-492f-a500-537b644b8974.png">

가위 바위 보 이후에 묵찌빠 실행되는 로직 구성

<br>

<br>

### 실행 화면

시작화면 -> 숫자를 통한 가위바위보 입력 -> 판정

![가위바위보](https://user-images.githubusercontent.com/64566207/132978386-a93d0823-cd4f-447c-8f64-cc2e7cde2b5f.gif)



가위바위보 이후 -> 숫자를 통한 묵찌빠 입력 -> 판정(게임 종료)

![묵찌빠](https://user-images.githubusercontent.com/64566207/132978387-0a21b504-fa86-4843-8689-b9567fa14b08.gif)

<br>

<br>

### 프로젝트 일정 기록

- **2021.03.02 (화)**

  팀원들과 git message 템플릿 생성, [git commit convention](https://github.com/kane-young/rock-paper-scissors/blob/main/CommitConvention.md) 정함

  `RockPaperScissors ` 클래스 청사진 그리기, `RockPaperScissors` 클래스 내에 가위 바위 보 구현

  Pull Request를 통한 Step1 리뷰 요청

- **2021.03.03 (수)**

  class, struct에 대한 개념 학습

- **2021.03.04 (목)**

  리뷰에 대한 팀원들 간의 회의 및 코드 수정

  Step1 merge

- **2021.03.05 (금)**

  `MukjjibbaGame` 클래스 청사진 그리기, 묵찌빠 구현

  Pull Request를 통한 Step2 리뷰 요청

<br>

<br>

## 학습 내용 기록

### Pull Request를 통한 리뷰

[Step1 리뷰](https://github.com/yagom-academy/ios-rock-paper-scissors/pull/27)

[Step2 리뷰](https://github.com/yagom-academy/ios-rock-paper-scissors/pull/44)

<br>

<br>

### git commit 컨벤션 및 템플릿

[git commit convention](https://github.com/kane-young/rock-paper-scissors/blob/main/CommitConvention.md) 

템플릿 참고 자료)

 [좋은 커밋 메시지를 작성하기 위한 커밋 템플릿 만들어보기](https://junwoo45.github.io/2020-02-06-commit_template/)

[udacity git style guide](https://udacity.github.io/git-styleguide/)

<br>

<br>

### 일반화 추상화 개념 학습

- 일반화 : **서로 다른 개체들로부터 공통된 개념을 추출하는 것을 말한다.**
- 추상화 : **복잡함 속에서 필요한 관점만을 추출하는 것을 말한다.**

묵찌빠 게임과 가위바위보 게임의 공통된 기능을 중복해서 구현하지 않는 구조를 고민함

```swift
class MukjjibbaGame: RockPaperScissorsGame {
  //...
}
```

묵찌빠가 가위바위보를 상속하는 구조를 선택

<br>

<br>

### mutating 키워드 학습

값 타입 인스턴스의 메서드가 인스턴스 프로퍼티 값을 변경하고자 하는 경우, `mutating` 키워드를 적어서 값 변경이 되는 것을 확실하게 해준다!

```swift
struct Person {
    var name: String

    mutating func makeAnonymous() {
        name = "Anonymous"
    }
}
```

<br>

<br>

### CaseIterable 프로토콜 학습

참고자료) [Apple Developer's Document - CaseIterable](https://developer.apple.com/documentation/swift/caseiterable)

```swift
enum CompassDirection: CaseIterable {
    case north, south, east, west
}

print("There are \(CompassDirection.allCases.count) directions.")
// Prints "There are 4 directions."
let caseList = CompassDirection.allCases
                               .map({ "\($0)" })
                               .joined(separator: ", ")
// caseList == "north, south, east, west"
```

열거형 케이스들을 선회할 때 유용하게 사용할 수 있는 프로토콜이다

`allCases` 를 통해서 case 전부를 array element 로 가지고 있는 배열을 얻을 수 있다

<br>

<br>

### Comparable 프로토콜 학습

참고자료) [Apple Developer's Document - Comparable](https://developer.apple.com/documentation/swift/comparable)

```swift
struct Date {
    let year: Int
    let month: Int
    let day: Int
}

extension Date: Comparable {
    static func < (lhs: Date, rhs: Date) -> Bool {
        if lhs.year != rhs.year {
            return lhs.year < rhs.year
        } else if lhs.month != rhs.month {
            return lhs.month < rhs.month
        } else {
            return lhs.day < rhs.day
        }
    }
}
```

사용자 정의한 타입의 인스턴스를 쉽게 비교할 수 있게 해준다!



```swift
static func < (lhs: Hand, rhs: Hand) -> Bool {
    if (lhs == .scissors && rhs == .rock)
    || (lhs == .paper && rhs == .scissors)
    || (lhs == .rock && rhs == .paper) {
      return true
    } else {
      return false
    }
}
```

가위 바위 보의 우위를 표현하기에 매우 적합하다!!



<br>

<br>

## 프로젝트를 끝마치고

### UML을 통해서 쉽게 파악하는 구조

참고자료) [Swift에 적합한 UML 작성 방법 블로그](https://zdodev.github.io/uml/swift/UML-Class-Diagram/#dependency-의존-관계)

[UML에 대한 학습 TIL](https://velog.io/@leeyoungwoozz/TIL-2021.03.23-Tue)

<br>

`MukjjibbaGame` 클래스와 `RockPaperScissorsGame` 의 관계에서 상속 관계, 의존 관계를 볼 수 있었다

프로젝트 이후에 `SOLID` 법칙을 배워서 알았지만 굉장히 비효율적인 구조로 작성했다는 것을 깨달았다!

가위바위보 클래스를 추상화 시켜서 추상화 시킨 프로토콜을 묵찌빠 클래스에서 주입 받는다면, 확장에는 열리고 변경에는 닫힌 구조가 될 것 이다

<img width="311" alt="스크린샷 2021-09-12 오후 4 40 09" src="https://user-images.githubusercontent.com/64566207/132978110-da3501ac-7a3f-499e-87ae-627c2d3b3d66.png">



`RockPaperScissorsGame` 가 `Hand` 타입과 `GameError`에 의존하는 구조를 가지고 있다

<img width="588" alt="스크린샷 2021-09-12 오후 4 37 03" src="https://user-images.githubusercontent.com/64566207/132978113-b41144c9-44e8-4ca4-9284-fcd77bc22ac7.png">

`MukjjibbaGame` 가 `GamePlayer` , `Hand` , `GameError` 에 집합관계, 의존관계를 가지는 구조를 가지고 있다

<img width="607" alt="스크린샷 2021-09-12 오후 4 36 16" src="https://user-images.githubusercontent.com/64566207/132978114-d077c1fa-0d3f-468a-be57-6927604f5a76.png">



### 접근 제한자

접근 제한자는 코드를 작성한 사람의 의도대로 타입에 대한 인터페이스의 공개 정도를 정할 수 있다. 이는 매우 중요한 작업으로 `private` 접근제한자를 통해서 `Dynamic Dispatch` 또한 최소화할 수 있다

[Dynamic Dispatch 에 대한 학습 및 기록](https://velog.io/@leeyoungwoozz/TIL-2021.03.15-Mon)

