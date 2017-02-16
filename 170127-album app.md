# react-native app 만들기

brwe 설치 후 node와 watchman 설치
```
brew install node
brew install watchman
```

react-native-cli 설치
```
npm install -g react-native-cli
```


설치법 및 ios 실행법
```
react-native install project-Name
react-native run-ios
```

react-native 역시 react 와 마찬가지로 컴포넌트 단위로 뷰를 짜주어야한다.

오직 root 컴포넌트만 AppRegistry를 사용할 수 있다.

## 기본 프레임


```javascript

// index.ios.js - place ode in here for ios

// import a library to help create a component
import React from "react";
import { Text, AppRegistry, View } from "react-native";
import Header from "./src/components/header";
import AlbumList from "./src/components/AlbumList";

// 컴포넌트를 만들자

//OLD
// const App = () =>{
//     return(
//       <Text>Some Text</Text>
//     );
// };


//New
const App = () =>(
    //다이렉트 선언도 가능
    //flex:1은 화면 전체를 뜻합니다.
    <View style={{flex:1}}>
    //헤더와 AlbumList를 가져와 뷰에 쀼러줍니다.
        <Header headerText="Albums" />
        <AlbumList />
    </View>
);

//render it to device
//앨범에다가 App을 실행해 !


//albums와 project이름을 일치시켜야한다. 그 후 렌더링할 method 이름을 선언하여준다.
AppRegistry.registerComponent("albums", () => App);
```


## 헤더만들기
header.js
```javascript
// Import Libraries for making a component
import React from "react";

//뷰는 포지션과 스타일을 관장한다. div 같은 느낌
import {Text, View} from "react-native";
// make a compontnt


//props = property ,data rendring 등의 용도로 활용
const Header = (props) => {

    const { textStyle, viewStyle} = styles;


    return(
        <View style={viewStyle}>
            <Text style={textStyle}>{props.headerText}</Text>
        </View>
    )
};


//스타일을 아래와 같이 선언한다.
const styles = {
    viewStyle:{
      backgroundColor:'#f8f8f8',
        //가운데정렬
        justifyContent: 'center',
        //중앙정렬
        alignItems:'center',
        height:60,
        //맨 위 간격을 만들어 모바일의 시간 부분을 가리지 않도록
        paddingTop:15,
        shadowColor: '#000',
        shadowOffset:{width:0, height:2},
        shadowOpacity: 0.2,
        elevation:2,
        position:'relative'
    },
    textStyle: {
        fontSize: 20
    }
}
//당장 렌더를 언하지 않을수도 있기에 일단은 쪼개어 놓는다.
//make the compontnt able to other paort of the app

export default  Header;
```
## 리스트 화면
```javascript
// Import Libraries for making a component
import React, {Component} from "react";

//뷰는 포지션과 스타일을 관장한다. div 같은 느낌
import {View, ScrollView} from "react-native";
import axios from "axios";
import AlbumDetail from './AlbumDetail';

// make a compontnt


//컴포넌트도 가져오야합니다.
// import component
//class based component

class AlbumList extends Component {

    state = {albums: []};

    componentWillMount() {
        // ASYNC HTTP Request to get albums from the API.
        // eslint-disable-next-line
        axios.get('https://rallycoding.herokuapp.com/api/music_albums')
            .then(response => this.setState({albums: response.data}));
    }

    renderAlbums() {
        //map is array helper
        //array 개수만큼 실행되게 됩니다.
        //albums가 들어간 만큼 title이 출력됩니다.
        //대소문자 구분
        return this.state.albums.map(album =>
            <AlbumDetail key={album.title} album={album}/>
        );
    }

    render() {
        console.log(this.state);


        return (
            <ScrollView>
                {this.renderAlbums()}
            </ScrollView>
        );
    };
}
;

export default AlbumList;
```

## 디테일 화면
```javascript
import React from 'react';
import {View, Text, Image, Linking} from 'react-native';
import Card from './Card';
import CardSection from './CardSection';
import Button from './Button'

const AlbumDetail = ({album}) => {

    const {title,artist,thumbnail_image,image, url} = album;
    const {
        thumbnailStyle,
        thumbnailContainerStyle,
        headerContentStyle,
        headerTextStyle,
        imageStyle
    } = styles;

    return(
        <Card>
            <CardSection>
                <View style={thumbnailContainerStyle}>
                    <Image
                        style={thumbnailStyle}
                        source={{uri: thumbnail_image}}
                    />
                </View>
                <View style={headerContentStyle}>
                    <Text style={headerTextStyle}>{title}</Text>
                    <Text>{artist}</Text>
                </View>
            </CardSection>

            <CardSection>
                <Image
                    style={imageStyle}
                    source={{uri:image}}
                />
            </CardSection>

            <CardSection>
                <Button onPress={()=>Linking.openURL(url)}>
                    buy it
                </Button>
            </CardSection>
        </Card>
    )
};

const styles = {
  headerContentStyle:{
      flexDirection:'column',
      justifyContent:'space-around'
  },
    thumbnailStyle:{
        height:50,
        width:50
    },
    headerTextStyle:{
        fontSize:18
    },
    thumbnailContainerStyle:{
        justifyContent:'center',
        alignItems:'center',
        marginLeft:10,
        marginRight:10,
    },
    imageStyle:{
        height:300,
        flex:1,
        width:null
    }
};

export default AlbumDetail;
```

## card.js
```javascript
import React from 'react';
import {View} from 'react-native';

const Card = (props) =>{
    return(
        <View style={styles.containerStyle}>
            {/*하위 내용 보여주기*/}
            {props.children}
        </View>
    );
};

const styles={
    containerStyle:{
        borderWidth:1,
        borderRadius:2,
        borderColor:'#ddd',
        borderBottomWidth:0,
        shadowColor:'#000',
        shadowOffset:{width:0, height:2},
        shadowOpacity:0.1,
        shadowRadius:2,
        elevation:1,
        marginLeft:5,
        marginRight:5,
        marginTop:10
    }
}

export default Card;
```

## cardsection.js

```javascript
import React from 'react';
import {View} from 'react-native';
//카드 섹션은 단지 데코를 위한 내용
const CardSection = (props) =>{
    return(
        <View style={style.containerStyle}>
            {props.children}
        </View>
    );
};

const style={
    containerStyle:{
        borderBottomWidth:1,
        padding:5,
        backgroundColor:'#fff',
        justifyContent:'flex-start',
        //one line by oneline
        flexDirection:'row',
        borderColor: '#ddd',
        position: 'relative'
    }
}

export default CardSection;
```
