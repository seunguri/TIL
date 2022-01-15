# DB 접근기술 이어서~
## 스프링 통합 테스트

@SpringBoot: 스프링 컨테이너와 테스트를 함께 실행   
@Transactinal: 테스트 전에 트랜잭션, 후에 롤백

> 롤백?
> 

@Commit: DB에 커밋해줌

## 그러면 통합테스트만 하면 되는거 아닌가요?

단위테스트: 자바코드로 순수하게 → 훨씬 좋을 확률이 높다.  
통합테스트: 스프링 컨테이너와 함께  

# 스프링 JdbcTemplate

TemplateMethodPattern: 디자인 패턴

```
public JdbcTemplateMemberRepository(DataSource dataSource) {
	jdbcTemplate = new JdbcTemplate(dataSource);
}
```

작업의 60~70%는 testcode를 짠다.  
작은 오류하나가 수십억원의 피해로 돌아온다.  

# JPA
자바 퍼시스턴스 API  
ORM  

jpa 표준  
hibernate 구현체 중 하나  

데이터를 저장하거나 변경할 때 @Transactional  

### 트래픽이 크고 금액이 큰 실무에서 JPA를 쓸 수 있을까?
ㅇㅇ 정말 많이 씀.

# 스프링 데이터 JPA
🐸테스트 코드 작성을 앞두고 있는 시점에서 눈이 확 뜨였다. 장고를 사용해본 입장에서 스프링 데이터 JPA를 알기전에 JPA를 잘알아야한다는 말이 납득이 되었다. 모르는 개발자가 모르고 쓰는것보다 아는 개발자가 편하게 쓰라고 있는것

```
@Configuration
public class SpringConfig {
	private final MemberRepository memberRepository;
	
	@Autowired
	public SpringConfig(MemberRepository memberRepository) {
		this.memberRepository = memberRepository;
	}

	@Bean
	public MemberService memberService() {
		return new MemberService(memberRepository);
	}
}
// interface에 대한 구현체를 알아서 찾음
```

```
// 인터페이스 이름만으로 개발이 끝남
```

+Querydsl: 복잡한 동적 쿼리  
+JdbcTemplate  
+JPA

다 섞어서 씀

# 기타
- Google Trends 좋다

### 단축키
- ^+ t → inline valiable: 같은 변수 합쳐줌

# AOP
좌절포인트(c언어 포인터같은 존재)  
언제 왜 쓰는지 알면 전혀 어렵지 않음!

상황:  
모든 api 호출 시간 뽑아와봐  
api에 start,finish 다 달아야하는 상황

공통 관심 사항과 핵심 관심 사항을 분리한다.

```
@Aspect
public class TimeTraceAop {
	
}
```

프록시가 주입되서 작동(코드 복제)

🐸 푸쉬알림 기능을 구현할 때 비슷한 고민을 했었다. action이 이루어지는 메서드에 푸시알림 전송 로직을 넣는게 정말 깔끔하지 않았다. Signal 사용을 고민했었다. 이 경험으로 AOP 개념이 조금 더 이해가 잘됐다.

