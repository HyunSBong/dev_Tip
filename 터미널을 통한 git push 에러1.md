# 저장소에 파일을 git push로 올리려는데..

인텔리제이와 연결되어있는 저장소에 터미널로 git push 를 해보니 아래와 같은 에러가 난다.

>! [rejected]    main -> main (fetch first) 
>
>error: failed to push some refs to'https://github.com/HyunSBong/TIL.git'

## 원인

원격 저장소와 현재의 로컬 저장소가 동기화되어 있지 않기 때문에 나타난 원인이다.

![Imgur](https://user-images.githubusercontent.com/69189272/97777897-81c37400-1bb6-11eb-98cc-ec6ca5a9ca7e.png)

## 해결

해결 방법은 매우 간단하다. 저장소에 있는 정보를 가져온 후 같이 재업로드하는 방식이다.

1. git pull --rebase 원격저장소별칭 main 또는 master 

   ex) git pull --rebase origin main 또는 master

push가 정상적으로 진행되었다!

![Imgur](https://user-images.githubusercontent.com/69189272/97778037-bdab0900-1bb7-11eb-8997-e0cff658d28f.png)

## 정리

>- 별거 아니었다...
