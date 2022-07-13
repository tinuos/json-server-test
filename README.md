# JSON 서버를 이용한 REST 실습

> 바닐라 자바스크립트 - 고승원 (비제이퍼블릭) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## JSON 서버

> 책에 나온 설치 및 실행 과정은 [npmjs](https://www.npmjs.com/package/json-server)에 그대로 나온 내용으로 해당 사이트를 참고해도 된다.

### 설치

- JSON으로 fake REST API 서버를 구축하는 npm 모듈(라이브러리)
- npm 을 이용하여 설치
  - 전역(g)으로 설치하여 추후 json-server 명령어를 그대로 실행

```shell
npm install -g json-server
```

### fake DB 생성

- DB로 사용할(json 파일들이 저장될) 디렉터리 하나 생성 후  json 파일을 만든다.
- 파일의 기본 내용은 책 내용 그대로 진행

```json
// json-server-test/json-server/db.json
{
  "posts": [{ "id": 1, "title": "json-server", "author": "typicode"}],
  "comments": [{ "id": 1, "body": "some comment", "postId": 1 }],
  "profile": { "name": "typicode"}
}
```

### 서버 실행

- 전역으로 설치했기 때문에 json server 명령어를 그대로 넣어 실행한다.
- 앞 서 생성한 디렉터리(DB)로 이동하여 실행

```shell
json-server --watch db.json
```

![image](https://user-images.githubusercontent.com/104971437/178637910-bc3b9404-2b47-4d5e-a489-fddc8b7fa3e5.png)

- 명령어를 실행하면 위와 같이 fake json 서버가 동작하게 되며 설정된 자원들을 확인할 수 있다.
- json 파일 생성 시 첫번째로 작성한 키들이(posts, comments, profile) 각각의 자원에 대응된다.
- 실제 위 Home 주소로 들어가면 JSON Server 기본 홈 화면을 아래와 같이 확인할 수 있다.

![image](https://user-images.githubusercontent.com/104971437/178639041-03e897a3-0470-41ca-8a89-05092eb557df.png)

---

## CRUD 테스트

- 책에서는 fetch() 를 이용하여 실습

### GET 요청

- 데이터 조회 (`./crud-test/json-get.html`)
- 책에서는 fetch 를 이용하여 간단히 조회 요청을 테스트
  - [Json server](https://www.npmjs.com/package/json-server#routes) 에 제시하는 루트 작성 법에 따라 조회를 요청해야 한다.
  - 순서대로 전체 데이터, 특정 id 데이터, postId를 특정한 쿼리 데이터로 요청하는 예시이다.
- 요청이 될 때마다 json server 콘솔에서 로그 확인 가능하다.
  - 여기서는 200 상태이지만 계속 요청해보면 304로 바뀐다. (캐시 관련 내용, HTTP 내용)

```shell
GET /comments 200 2.668 ms - 68
GET /comments/1 200 5.148 ms - 54
GET /comments?postId=1 200 7.401 ms - 68
```

### POST 요청

- 데이터 등록 (`./crud-test/json-post.html`)

### PUT 요청

- 데이터 수정 (`./crud-test/json-put.html`)
- POST 방법과 다른 점이 보이는 데 POST에서는 데이터를 등록할 때 id 값을 따로 정하지 않아도 Json Server에서 자동으로 부여해준다.

### DELETE 요청

- 데이터 삭제 (`./crud-test/json-delete.html`)

> GET을 제외한 다른 메서드 요청은 fetch의 두번째 인자로 method를 명시하여 전달한다. 요청하고자 하는 처리에 따라 URI 및 HTTP 정보를 다르게 작성. 이러한 작성법은 해당 API 공식문서를 참고하는 수 밖에 없다. (실무라면 백엔드 개발자와의 소통이 될 것 같다)

---

## 정리

- 간단한 실습을 통해 API의 중요성을 경험할 수 있었다.
- 꼭 REST API가 아니더라도 API 서버가 제시하는 방법을 통해 요청을 보내고 응답 내용을 확인할 수 있어야 한다고 생각. 웹이라면 HTTP를 심도있게 학습해야 제대로 다룰 수 있을 것 같다. (추가적으로 네트워크 개념도)
- 그리고 여기선 나오진 않았지만 API key 및 보안과 관련된 내용도 있다. 요청을 보낼 때 HTTP 헤더 등에 관련 내용을 명시하여 처리하는 것으로 보이는데... 이 또한 추가 학습 필요.😭