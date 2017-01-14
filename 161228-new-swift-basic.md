# swift3 기초문법

## Decelation

## unary declation
이용하는 변수가 1개인 경우
```swift
amICool = !amICool
```

## biary declation
이용하는 변수가 2개인 경우
```swift
var temp = 4
var amICool = temp
```

## type inference
타입을 명시하지 않아도 타입을 자동으로 추론함

```swift
var st11r = "ehhlo, playgounrd"      //타입인퍼런스
var str1:String = "hello, playhroud" //자료형명시
```

## String

### string 합치기

```swift
var firstName = "jack"
var lastName = "bauer"
var age = 45;
var fullname = firstName + " " + lastName
```

### String interpolation
```swift
var fullName2 = "\(firstName) \(lastName) is \(age)"; //"jack bauer is 45"
```

### String.append
스트링을 이어붙이는 경우 append 메소드를 사용할 수 있다.

```swift
fullname.append(" III ") //"jack bauer III "

```


### String.capitalized

```swift3
var bookTitle = "revenge of the crab cakes"
bookTitle = bookTitle.capitalized
//result is "Revenge Of The Crab Cakes"
```
### String.lowercased()
모두 소문자로 바꿈
특히 로그인 아이디받을때 아이폰의 경우 첫글자가 대문자로 인식이 되는데 대소문자 구분안하고
아이디정보를 받을 때 유용

### contains와 replacingOccurences

```siwft3
var sentence = "what the fetch?! Heck that is crazy!"
if sentence.contains("fetch") || sentence.contains("Heck"){
    sentence.replacingOccurrences(of: "fetch", with: "tuna"); //"what the tuna?! Heck that is crazy!"
    sentence.replacingOccurrences(of: "Heck", with: "playa"); //"what the fetch?! playa that is crazy!"
}
```
- String.contains(string) 의 경우 단어를 포함하고 있는지를 확인하고 boolean값을 리턴

- replacingOccurrences(of: "바꿀단어", with: "바뀌어질 단어")


## Number

```siwft3
var age1 = 30         //type inefrence
var age1:int = 30     //타입명시
```

```siwft3
var someNum : UInt8 = 123123
```

타입을 Unit8, Unit16, Unit32등 더 세부적으로 정수형을 선언할 수 있지만 이럴경우 오버플로우에 주의하자


```siwft3
var area = 15 * 20 // 곱

var sum = 5 + 6 // 더하기

var diff = 10 - 3 //빼기

var div = 13 / 5 //result is 2

var reminader = 13 % 5; // result is 3
```

## 함수

```siwft3
func calculateArea(length: Int, width: Int) -> Int {
    return length * width
}
calculateArea(length:5, width:4)
```
기본적인 함수의 형태로 내부에서 사용할 인자명과 타입 그리고 리턴타입을 선언하여준다.


```siwft
func purchaseItem(currentBalance: inout Double, itemPirce:Double) -> Double {
    if itemPirce <= currentBalance{
        //이곳에서 바뀌면 내부에서도 바뀜
        currentBalance = currentBalance - itemPirce
        print("purchased item for: $ \(itemPirce)")
        return currentBalance - itemPirce
    }else{
        print("u r broke. u should learn!! something for saving money ! !")
        return currentBalance
    }
}

let newBalance = purchaseItem(currentBalance: &bankAccountBalance, itemPirce: sigourneyWeaverAlienStomperShoes)
```

메서드에서 inout인자를 넣어주고 값을 넘길때 &를 통한 참조형으로 넘겨줄경우 함수내부에서
값이 바뀔경우 해당 메모리의 값도 바뀌게 된다.

## logic 연산자

 - || or
- && AND
- != Not
- = Eqal


## optional

```swift3
var lotteryWinnings: Int?
```
일반적인 옵셔널 선언의 경우 '?'를 사용

옵셔널을 사용하는 이유는 value가 없을경우 나타나는 문제때문인데


```
class Car{
    var model: String?    
}

var vehicle: Car? //car 클래스를 옵셔널 선언.

//if let v = vehicle{
//    if let m = v.model{
//        print(m)
//    }
//}


// ?를 통하여 선언할경우 그 변수가 없을 경우에도 안전하게 사용할 수 있다.
// 하지만 !표를 먼저 선언할경우 오류가 나게 된다.
print(vehicle?.model)


```

이렇게 model이 정의되어있지 않았다하여도 optional로 감싸져 있기 때문에 오류가 나타나지 않는다.

```siwft3
print(lotteryWinnings!)
```
참조할 때 해당상태와 같은 형태로 사용하는것은 매우 위험하다.
반드시 아래와 같은 패턴으로 이용하여야한다.

```swift3
if lotteryWinnings != nil{
    print(lotteryWinnings!)
}
```
