# as 형변환와 키보드 닫기

```swift3
@IBOutlet weak var selectDatePicker: UIButton!
var buttonTag:Int = 1;

@IBAction func departSelectDate(_ sender: Any) {
        if selectDatePicker.isHidden == false{
            selectDatePicker.isHidden = true
        }else{
            selectDatePicker.isHidden = false
        }
        buttonTag = (sender as! UIButton).tag;
    }
```

selectDatePicker의 상태값을 보고 분기시킨다.
요기서 buttonTag가 중요한 부분인데 sender로 받은 버튼값을
as! 메서드를 통해 UIButton으로 변경한 후 거기서 태그값을 가져온다.

```swift3
override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {
        self.view.endEditing(true)
    }
```

뷰를 눌렀을 때 실행되는 메서드다(touchesBegan)

바탕 아무 뷰를 눌렀을 경우 self.view.endEditing(true) 에디팅이 끝나게된다.

self의 경우 뷰커늩롤러이다.
