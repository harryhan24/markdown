# swift ios 개발에서의 MVC 패턴

## 디렉토리 구조
```
Util - 유틸리티, 3rd 관련 내용
Resources - 이미지파일, 폰트파일 등등.
Model - 데이터 관련 다루는 내용
View - 스토리보드와 관련된 내용
Controller - 전체적인 제어 역활
```


## Model의 일반적인 형태

```
class Person{
  //사용할 변수들을 선언해주며 되도록 외부에서 참조될 수 없는 private으로 선언
  private var _firstName: String!
  private var _lastName: String!

//get과 set를 통해서 데이터를 컨트롤
  var firstName: String{
    get{
      return _firstName
    }
    set{
      _firstName = newValue
    }
  }

  var lastName: String{
    return _lastName
  }


  //이니셜라이징
  init(first:String, last:String){
    self._firstName = first
    self._lastName = lase
  }

  //이렇게 데이터를 다루는 내용은 되도록 Model에서 전부 처리하도록 한다
  var fullName: String{
    return "\(_firstName) \(_lastName)"
  }
}
```


## view의 일반적인 형태

이미지 UI를 다룰 경우 해당 내용을 다룰 수 있는 코코아 터치 프레임워크 파일을만들어 다룬다.
일단 클래스를 UIImageView등과 같이 UI내용을 상속받을 수 있는 형식으로 파일을 만든다.

그리고 해당 이미지뷰 UI의 클래스를 만들어낸 클래스 명과 일치시켜준다

![Pasted Graphic 7](http://i.imgur.com/oatXYq7.png)

```object-c
class RoundedImageView: UIImageView{
  //viewDidLoad와 비슷한 역활
  override func awakeFromNib(){
    //이곳에서 self는 연결된 UI를 의미한다.
    self.layer.cornerRadius = 5.0
  }
}
```


## controlloer
대망의 컨트롤러
클래스를 초기화 한다거나 각 뷰들을 모델과 연결해주는 작업을 한다.

```swift
class ViewControlloer: UIViewController{
  @IBOutlet weak var renameField: UITextField!
  @IBOutlet weak var fullName: UILabel!
  //DB init
  let person = Person(first:"John", last:"Hancock")

  oveeride func videDidLoad(){
    super.viewDidLoad()

    fullName.text = person.fullName
  }

  @IBAction func btnPressed(sender:AnyObject){
    if let txt = renameField.text{
      person.firstName = textfullName.text = person.fullName
    }
  }
}
```
