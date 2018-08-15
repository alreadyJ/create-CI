# create-CI
CI with jenkins, docker, ngrok, git and spring framework 

<h2> CI 구축하기 (create CI) </h2>

<h4> 준비물 (Preparing) </h4>

- docker (VM의 한 종류인데 OS위에 다른 OS를 가상화하여 만드는 것이 아니라 OS위에 docker 엔진을 올리고 그 위에 container라는 가상화된 OS 설치하는 것.)
- jenkins (CI 툴.)
- ngrok (gnrok 홈 페이지에 Public URLs for testing on mobile devices.라고 적혀있다. 즉 로컬에 외부 접속을 편하게 해주는? )
- github (네!)
- your project
 
 우선 준비물로는 위의 5가지가 필요합니다. 저는 docker container를 이용해 CI를 구축할 예정입니다.
 
 그럼 차근 차근 순서대로 진행해 보도록 하겠습니다. 
 
<h3> docker 설치하기 </h3>
 
 https://docs.docker.com/docker-for-mac/
 
![image](https://user-images.githubusercontent.com/24931420/44129032-3a42adb0-a081-11e8-8ad5-1997e1697f3e.png)

링크를 클릭하고 들어가서 빨간 부분을 클릭합니다.

![image](https://user-images.githubusercontent.com/24931420/44129392-f903d3b8-a082-11e8-9423-b9325cf65428.png)

그리고 또 클릭합니다.

![image](https://user-images.githubusercontent.com/24931420/44129461-753a96a6-a083-11e8-97f8-f86f82edbfd2.png)

위 상황은 docker store에 로그인 했을 때의 상황입니다. 로그인은 github 아이디로도 할 수 있습니다~ 그리고 또 클릭합니다.

그럼 docker 설치가 완료될 것입니다. 

![image](https://user-images.githubusercontent.com/24931420/44129558-eb32cb58-a083-11e8-9cb8-ceed31ed74dc.png)

설치가 완료되면 다음과 같은 터미널에서 다음과 같이 명령어를 입력해 보면 실행이 잘 될 겁니다.

<h3> jenkins 설치하기 </h3>

jenkins는 어디서 설치할까요?

생각보다 가까운 곳에 답이 있었습니다.
<p align="center">
  
![image](https://user-images.githubusercontent.com/24931420/44129657-5dad9686-a084-11e8-9931-bd671d5c1bbe.png)

</p>

docker가 설치 되면서 위에 docker 아이콘이 생겼을 겁니다.
그걸 클릭하고 Kitemetic 이라는 곳을 클릭해주세요. 이것도 설치하라고 뜰겁니다. 

![image](https://user-images.githubusercontent.com/24931420/44129872-8387cab0-a085-11e8-9044-54d50cdf2677.png)

그리고 다시 실행을 하게 되면, 제가 기억하기로는 젠킨스가 제일 위에 있던걸로 기억해요 :) 젠킨스를 설치합니다.

그럼 오른쪽에 웹페이지 미리보기가 있을 겁니다. (벌써 다 되있습니다.) 오른쪽을 보시면 비밀번호에 관한 안내가 나와있는데 그대로 해봅시다.

![image](https://user-images.githubusercontent.com/24931420/44130004-6199c452-a086-11e8-8a17-959584f8e7c1.png)

(읭? 없는데요?)

![image](https://user-images.githubusercontent.com/24931420/44130036-93d3bef0-a086-11e8-98f7-d9da8efe007a.png)

일단 jenkins가 제대로 설치 됐는지 확인해봅니다. 잘 있네요? 

![image](https://user-images.githubusercontent.com/24931420/44130160-0f287032-a087-11e8-90e8-60f58cc96d97.png)

image를 컨테이너에 올립시다.

![image](https://user-images.githubusercontent.com/24931420/44130202-4e51745c-a087-11e8-881a-fb4a332d2186.png)

무사히 입장한 후, 이곳으로 이동 후 cat으로 긁어 보면?? 비밀번호가 나옵니다!!

![image](https://user-images.githubusercontent.com/24931420/44130258-89661c8c-a087-11e8-9644-a81a70a669c0.png)

이제 젠킨스에 로그인 합니다 !!! 설치는 이 것으로 마무리됩니다.


<h3> ngrok으로 젠킨스 외부 접속 허용시키기 </h3>

https://ngrok.com 으로 이동해서 ngrok을 다운 받을 수 있습니다.

![image](https://user-images.githubusercontent.com/24931420/44130406-4f7e34cc-a088-11e8-9e19-835954f8c566.png)

Downloads 폴더에 생겼습니다 :) 설치가 된 듯 합니다.

클릭하여 실행 후 ngrok 명령어를 실행해보지만 안됩니다 :(

![image](https://user-images.githubusercontent.com/24931420/44130479-cb1b59c0-a088-11e8-9e36-781c45c05212.png)

ngrok 파일을 이곳으로 옮깁니다 :) 이후 실행해보면 잘 될 겁니다.


잘은 모르지만 이런 방식으로 jenkins를 생성했을 때, jenkins의 포트는 32769 입니다. 아마도 default 포트인 것 같습니다.


![image](https://user-images.githubusercontent.com/24931420/44130543-0dc4d882-a089-11e8-9bc3-8b89b770b3b6.png)

자 이제 됐습니다.

![image](https://user-images.githubusercontent.com/24931420/44130619-5aab5112-a089-11e8-8fff-d0301e2a75a1.png)

생성된 주소로 접근해보면 잘 접근되는 것을 확인하실 수 있습니다 :)

<h3> 젠킨스에 모듈 설치하기 </h3>


![image](https://user-images.githubusercontent.com/24931420/44130916-bb3dd300-a08a-11e8-91e9-833a2500a3de.png)


그림과 같이 Jenkins 관리를 클릭하여 들어갑니다.

![image](https://user-images.githubusercontent.com/24931420/44130973-f7f00ad4-a08a-11e8-8efc-41f385c299a0.png)

그리고 플러그인 관리를 누릅니다.

![image](https://user-images.githubusercontent.com/24931420/44131014-32260104-a08b-11e8-91d8-8b1b9619a06a.png)

그리고 설치가능 탭을 누른 후 deploy 라고 검색을 합니다.

![image](https://user-images.githubusercontent.com/24931420/44130992-1314c4ee-a08b-11e8-8d38-1aa6a7bca548.png)

자 이것을 설치합시다 :)

저는 maven을 이용한 project를 빌드할 것이기 때문에 사용할 maven과 jdk등을 설치하도록 하겠습니다.

![image](https://user-images.githubusercontent.com/24931420/44131448-12650bc8-a08e-11e8-8761-6a21cc21c2de.png)

global tool configuration을 클릭하여 들어 갑니다.

![image](https://user-images.githubusercontent.com/24931420/44131574-ed471308-a08e-11e8-8f55-06a3ed8c7123.png)

jdk installation을 클릭한 후, 저는 jdk9를 사용할 것이기 때문에 위와 같이 선택했습니다:) 아 그리고 jdk 설치할 때, oracle 계정이 필요하다더군요...

![image](https://user-images.githubusercontent.com/24931420/44131636-671c824e-a08f-11e8-8270-ee03dfa65efc.png)

이제 아래로 내려가 git을 사용할 것이기 때문에 위와 같이 세팅을 해줍니다.

![image](https://user-images.githubusercontent.com/24931420/44131643-6f7400d4-a08f-11e8-97fb-1e943fbf9442.png)

더 아래로 내려가면 maven 설정하는 부분도 위와 같이 설정해주시면 될 것 같습니다 :)

<h3> 젠킨스에서 project 생성하기 </h3>

![image](https://user-images.githubusercontent.com/24931420/44131057-6d7ab59c-a08b-11e8-85bc-469648db75eb.png)

다시 home으로 돌아와서 새로운 아이템을 만듭시다 :)

![image](https://user-images.githubusercontent.com/24931420/44131217-70f19848-a08c-11e8-9ada-6208dd3acdca.png)

이름을 적고, 빨간 부분을 클릭하여 생성합시다.

![image](https://user-images.githubusercontent.com/24931420/44131310-1bcadec8-a08d-11e8-86e3-8cb5ccb9cd6f.png)

이름과 설명을 적습니다 :)

![image](https://user-images.githubusercontent.com/24931420/44131358-6ecbbcf0-a08d-11e8-8d9c-4d52280ce1f5.png)

연동시킬 github poject url을 적습니다. :) (clone할 때, 그 주소입니다) 그리고 add를 눌러 github username(not email)과 비밀번호를 입력합니다.

그리고 branch를 선택하면 끝입니다.

![image](https://user-images.githubusercontent.com/24931420/44131720-cbe45404-a08f-11e8-91ce-9de272b49b1b.png)

빌드가 언제 발생하는지와 빌드 환경은 위와 같이 선택했습니다.

![image](https://user-images.githubusercontent.com/24931420/44131759-04ea795e-a090-11e8-803b-7de3e605a416.png)
![image](https://user-images.githubusercontent.com/24931420/44131768-13bf0ff8-a090-11e8-9b90-235f4a635a01.png)

빌드에 관한 부분인데 maven 빌드를 할 때, clean install 명령어를 사용할 것이기 때문에 위와 같이 작성하였습니다.

![image](https://user-images.githubusercontent.com/24931420/44131936-1d64faee-a091-11e8-9344-9bce3f68e1e8.png)

마지막으로 빌드 후 조치 버튼을 클릭 후, deploy war/ear to a container를 선택합니다 :) 이 작업은 war를 톰캣에 배포하기 위해 필요한 작업입니다.

````
%TOMCAT8_PATH%/conf/tomcat-users.xml
````
그 전에 tomcat의 사용자에 대한 설정을 할 필요가 있습니다. 위의 위치로 이동합니다.

````

````

