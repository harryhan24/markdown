# [ES6] Promise

자바스크립트의 비동기서의 특징상 콜백 지옥에 빠지기 쉽다.
이런 콜백 지옥을 방지하기위해 ayncs를 쓰는것도 좋은 방법이지만
es6 문법중 하나인 promise 역시 좋은 대안이 될 수 있다.



**콜백지옥의 예**
```javascript
fs.readdir(source, function(err, files) {
  if (err) {
    console.log('Error finding files: ' + err)
  } else {
    files.forEach(function(filename, fileIndex) {
      console.log(filename)
      gm(source + filename).size(function(err, values) {
        if (err) {
          console.log('Error identifying file size: ' + err)
        } else {
          console.log(filename + ' : ' + values)
          aspect = (values.width / values.height)
          widths.forEach(function(width, widthIndex) {
            height = Math.round(width / aspect)
            console.log('resizing ' + filename + 'to ' + height + 'x' + height)
            this.resize(width, height).write(destination + 'w' + width + '_' + filename, function(err) {
              if (err) console.log('Error writing file: ' + err)
            })
          }.bind(this))
        }
      })
    })
  }
})
```

## promise 문법예시1

```javascript
var somePromise = new Promise((resolve, reject)=> {

    setTimeout(()=> {

        resolve('hey. it work!');
        //reject('unable to fulfill promise');

    }, 2500);

});


somePromise.then((message)=> {
    console.log('success:', message);
}, (err)=> {
    console.log('err', err);
});

```

resolve가 실행되면 success
reject가 실행되면 err를 보낸다.

promise패턴 안에서 인자를 reslove  또는 reject로 보내면
then 메서드를 통하여 해당 인자를 받아 내용을 기술한다.




## promise 문법예시2
```javascript
var asyncAdd = (a, b) => {
    return new Promise((resolve, reject)=> {
        setTimeout(()=> {
            if (typeof a === 'number' && typeof b === 'number') {
                resolve(a + b);
            }else{
                reject('argument muse be nubmer');
            }
        }, 1500)
    });
};

asyncAdd(5,7).then((res)=>{
    console.log(res);
    return asyncAdd(res, 33);
},(error)=>{
    console.log(error);
}).then((res)=>{
    console.log('should be 45', res);
}, (err)=>{
    console.log(err);
});
```
