# swift3 기초문법 정리

## 선언
var 변수 - 재정의 가능
let 상수 - 재정의 불가

값 자동추정
```swift3
var maxiumLogin = 10
```

선언시 미리 타입 선언
```swift3
var welcome:String
```
## 배열

### 기본문법
```swift3
var comment:Array<String> = []
var comment2:[String] = []
```

### 배열추가

```swift3
comment.append("Anna")
comment += ["alex"]
```

### 배열 값에 접근

```siwft3
comment3[1] = "aaa";
```

### 딕셔너리
key와 value로만 구성되어있는 값의 집합

#### 선언
```swift3
var legs:Dictionary<String, Int> = [:] //풀문법
var legs1:[String:Int] = [:]
```

#### 초기화
```swift3
var arg1 = ["ant":5,"angke":8]
```

## 반복문

### for in
우리가 일반적으로 보는 for(int i = 0; i<10; i++) 형태의 문법은 siwft3에는 없다.


1~5까지 실행

```swift3
for index in 1...5{
  print("\index) time 5 is \(index*5)")
}

// 1 times 5 is 5
// 1 times 5 is 10
// 1 times 5 is 15
// 1 times 5 is 20
// 1 times 5 is 25
```

#### 배열을 인자로 사용할 경우

```swift3
let names = ["ann","alex","jack","kim"]

for name in names{
  print("hello, \(name)!")
}
```

#### 반복문 리터럴

```swift3
배열 리터럴
for name in ["anna","alex”,”jack","braidn"]{
    print("hello, \(name)");
}

딕셔너리 리터럴
for(animalName, legs) in ["ant":5,"gang":5,"lelel":10]{
    print("animals \(animalName) is \(legs)");
}
```

#### 각 인자값이 필요없을 경우
```swift3
let base = 3
let power = 10
let answer 1

for _ in 1...power{
  answer *= base
}

print("\(base) to the power of \(power) is \(answer)")
```
위처럼 변수가 필요 없을 경우는 언더바로만 선언한다.

### while

```swift3

//while 차일때만
while condition{

}

//do while같은 개념
repeat {

} while

```

## 조건문

### if

```swift3
let age = 20

if age < 3 {
    print("baby")
}else if age >= 3 && age < 20{
    print("child")
}else{
    print("adult")
}
```

### switch

default 꼭 선언해주어야 함.
일반적인

```swift3
switch age{
  Case0:
  case1:
  case:2
  break;
}

```
위와 같은 형태의 문장은 성립하지 않는다.


```swift3
switch age {
case 0:
    print("baby")
case 1,2:
    print("baby")
case 3 ... 20: //확장문법 20까지 걸림.
    print("teenager")
default:
    print("Adult")
}
```

## 함수
swift3의 경우 일반적으로 외부변수명과 내부인자명을 선언해주어야 한다.
각각 argument label과 parametter name이라 하며

```swift3
func somefunc(argumentLabel parapmeterName:int){
  //parapmeterName이 내부에서 쓰인다.

}
```

```swift3
func somefunc(para:Int = 12){
  //위처럼 하나만 선언하는경우 내부인자명과 외부변수명의 이름이 같다.
}

somefunc(para:6)
somefunc() // 입력하지 않은 경우 초기값 12로 설정됨
```

### 일반적 선언 예시

```swift3
func sayHello(){
    print("hello");
}

sayHello();

func sayHello2(name:String){
    print("hello \(name)")
}

sayHello2(name:"choi");

func sayHello3(name:String) -> String{
    return "hello " + name;
}

print(sayHello3(name: "jackson"));

func sayHello4(name:String = "Park"){
    print("hello \(name)")
}

sayHello4();
sayHello4(name:"gin");

func sayHello5(insertYourName name:String, internationalAge age:Int){
    print("hello \(name) is \(age) years old");
}

sayHello5(insertYourName: "kim", internationalAge: 22);

func sayHello6(name:String, _ age:Int) -> String{
    return "hello \(name) is \(age) years old" ;
}

//언더바로 쓸경우 생략가능.
print(sayHello6(name: "aaa", 5));
```

## 클래스

**클래스와 구조체의 차이는 클래스의 경우 상속이 되며 형변환이 가능하다.**

### 일반적인 클래스 선언
```swift3
class Vehicle{
    var currentSpeed = 0.0; //stored property
    var description:String{
        return "travaling at \(currentSpeed) miles per hour"
    }

    func makeNoise() {
        print("Noiiiiise1!!!");
    }
}

var car1 = Vehicle();
car1.makeNoise();
car1.currentSpeed = 5.5;

print("Vehicle: \(car1.description)”);
```

### 상속과 오버라이딩
```siwft3
class Vehicle{
    var currentSpeed = 0.0; //stored property
    var description:String{
        return "travaling at \(currentSpeed) miles per hour"
    }

    func makeNoise() {
        print("Noiiiiise1!!!");
    }
}

var car1 = Vehicle();
car1.currentSpeed = 5.5;

car1.makeNoise();

print("Vehicle: \(car1.description)");



//상속
class Bicycle:Vehicle{
    var hasBasket = false;
}

let bicycle = Bicycle();
bicycle.hasBasket = true;
bicycle.currentSpeed = 15;

print(bicycle.description);

class Tandem:Bicycle{
    var currentNumberOfPassenger = 0;
    override var description: String{
        return "travelling at \(currentSpeed) mile per hour and \(currentNumberOfPassenger), and basket: \(hasBasket)"
    }
}

let tendem = Tandem();
tendem.hasBasket = true;
print(tendem.description);

class Train:Vehicle{
    override func makeNoise() {
        print("oooo");
    }
}


var train = Train();
train.makeNoise();




class Car:Vehicle{
    var gear = 1;
    override var description:String{

        //상위 클래스의 decription을 가져와서 뒷부분만 string을 추가해줌.
        return super.description + "in gear \(gear)"
    }
}


```


### observer
클래스가 선언될때 실행된다. didSet은 선언 후 willSet은 선언직전
```

//observer

let car = Car()
car.currentSpeed = 25.0
car.gear = 3
print("car:\(car.description)");

class AutomagicCar:Car{
    override var currentSpeed: Double{
        didSet{
            gear = Int(currentSpeed/10)+1;
        }
    }
}

let automagic = AutomagicCar();

//이때 기어값이 바뀌게 됨.
automagic.currentSpeed = 30.0;

//willset은 데이터 변경 직전.

print("Automagic car:\(automagic.description)”);


```



## 구조체

각각의 내용을 전부 각각 선언할려면 조회하는데 어려움이 많다.

```swift3
var name = ["Park","Jac","Kim","lee"]
var age = [3,4,5,6]
var height = [40,50,60,70]

print(name[0],age[0],height[0]);


```

위와같이 복잡해지는걸 방지하기 위해 구조체를 활용하자

```
//해결을 위해 구조체를 사용하자.
struct Student{
    var name:String
    var age:Int
    var height:Int
}

//안에 함수도 넣을 수 있지만 상속이 안됨.

var stduent1 = Student(name: "park", age: 3, height: 40);
var stduent2 = Student(name: "kim", age: 5, height: 60);

```

## optional

물음표를 넣어 선언하면 값에 nil을 넣을 수 있다.

optional을 쓰는 이유는 값에 nil 값을 넣기 위함인데

nil 선언으로 인한 문제점을 피할 수 있다.


```swift3
class Optional{
    // 헬로로 초기화
//    var optionalString:String? = "hello"

    //물음표를 넣으면 String에 null값도 넣을 수 있다.


    var optionalString:String? = "hello";

    func hello(){
        //optionalString = nil;
        print(optionalString == nil);

        //물음표가 있는 상태에서는 값의 형이 optional형이다. 하지만
        //그럴경우 느낌표를 붙여 언랩핑 시켜야한다.
        print(optionalString!);

    }
}

var option = Optional();
option.hello();
```
