# pickerview 구현

pickerview를 구현하기위해선 UIPickerViewDataSource,UIPickerViewDelegate 두개의 프로토콜을 뷰컨트롤러에 선언하여준다. 그 후 pickerview의 deletegation을 뷰컨트롤러로 설정하여주자.

## pickerview depth 개수 수현

```swift
func numberOfComponents(in pickerView: UIPickerView) -> Int {
        return 2
    }
```

## 피커뷰 내용을 채워줍니다.
```swift
func pickerView(_ pickerView: UIPickerView, titleForRow row: Int, forComponent component: Int) -> String? {

        //0번 컴포넌트 1번 채우고 2번채우고
        //1번 컴포넌트 1번 그 후 2번
        if component == 0{
            return carCompanyName[row]
        }else{
            return carModel[row]
        }
    }
```

각각 로우마다의 개수를 리턴하여줍니다.

## 전체 카운터 개수를 반환

```swift
func pickerView(_ pickerView: UIPickerView, numberOfRowsInComponent component: Int) -> Int {

        //컴포넌트가 첫 로우일때
        if component == 0{
            return carCompanyName.count
        }else{
            return carModel.count
        }
    }
```


## 컴포넌트가 변경될 때를 감지하여 리로드

```swift
//몇번 컴포넌트의 몇번째가 실행되나 감지
   func pickerView(_ pickerView: UIPickerView, didSelectRow row: Int, inComponent component: Int) {
       if component == 0 && row == 0 {
           carModel = tesla
           carModelImage = teslaImageNames
       }else if component == 0 && row == 1 {
           carModel = lamborghini
           carModelImage = lamborghiniImageNames
       }else if component == 0 && row == 2 {
           carModel = porsche
           carModelImage = porscheImageNames
       }

       //전체 피커뷰 리로드
       pickerView.reloadAllComponents()

       imgView.image = UIImage(named: carModelImage[pickerView.selectedRow(inComponent:1)])

   }
```ㅈ

## 초기화
```javascript
override func viewDidLoad() {
        super.viewDidLoad()
        //테슬라를 초기로
        carModel = tesla
        //이미지 배열역시 테슬라로 초기화 시켜줍니다.
        carModelImage = teslaImageNames

        //하드코딩으로 뷰 컨트롤.
        imgView.layer.cornerRadius = 50.0
        imgView.layer.masksToBounds = true

        // Do any additional setup after loading the view, typically from a nib.
    }
```
