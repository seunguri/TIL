김영한님의 '스프링 입문 - 코드로 배우는 스프링부트, 웹, MVC, DB 접근기술 강의'를 듣고 작성
# https://start.spring.io

---

spring initializer

spring boot 기반 프로젝트를 만들어주는 사이트  
Project: 라이브러리를 땡기고 빌드하는 라이프사이클을 관리해주는 툴  
Dependencies: 어떤 라이브러리 사용할건지  

**익숙해**

```python
django-admin startproject
```

명령어 후에 후두두둑 생기는 걸 봤던 첫 날이 떠오른다  
하나도 모르겠는 파일들의 쓰임새를 알기까지 많이 걸렸는데 Spring은 어떨까

## 구조

- .idea 인텔리제이 설정파일
- gradle gradle 관련 폴더
- src
    - main
        - java
            
            실제 패키지, 소스파일
            
        - reso
            
            urces
            
            자바 파일을 제외한 나머지(xml, html 등)
            
    - test ❗
        
        테스트코드와 관련된 소스
        
- build.gradle
    
    설정파일이 다 제공된다.
    
    mavenCentral(): dependecies 라이브러리를 다운받을 때 ‘mavenCentral’이란 공개된 사이트로 설정되어있음.
    

## 실행

```python
Tomcat started on port(s): 8080 (http) with context path '’
```

[localhost](http://localhost):8080 확인  
![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ca57fc34-97c9-4a99-9f73-f96704b5826a/Untitled.png)

Tip. gradle을 intellij로 실행하면 더 빠름.

**익숙해**  
장고 로켓을 본 느낌이야

# Library

---

## WAS

`spring-coot-tomcat`

### WAS, Web Server

Python 에서는 Nginx와 Gunicorn으로 구현했었음.  
Web Server: 정적인 컨텐츠 제공하는 프로그램(소프트웨어 관점에서)  
WAS: 동적인 컨텐츠 제공하는 Application Server

> [Java, Spring 관점으로 잘 설명되어있는 블로그](https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html)
> 

## Logging

`spring-boot-starter-logging`  
logback: 로그를 어떤 구현체로 출력할 지, slf4j:인터페이스

## Test

`junit` : 테스트 프레임워크  
`mockito` : 목 라이브러리  
`assertj` : 테스트 코드를 좀 더 편하게 작성하도록 도움.  
`sprint-test` : spring 통합 test 지원

# View

---

정적 파일

resources/static/index.html → welcome page

> spring은 출시 이후 어마어마한 기능이 추가됌. 머릿속에 다 넣을 수 없고 필요할 때 잘 찾는 것이 중요.  
> spring boot는 spring 생태계를 감싸서 편리하게 사용할 수 있도록 도와줌.
> 
> ## spring.io
> spring boot → **reference documentation**  
> 익숙해.. 장고 docs 뒤지던 날들,,  
> 

## Template Engine

1. create controller pakage
    
    **익숙해**
    MTV, MVC  
    장고 시작할 때, 같은 애들인데 이름이 다르다며 알고만있어라했던 그 패턴
    
2. create template  
**장고로 하면 어떤 코드일까?**

```java
//controller
@Controller
public class HelloController {

    @GetMapping("hello")
    public String hello(Model model) {
        model.addAttribute("data", "hello!!");
        return "hello";
    }
}

//templates
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Hello</title>
</head>
<body>
<p th:text="'안녕하세요. ' + ${data}">안녕하세요. 손님</p>
</body>
</html>
```

```python
#urls.py
urlpatterns = [
	path('hello/', views.hello, name='hello'),
]

# views.py
def hello(request):
		context = {'data': 'hello!'}
    return render(request, 'hello.html', context)

# templates/hello.html
<p>'안녕하세요. ' + {{data}}</p>
```

Spring에서 model이 MVC의 모델이라고 했음.  
그럼 Django Model을 정의하는 것과 같은 개념인지 의문임!  
th가 어떤 식으로 작동하는지도 궁금함.

### build

```java
gradlew.bat build
java -jar hello-spring-0.0.1-SNAPSHOT.jar
```

# 마치며

지금 써놓은 코드가 아마 완전히 틀렸을거같은데 강의가 진행되면서 수정하러 오겠음. 자바언어에 대한 공부도 필요함을 느낌.

오늘 ‘익숙해’ 라는 키워드를 참 많이 썼음.

친구들이 스프링으로 넘어갈 때 장고를 계속하면서, 잘 짜여진 프레임워크를 제대로 공부해보고 스프링으로 넘어가면 구조를 이해하는데 도움이되고 더해서 다양한 방식을 알게 되니 배로 공부가 될거라고 생각해왔음.

정말 전체적인 구조? 형식?은 유사한 것 같음. 하지만 이번 강의는 아주 기초적인 내용이었고 세부적으로 들어갈수록 다른것도 많을 것 같아 더 열심히 해야겠음..