# webstorm에서 scss 에서 설정하기

1. scss를 설치하여준다.

2. 설치 후 cmd + , 키를 통하여 Preference 창을 켜준 후 file watchers 메뉴로간다

3. 아래를 참조한다.

```
FILE type: scss
Prgoram: /usr/local/bin/scss // scss위치를 지정하여준다.


```

4.Output Dir를 설정할 수 있다.

```
$ProjectFileDir$/public/admin/css/$FileNameWithoutExtension$.css

```
\$\ProjectFileDir\$\ = 프로젝트 디렉토리
