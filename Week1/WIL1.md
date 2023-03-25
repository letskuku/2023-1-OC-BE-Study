# 필수 정리 내용

## 1. MVC 패턴이란?

MVC 패턴이란, 애플리케이션을 Model, View, Controller 세 가지 구성요소로 나눈 소프트웨어 디자인 패턴이다.

- Model : 화면에 보여줄 정보를 담아 넘겨준다
- View : 화면을 그리는 데에 모든 역량 집중, 모델로부터 정보를 받는다.
- Controller : 비즈니스 로직이나 서버 등에 관련된 일 처리

## 2. API와 서버? 

- API(Application Programming Interface) : 응용 프로그램에서 사용할 수 있도록 운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스 
(ex. API를 통해 기상청 소프트웨어 시스템에서 일일 기상 데이터를 가져와 날씨 정보 표시)

요청을 보내는 애플리케이션을 클라이언트, 응답을 보내는 애플리케이션을 서버라고 보기도 한다.

### 다양한 종류의 API

- 웹 API : 웹 서버와 웹 브라우저 간의 애플리케이션을 처리하는 인터페이스

웹 API에서는 XML, JSON 등의 방식으로 데이터를 만들어 HTTP 응답 메시지로 반환하여 HTTP의 BODY 부분에 데이터 내용을 직접 반환한다.

- REST API : REST 아키텍처의 제약 조건을 준수하는 특수한 유형의 웹 API



## 3. RESTful이란?

### REST란?

- REST(Representational State Transfer) : 자원의 표현(representation)을 통해 해당 자원의 상태(정보)를 주고 받는 것

REST는 네트워크 상에서 서버와 클라이언트가 통신하는 방식 중 하나이다.
HTTP URI(Uniform Resource Identifier)를 통해 자원을 명시하고, HTTP Method(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CRUD Operation을 적용한다.

- URI : 특정 자원을 식별하는 통합 자원 식별자(Uniform Resource Identifier)

웹 사이트의 이미지, 텍스트, DB 내용 등이 자원에 해당하며, 모든 자원에 고유한 ID인 HTTP URI를 부여한다. 
URL은 컴퓨터 네트워크 상에서 자원이 어디 있는지 알려주므로 URI의 일종이다.

- CRUD : Create(생성), Read(조회), Update(수정), Delete(삭제)

### REST의 구성요소 

REST는 자원(Resource), 행위(Verb), 표현(Representation)으로 구성된다.

- 자원 : 서버에 존재하는 모든 자원은 고유한 ID인 HTTP URI를 가지고 있으며, 클라이언트는 URI로 자원을 지정하여 해당 자원의 상태(정보)에 대한 operation을 서버에 요청한다.
- 행위 : HTTP 프로토콜의 Method(POST, GET, PUT, DELETE)를 통해 자원의 상태(정보)에 대한 operation을 요청한다.
- 표현 : 클라이언트가 요청한 operation에 대해 서버가 XML, JSON 등 여러 형태의 응답을 할 수 있다.

### RESTful이란?

RESTful이란 REST의 원리를 따르는 시스템을 의미한다. REST API를 제공하는 웹 서비스를 RESTful하다고 말할 수 있다.

REST의 원리를 따른다고 해서 무조건 RESTful한 것이 아니라, 다음과 같은 조건을 만족해야 한다.

- CRUD Operation을 모두 사용해야 한다. (ex. POST로만 구성되는 웹 서비스는 RESTful하지 않음)
- URI에 대한 규칙을 지켜야 한다. (자원과 id 외의 정보가 포함되서는 안됨)

즉, RESTful은 REST를 REST답게 쓰기 위한 방법으로, 개발자들이 비공식적으로 제시한 것이다.

# 강의 정리 내용

## Section 1

- Maven? Gradle? : 필요한 라이브러리를 가져오고, 빌드하는 라이프 사이클까지 관리해주는 툴

Maven이나 Gradle 같은 빌드 툴들은 의존관계를 관리해준다. 다시말해, 의존관계가 있는 라이브러리를 함께 가져온다. 
예를 들어, 사용자가 spring-boot-starter-web을 가져오면 이 라이브러리가 필요로 하는(의존관계에 있는) 라이브러리를 모두 가져온다.

IntelliJ에서 프로젝트를 열었을 때 External Libraries에서 가져온 라이브러리를 확인할 수 있다.

- Welcome Page : 도메인만 적고 들어왔을 때의 첫 화면이다. 스프링 부트는 main의 resources에 static/index.html을 올려두면 Welcome Page로 기능한다.

- Thymeleaf : html 만들어주는 템플릿 엔진

### thymeleaf 템플릿 엔진

resources/static/index.html은 정적 페이지이다. 즉, 적어놓은 파일을 웹 서버가 그대로 웹 브라우저에 넘겨준다. 템플릿 엔진은 정적 페이지의 모양을 바꿀 수 있게 해준다.

먼저, main의 java에 controller라는 package를 만들고 그 안에 HelloController 클래스를 만든다. 
이때, 애노테이션에 언급된 Controller는 웹 어플리케이션의 첫번째 진입점이라고 볼 수 있다.

```
package hello.hellospring.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class HelloController {

    @GetMapping("hello")
    public String hello(Model model) {
        model.addAttribute("data", "hello!!!");
        return "hello";
    }
}
```

resource/templates/hello.html 파일의 코드는 다음과 같다.

```
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Hello</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
</head>
<body>
<p th:text="'안녕하세요. ' + ${data}" >안녕하세요. 손님</p>
</body>
</html>
```

이때, ${data}는 model.addAttribute의 value인 hello!!!로 치환되어 화면에는 '안녕하세요. hello!!!' 라는 글자가 나타나게 된다.

### 동작 과정

스프링 부트는 톰캣이라는 웹 서버를 내장하고 있다. 먼저, 웹 브라우저에서 localhost:8080/hello를 내장 톰캣 서버로 던지면 톰캣이 /hello를 spring에 물어본다.

HelloController 클래스의 @GetMapping("hello")에서 Get은 http의 Get 메소드, Post 메소드를 이야기할 때의 Get이다. (http URL을 임의로 적어 엔터를 누르는 것을 Get 방식이라고 함)
@GetMapping("hello")이 hello URL과 매칭되어 HelloController 클래스의 hello 메소드가 실행된다.

hello 메소드는 hello를 반환한다. Controller에서 리턴 값으로 문자를 반환하면 viewResolver가 화면을 찾아 처리한다. 스프링 부트 템플릿 엔진의 기본 viewName 매핑은 resources:templates/ + {viewName} + .html이다.
즉, data라는 model을 넘기면서 스프링 부트가 resources의 templates에서 hello.html을 찾아 thymeleaf 템플릿 엔진 처리(data에서 값 꺼내 바꿈) 후 웹 브라우저로 넘긴다.

## Section 2

웹을 개발하는 방법에는 크게 3가지가 있는데, 각각을 정적 컨텐츠, MVC와 템플릿 엔진, API라고 한다.

### 정적 컨텐츠

정적 컨텐츠는 이전 시간에 만들어본 Welcome Page처럼 서버에서 무언가를 하는 것 없이 그냥 파일을 그대로 웹 브라우저로 내려주는 형태를 갖는다.

스프링 부트는 정적 컨텐츠 기능을 자동으로 제공하는데, 공식 문서를 보면 디폴트로는 static 폴더에서 파일을 찾아 제공하는 것을 알 수 있다.

정적 컨텐츠는 원하는 파일(정적 파일)을 넣으면 그대로 반환된다. 대신 어떤 프로그래밍을 할 수는 없다.

내장 톰캣 서버가 hello-static.html 요청을 받아 스프링으로 넘기면, 스프링은 먼저 컨트롤러쪽에서 hello-static이 있는지 찾아본다. 다시말해, 컨트롤러가 우선순위를 가진다는 의미이다.
스프링 부트가 컨트롤러쪽에서 hello-static을 찾지 못하면 내부의 resources에서 static/hello-static.html을 찾고, 있으면 그대로 웹 브라우저로 반환한다.

### MVC와 템플릿 엔진

웹 개발에서 가장 많이 사용하는 방식으로, jsp, php 같은 것들이 소위 말하는 템플릿 엔진이다. 템플릿 엔진은 html을 그냥 주는 것이 아니라 뭔가 서버에서 프로그래밍을 해서 html을 동적으로 바꾸어 반환한다. 이걸 하기 위해 필요한 model, 템플릿 엔진 화면(view), controller를 MVC라고 한다.

과거에는 controller와 view가 따로 분리되어있지 않고 jsp를 가지고 view에서 모든 것을 다 했는데, 이것을 모델 1 방식이라고 한다. 그러나 지금은 MVC 방식을 많이 사용한다. 왜일까?

view는 화면을 그리는 데에 모든 역량을 집중해야한다. controller나 model과 관련된 부분들은 비즈니스 로직과 관련있거나 내부적인 것을 처리하는 데에 집중해야한다. 그렇기 때문에 model, controller, view로 나눈 것이다.
view는 화면과 관련된 일만 하고, 비즈니스 로직이나 서버 등에 관련된 일은 controller나 비슷한 비즈니스 로직에서 다 처리하고 model에 화면에서 필요한 것들을 담아 화면쪽에 넘겨주는 패턴이라고 할 수 있다.

웹브라우저에서 localhost:8080/hello-mvc를 넘기면 내장 톰캣 서버가 hello-mvc를 스프링에 넘긴다. 스프링은 helloController의 helloMvc 메소드와 hello-mvc가 매핑된 것을 확인한 후, helloMvc 메소드를 호출한다.
메소드가 모델과 함께 hello-template을 스프링에 넘겨주면 viewResolver가 동작한다. viewResolver는 화면 관련 해결자로, view를 찾아주고 템플릿 엔진을 연결시켜준다.
viewResolver가 templates/hello-mvc.html을 찾아서 thymeleaf 템플릿 엔진에 처리해달라고 넘기면, 템플릿 엔진이 렌더링해서 변환한 html을 웹브라우저에 넘긴다.

### API

템플릿 엔진은 view라는 템플릿이 있고, 거기에서 어떠한 조작을 가한다. 지금 같은 경우에는 템플릿 엔진과는 달리 데이터를 그대로 넘겨준다.

API에서는 @ResponseBody를 사용한다. http는 크게 헤더와 바디로 나뉘어져있는데, @ResponseBody를 사용하면 viewResolver를 사용하지 않고 http의 바디 부분에 데이터를 직접 넣어준다.

과거에는 xml 같은 포맷이 많이 사용되었다. 그러나, 요즘에는 json이라는 데이터 구조 포맷으로 클라이언트에게 데이터를 전달한다. JSON은 key-value로 이루어진 구조이다. 과거에는 xml 방식도 많이 사용되었는데, html 태그가 xml 방식으로 작성하는 것 중 하나이다. 
xml 방식의 경우, 여는 태그와 닫는 태그가 필요해 작성을 두 번 해야하지만, JSON은 name:value의 단순한 구조를 갖는다.

내장 톰캣 서버가 웹브라우저로부터 localhost:8080/hello-api를 받아 hello-api를 스프링으로 던진다. @ResponseBody가 사용되었으므로 스프링은 http에 데이터를 그대로 넘기도록 동작한다. 문자는 문자 값을 바로 http 응답에 넣고 넘겼지만, 반환하는 것이 객체인 경우 객체는 기본 설정인 JSON 방식으로 데이터를 만들어 http 응답에 반환한다.
또한, viewResolver 대신 HttpMessageConverter가 동작한다. 반환이 단순 문자인 경우 StringConverter가 동작하고, 객체인 경우에는 객체를 JSON 스타일로 바꿔주는 JsonConverter가 동작한다.
JsonConverter가 동작하게 되면 JSON 스타일로 바꾼 데이터를 웹브라우저로 넘겨준다.
