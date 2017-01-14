# 프로토콜과 델리게이션

## 프로토콜
메서드의 전체적인 형태를 정의하여둔다.

### 사용하는 이유
특정한 이벤트의 콜백으로 메서드들이 선언되며 그 메서드가 프로토콜로 선언되어 있을경우
안해도되고 해도되는 옵셔널한 상태가 된다. 내가 구현이 필요할때만
해당 프로토콜을 찾아서 구현을 하면 된다.

## 델리게이션
특정 액션에 대한 반응하는 내용을 정의한다.
델리게이션을 사용하기 위해서는 어느쪽으로 이벤트를 내보낼 것인지 선언을 해야한다

 ```siwft3
 override func viewDidLoad() {
      super.viewDidLoad()
      // Do any additional setup after loading the view, typically from a nib.

      //델리게이션을 이쪽으로 가져온다.
      //self는 this(viewDidLoad)와 같다.
      nameTextField.delegate = self
  }

 ```

 위와 같이 사용하여준다.
