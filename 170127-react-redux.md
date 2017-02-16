# redux의 이해

[Action] => [Redux] => [State]

Action에서 어떠한 데이터 처리인지 그리고 어떠한 데이터인지를 넘겨주면 Redux는
그 데이터를 가공하여 리턴하는 역활만 한다.

## 문자열 분리

```javascript
//reducer에서 state(데이터)와 action을 받으면 그걸 split하여 리턴한다
const reducer = (state = [], action)=>{
  if(action.type === 'split_string'){
    return action.payload.aplit('');
  }

  return state;
}

//리덕스에 저장
const store = Redux.createStore(reducer)

//action에서 데이터와 타입 정의
const action  = {
  type: 'split_string',
  payload: 'asdf'
}


store.dispatch(action) //데이터를 가공

store.getState //데이터 리턴

```
## 데이터 추가

```javascript


if(action.type === 'split_string'){
  return action.payload.aplit('');
}else{
  //push와 비슷함
  // ...state = {a},{s},{d},{f} 형태의 데이터에 {a}도 같이 반환
  //state에는 영향을 주지 않는다.
  return [...state, action.payload];
}

///////////////////생략

const action2 = {
  type: 'add_character',
  payload:'a'
}


}
```
