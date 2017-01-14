# 앱의 생명주기
가장 먼저 AppDelegate가 호출된다.


## 각 메서드들

### willFinishLaunchingWithOptions
뷰컨트롤러를 만든다.
### didFinishLaunchingWithOptions
뷰 컨트롤러 만드는게 끝난 시점
### applicationWillResignActive
전화가 오거나 문자가 오거나 바탕화면에 나가는 시점
### applicationDidEnterBackground
바탕화면으로 들어갔을 때
### applicationWillEnterForeground
background 어플이 실행됬을 때
### applicationDidBecomeActive
어플이 다시한번 active 됬을 때
### applicationWillTerminate
어플이 꺼졌을 떄

## view  관련

```
import UIKit

class ViewController: UIViewController {

    var a = 1

    override func loadView(){
        //뷰를 직접 붙여야할 경우
        a += 1
        //parent 함수를 실행하는 경우.
        super.loadView()
        print(a)
    }
    //컨트롤러 생성자
    override func viewDidLoad() {
        super.viewDidLoad()
        print("view did load")
        // Do any additional setup after loading the view, typically from a nib.
    }
    //뷰생성시
    override func viewWillAppear(_ animated: Bool) {
        super.viewDidAppear(true)
        print("viewWillAppear")
    }
    //뷰 생성 끝나고
    override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(true)
        print("viewDidAppear")
    }
    //
    override func viewWillDisappear(_ animated: Bool) {
        super.viewDidDisappear(true)
        print("viewWillDisappear")
    }



}
```


## window

```
//Appdelegation 파일

    var window: UIWindow?
    //window?.rootViewContoller
    //모든 뷰컨트롤러는 윈도우의 하위 객체이다.

    //window?.rootViewConrtoller = ViewController()
    //사실은 이게 생략되어어있다..
```
