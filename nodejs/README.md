
# 여행상품 쇼핑몰

## Introduce
여행 상품을 판매하는 쇼핑몰 사이트 입니다. 원하는 여행 상품을 보고 구매 버튼을 누르면 paypal 결제가 됩니다.

<br/>

## Software development environment

|항목|내용|비고|
|:---:|:---:|:---:|
|React|||
|Redux |4.0.0| |
|express|4.17.1||
|multer|1.4.2||
|react-dropzone|10.2.2||
|MongoDB|6.0.1||
|react-gallery-carousel|1.0.7||
|react-paypal-express-checkout|1.0.5||


### * [paypal 추가하기](https://developer.paypal.com/developer/accounts)

</br>


## How to Run?

> AWS EC2 
1. select os that ubuntu 18.04 or ubuntu 20.04

2. connect instance via ssh.

3. install node, nvm. 
```
 sudo apt intall node
 # bash 사용자
 curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
 # Zsh 사용자
 curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | zsh
``` 
4. install npm
```
 npm install
 cd client
 npm install
``` 
5. start
```
 npm run dev
``` 
> Docker...!

1. install docker if you don't have docker in your pc.

2. install docker-compose

3. Run docker-compose
```
 docker-compose -f node.yml up
``` 

<br/>
<br/>
<br/>
<br/>


## <이슈사항>

### 1. ECONNREFUSED 에러

![https://user-images.githubusercontent.com/54494793/163204446-47be6994-1ab6-4421-b27e-eb0ae45ed58a.png](https://user-images.githubusercontent.com/54494793/163204446-47be6994-1ab6-4421-b27e-eb0ae45ed58a.png)

- 로그인 화면에서 이메일과 패스워드를 입력한 후 로그인을 시도하면 다음과 같은 오류가 발생.

![https://user-images.githubusercontent.com/54494793/163204650-83c2d6c8-f98f-46f9-8c68-b6748c9e8392.png](https://user-images.githubusercontent.com/54494793/163204650-83c2d6c8-f98f-46f9-8c68-b6748c9e8392.png)

-  이유는 server를 담당하는 express에서 package.json 파일안에 bcrypt 버전이 사용하는 nodejs 버전과 맞지 않았음.

-  dependencies 에서 버전을 수정하고 다시 npm install 후 오류를 해결.

<br/>

![https://user-images.githubusercontent.com/54494793/164894935-2cc0adb5-6840-4989-9a7f-c89075bd90e3.png](https://user-images.githubusercontent.com/54494793/164894935-2cc0adb5-6840-4989-9a7f-c89075bd90e3.png)

- DB에 있는 모든 정보를 가져오려고 하는데 위와 같은 에러가 발생.

### 2. npm ERR! code ELIFECYCLE 에러

![https://user-images.githubusercontent.com/54494793/165223901-ac2ebb02-3d56-4f1a-afad-f618812c0e9f.png](https://user-images.githubusercontent.com/54494793/165223901-ac2ebb02-3d56-4f1a-afad-f618812c0e9f.png)

- linux 서버에 파일을 올려서 node를 실행하면 npm ERR! code ELIFECYCLE 에러가 발생

```
- $ npm cache clean --force
- $ rm -rf node_modules package-lock.json
- $ npm install

```

- 해결 : npm 캐시파일을 모두 삭제하고 package-lock 의존성을 제거한 후 npm을 재설치

<br/>

### 3. Error: listen EADDRINUSE: address already in use :::5000 에러

- 5000번 포트를 사용하는 프로세스의 ID 확인
```
 $ netstat -ano 혹은 $ sudo lsof -i :5000
```
- 해당 프로세스 강제종료하기
```
 $ sudo kill -9 PID
```

<br/>

### 4. POST 400 (Bad Request) , in promise Error: Request failed with status code 400

- proxy 서버의 middleware 관련 문제
- setupProxy.js 파일의 내용을 변경해 해결


![https://user-images.githubusercontent.com/54494793/168082659-893079dd-b91a-4b9d-9dbb-65c4a9eb7cfb.png](https://user-images.githubusercontent.com/54494793/168082659-893079dd-b91a-4b9d-9dbb-65c4a9eb7cfb.png)

<br/>

### EC2 환경에서 퍼블릭 IPv4 주소:3000 으로 접속이 안된다?

### 인바운드 규칙으로 들어가서 다음과 같이 처리

![https://user-images.githubusercontent.com/54494793/162966738-bf69a374-2124-4011-bf97-14c9dd7febc2.png](https://user-images.githubusercontent.com/54494793/162966738-bf69a374-2124-4011-bf97-14c9dd7febc2.png)