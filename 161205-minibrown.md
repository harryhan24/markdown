# swift 미니브라우저 만들기

> Noticce: IBOutlet에서 weak과 Strong이 있다.
> Strong은 뷰가 삭제되도 프로퍼티가 메모리에서 삭제되지않고
> Weak은 사라진다.
> 씬이 삭제되고 다시 생성되는 상황이면 Strong
> 그렇지 않다면 Weak

## Delegation
콜백함수처럼 어떤 동장이 끝난 후 동작을 알려줄 때 Delegation을
활용하여준다.

### UITextFieldDelegate

키보드에서 return을 누를 때 실행되며 textField를
viewController로 Ctrl + 드래그하여 delegate을 지정해주자.

### UIWebViewDelegate

웹브라우저가 로딩되거나 로딩이 끝나는 시점등을 delegate을 통해 알려준다.


## 예시
```swift3
@IBOutlet weak var mainWebView: UIWebView!

override func viewDidLoad() {

        super.viewDidLoad()
        let urlString = "https://www.facebook.com"
        //url 로드
        mainWebView.loadRequest(URLRequest(url:URL(string:urlString)!));
        urlTextField.text = urlString;
    }
```

url을 받은 후 loadRequest를 통하여 로딩시켜준다.
URLRequest는 optional이므로 unwrapping 시켜준다.

![11](http://i.imgur.com/q6MiGqJ.png)

WebView를 직접 오른쪽 버튼을 눌러 뒤로가기 앞으로가기등을
버튼과 연결이 가능하다.


### return을 눌렀을 때

```swift3
func textFieldShouldReturn(_ textField: UITextField) -> Bool {
        var urlString = "\(urlTextField.text!)"
        if !urlString.hasPrefix("https;//"){
            urlString = "https://\(urlTextField.text!)"
        }
        mainWebView.loadRequest(URLRequest(url:URL(string:urlString)!));
        textField.resignFirstResponder();
        return true
    }
```
