# react-native with redux

기본 구조 스키마

```
ios
android

src
├── actions
│   └── index.js
├── app.js
├── components
│   ├── LibraryList.js
│   ├── ListItem.js
│   └── common
│       ├── Button.js
│       ├── Card.js
│       ├── CardSection.js
│       ├── Header.js
│       ├── Input.js
│       ├── Spinner.js
│       └── index.js
└── reducers
    ├── LibraryList.json
    ├── LibraryReducer.js
    ├── SelectionReducer.js
    └── index.js

```


redux는 데이터를 한방향으로 모두 밀집되도록 만들어주는 라이브러리이다. 이렇게 할경우 각자의 개별 컴포넌트간의 데이터 통신으로 인한 무수한 에러들은 막아준다.



## LibraryList
데이터를 직접 연결하여 출력해주는 컴포넌트의 역활이다.

```javascript

import React, { Component } from 'react';
import { ListView } from 'react-native';
import {connect} from 'react-redux'; //react와 redux 를 연결시키기 위한 메서드 이렇게하면 데이터를 따로 가져올 필요가 없다.
import ListItem from './ListItem';


class LibraryList extends Component {

    //컴포넌트 mount 전 실행
    componentWillMount() {

      //ListView 관여 함수 페이스북 리액트 예제 참고
        const ds = new ListView.DataSource({
            rowHasChanged: (r1, r2)=> r1 !== r2
        });

        this.dataSource = ds.cloneWithRows(this.props.libraries);
    }

    //각 Row를 listItem 메서드를 통하여 렌더링 시켜준다.
    renderRow(library){
        return <ListItem library={library} />;
    }

    render() {
        return(
            //listView를 설정하여 데이터를 넣어준 배열과
            //각 render row 를 선언하여준다.
            <ListView
                dataSource={this.dataSource}
                renderRow={this.renderRow}
            />
        )

    }
}



// connect 함수를 통해 state중 원하는 데이터만
// 내부 props로 리턴하여준다.
const mapStateToProps = state => {
    return { libraries: state.libraries };
};
export default connect(mapStateToProps)(LibraryList);


//데이터를  import로 가져오는게 아닌 redux를 사용해야 한다
```
