# postman 설정 팁

# 환경변수 설정


상단 오른쪽 톱니바퀴 버튼을 누르고 manage Enviroment를 들어간 후

![BC2D72B0-A4E2-4430-B528-868E68831174](http://i.imgur.com/zFocULg.png)

환경변수 명을 입력한 후 각각 대응하는 값을 입력하여준다.

![29022AAA-8757-42AA-A02D-84567A90A532](http://i.imgur.com/7dGohZi.png)


그 후 쿼리를 보낼 때 {{apiUrl}} 와 같은 형식으로 이용할 수 있다.

# 환경변수 자동화

test탭을 통하여 코드를 입력할 수 있다.
예를들어 test에

```
var token = postman.getResponseHeader('x-auth');
postman.setEnviromentVariable('x-auth', token);
```

![ED48A24A-9A73-4FDC-ACD8-7F536C5FF612](http://i.imgur.com/332NYr8.png)
을 통하여 들어오는 x-auth변수를 변수로 설정할 수 있다.
추후에 {{x-auth}}  형태로 사용 가능하다.
