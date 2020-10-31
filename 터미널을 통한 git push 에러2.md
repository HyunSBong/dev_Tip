# 저장소에 파일을 git push로 올리려는데..2

인텔리제이와 연결되어있는 저장소에 터미널로 git push 를 해보니 아래와 같은 에러가 난다.

>error: src refspec master does not match any.
>
>error: failed to push some refs to'https://github.com/HyunSBong/TIL.git'

## 원인

저장소에 커밋한 내용이 없어서 서버에 추가할 branch가 존재하지 않아 발생한 오류이다.

-> 저장소가 비어있다는 것이다.

그런데 이미 인텔리제이와 연동되어 파일이 존재하는 저장소이다. 그래서 branch를 살펴보니  얼마 전에 기본 branch가 master에서 main 으로 변경되었다. ('Black Lives Matter' 운동에 따라 master와 slave의 관계가 연상되는 단어를 바꾼거란다....) 

##   해결

터미널에서 (윈도우에서는 git bash에서) branch 설정을 main으로 바꿔주면 된다.

1. 커밋 다음 단계에서 git branch -M main 을 입력해주면된다. 물론 push에서도 git push -u origin main 처럼 master를 main으로 변경해주면 된다.

push가 정상적으로 진행되었다!

![Imgur](https://user-images.githubusercontent.com/69189272/97778037-bdab0900-1bb7-11eb-8997-e0cff658d28f.png)

## 정리

>- 바꿀 거면 알려주던가...


