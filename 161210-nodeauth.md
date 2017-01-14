# nodejs 세션을 통한 로그인/회원가입

## 가입설정

```javascript
app.post('/auth/register', function(req, res){
  hasher({password:req.body.password}, function(err, pass, salt, hash){
    var user = {
      username:req.body.username,
      password:hash,
      salt:salt,
      displayName:req.body.displayName
    };
    users.push(user);
    req.session.displayName = req.body.displayName;
    req.session.save(function(){
      res.redirect('/welcome');
    });
  });
});
```

password 객체를 받아 salt(인코딩된 base64 문자열)을 생성하고 해당 문자열을 통하여
hash(암호화된 값)를 만들어낸다.


그 후  아래 메서드를 통해 세션을 할당하고 저장 한 후 콜백함수로 welcome페이지로 보낸다.
req.session.displayName = req.body.displayName;

requesst에서 session객체를 사용하려면

```javascript
var session = require('express-session');

var FileStore = require('session-file-store')(session);
app.use(session({
  secret: '1234DSFs@adf1234!@#$asd',
  resave: false,
  saveUninitialized: true,
  store:new FileStore()
}));
```

위 코드를 통하여 미리 설정해주어야 한다


## 로그인

 ```javascript
 app.post('/auth/login', function(req, res){
  var uname = req.body.username;
  var pwd = req.body.password;
  for(var i=0; i<users.length; i++){
    var user = users[i];
    if(uname === user.username) {
      return hasher({password:pwd, salt:user.salt}, function(err, pass, salt, hash){
        if(hash === user.password){
          req.session.displayName = user.displayName;
          req.session.save(function(){
            res.redirect('/welcome');
          })
        } else {
          res.send('Who are you? <a href="/auth/login">login</a>');
        }
      });
    }
  }
  res.send('Who are you? 2<a href="/auth/login">login</a>');
});
 ```
아이디와 비밀번호를 받아 일치하는 회원이 있는지 찾아준다  (메모리에 저장한 데이터라  for을 이용)
패스워드에 salt값으로 암호환 된 내용과  사용자에게 받은 값을 salt값으로 암호화 한게
맞는지 확인한다.


## 로그아웃

```javascript
app.get('/auth/logout', function(req, res){
  delete req.session.displayName;
  res.redirect('/welcome');
});
```

세션 삭제를 통한 로그아웃 구현

## 사용자페이지

```javascript
app.get('/welcome', function(req, res){
  if(req.session.displayName) {
    res.send(`
      <h1>Hello, ${req.session.displayName}</h1>
      <a href="/auth/logout">logout</a>
    `);
  } else {
    res.send(`
      <h1>Welcome</h1>
      <ul>
        <li><a href="/auth/login">Login</a></li>
        <li><a href="/auth/register">Register</a></li>
      </ul>
    `);
  }
});
```
세션에 해당 사용자가 있을경우는 메세지를 보여주고 아닐 경우는
로그인 페이지 출력


## passport.js

```javascript
app.use(passport.initialize());
app.use(passport.session());
```
패스포트를 사용하기 위한 미들웨어

```javascript
app.post(
  '/auth/login',
  passport.authenticate(
    'local',
    {
      successRedirect: '/welcome',
      failureRedirect: '/auth/login',
      failureFlash: false
    }
  )
);
```
login은 post 로 데이터를 받았을 경우 passport를 통해 검증을 하고
successRedirect는 성공하였을 경우의 링크 는 아닐경우의 링크를
출력한다.

```javascript  
passport.use(new LocalStrategy(
  function(username, password, done){
    var uname = username;
    var pwd = password;
    for(var i=0; i<users.length; i++){
      var user = users[i];
      if(uname === user.username) {
        return hasher({password:pwd, salt:user.salt}, function(err, pass, salt, hash){
          if(hash === user.password){
            console.log('LocalStrategy', user);
            done(null, user);
          } else {
            done(null, false);
          }
        });
      }
    }
    done(null, false);
  }
));
```

username과  password, 콜백함수를 전달받고
아이디와 패스워드를 통하여 검증을 한 후 콜백함수를 실행한다.
성공하였을 경우에는 데이터를 전달하고 그렇지 않았을 경우  false를 리턴

로그인에 성공을 하였을 경우 아래 메서드를 호출한다.

```javascript
passport.serializeUser(function(user, done) {
  console.log('serializeUser', user);
  done(null, user.authId);
});
```

인증이 된 경우 페이지에 접근 시 마다  deserializeUser를 실행하게된다.

```javascript
assport.deserializeUser(function(id, done) {
          User.findById(id, function(err, user) {
            done(err, user);
          });
        });
```

db에 계속 요청하기보다  reddis나 세션에 모든 데이터를 집어넣도록 하자.


## 쿠키

```javascript
app.use(cookieParser());

app.get('/count', function(req,res){

  res.cookie('count', 1);
  res.send('count:'+req.cookies.count);
});

```

쿠키값 저장


```javascript
res.clearCookie("key");
```
쿠키삭제

```javascript
app.get('/count', function (req, res) {

    if (req.signedCookies.count) {
        var count = parseInt(req.signedCookies.count);
    } else {
        var count = 0;
    }

    res.cookie('count', count+1, {signed:true});
    res.send('count:' + req.cookies.count);
});


```

signedCookie를 활용한 쿠키 암호화
