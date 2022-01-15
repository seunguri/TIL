# 웹 개발 기초
1. 정적컨텐츠
    
    /hello-static.html
    
    1. hello-static 관련 컨트롤러
    2. resources.static/hello-static.html
2. MVC, 템플릿 엔진
    
    > 관심사를 분리. 역할과 책임
    > 
    
    View: 화면을 그림
    
    Controller:
    
    Model:
    
    viewResolver: 화면을 찾아주고 템플릿엔진 연결
    
3. API
    
    `json` 반환
    
    ```java
    @GetMapping("hello-api")
    @ResponseBody
    public String helloString(@RequestParam("name") String name) {
    	Hello hello = new Hello();
    	hello.setName(name);
    	return hello;
    }
    
    static class Hello {
    	private String name;
    	
    	public String getName() {
    		return name;
    	}
    
    	public String setName() {
    		this.name = name;
    	}
    }
    ```
    
    HttpMessageConverter
    
    - JsonConverter: 객체를 json 파일로 변환
    - StringConverter
    
    이클립스 자동완성 단축키: command+shift+enter

# 백엔드 개발
이게 뭐지..? 하는 생각이 들 때쯤 거의 효자손으로 박박 긁어주시는 강의였음.

1. test db는 언제 갈아주는거지? → ^^ @AfterEach를 쓰세요.
2. testcase에서 Repository를 정의하지 않았는데 어디에 있는 객체를 갈아주는 거지? → DI 쓰세요.

## 웹 애플리케이션 계층 구조

- 컨트롤러
- 서비스: 핵심 비즈니스 로직
- 리포지토리: 데이터베이스에 접근, 도메인 객체를 DB에 저장하고 관리
- 도메인: 비즈니스 도메인 객체(주로 데이터베이스에 저장하고 관리됨)

1. domain
2. repository
3. test repository
    
    @Test
    
    @afterEach
    
    django에서는 자동으로 비워서 할 수 있었음.
    
    **TDD 테스트 주도 계발**: 테스트 코드 먼저 하고 코드 작성
    
4. service: 비즈니스 로직, 롤 과 관련된 네이밍
5. test service
    - ^ + shift + t : create new test
    - 테스트 코드는 직관적으로 적으세요.(한국어도 ㄱㅊ)
    - 주석 추천
    
    ```java
    @Test
    void join() {
    	//given
    	//when
    	//then
    }
    ```
    
    - DI
    
    ```java
    public class MemoryRepository implements MemberRepository {
    	private static Map<Long, Member> store = new HashMap<>();
    	private static long sequence = 0L;
    	
    	...
    }
    ```
    
    static이어서 인스턴스와 상관없이 클래스에 붙어 상관없지만 testcase에서 new로 다른 레포지토리 객체를 생성하면 좋지 않다. 서로 다른 인스턴스다.
    
    static아니면 다른 DB(리포지터리)이므로 바로 문제가 생김.
    
    **DI**
    
    ```java
    // src.service.MemberService
    public class MemberService {
    
    	private final MemberRepository memberRepository;
    
    	public MemberService(MemberRepository memberRepository) {
    		this.memberRepository = memberRepository;
    	}
    	...
    }
    
    // test.service.MemberServiceTest
    class MemberServiceTest {
    
    	MemberService memberService;
    	MemberRepository memberRepository;
    	
    	@BeforeEach
    	public void beforeEach() {
    		memberRepository = new MemberRepository();
    		memeberService = new MemberService(memberRepository);
    	}
    	...
    }
    ```
    
    @BeforeEach
    

Optional<>: 한 번 감싸서 표현

optional의 여러 메서드들을 사용할 수 있음

```java
Optional<> result = ...;
result.ifPresent( ... );
// 이전에는 if null ~~
```

variable rename: shift + F6

자동 리턴: command + option + v

cntl + t(리팩토링 관련) → extract method

# 스프링빈과 의존 관계
Controller를 통해서 외부 요청을 받고 Service를 통해서 비즈니스 로직을 처리하고 Repository에서 데이터를 저3 장함.

## dependency injection: 의존 관계를 주입하자

`@Autowired`

> Controller → Service → Repository
> 
1. 생성자 주입
2. 필드 주입 ❌: 변경 불가
3. setter 주입 ❌: 조립 이후엔 변경할 일 없는데 계속 변경 가능

## 스프링 빈 등록

1. 컴포넌트 스캔과 자동 의존관계 설정 `@Component` , `@Autowired`
2. 자바 코드로 직접 스프링 빈 등록하기 `@Configuration` `@Bean`

싱글톤으로 등록해서 같은 스프링 빈이면 모두 같은 인스턴스임.

상황에 따라 구현 클래스를 변경해야하면 성정을 통해 스프링빈으로 등록한다.

```java
@Configuration
public class SpringConfig {
	@Bean
	public MemberRepository memberRepository() {
		//return new MemoryMemberRepository();
		return new DBMemberRepository();
	}
}
```

# 웹 MVC 개발
스스로 코드 작성해보자

1. /
2. /members/new
3. /members/createForm
4. /members
5. /`members/memberList

메모리에 있기 때문에 서버를 재시작하면 데이터가 다 사라진다.

최근 파일 : ^ + E

# DB 접근 기술
1. H2: sqlite 썼을 때가 생각나
2. 순수 Jdbc
3. 스프링 JdbcTemplate
4. JPA
5. 스프링 데이터 JPA

# H2
로컬서버에서 사용함.

### 연결

파일로 접근해서 연결하면 충돌날 수 있음

→ 소켓으로 jdbc:h2:tcp://localhost/~/test

```java
2022-01-09 오전 06:08 20,480 test.mv.db
```

🐸오 신기행

### sql 파일도 관리하자.

/sql/ddl.sql

# 순수 Jdbc

🐸편하게 들으라고 하셔서 편하-게 들음. 2학년 때, Jdbc로  버스터미널 DB짜던 수업이 새록새록 떠올랐음.

- DataSourceUtils를 통해서 getConnection, Close → 트랜잭션 등으로 연결 바뀔 때 동일하게 유지하기 위함
- **객체 지향이 왜좋냐 `다형성`**
    
    기존 코드는 손대지 않고, 설정만으로 구현 클래스를 변경할 수 있음.
    
    OCP, Open-Closed Principle: 확장에는 열려있고, 수정에는 닫혀있다.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/452cb059-4517-4f57-900a-270bd27694d3/Untitled.png)