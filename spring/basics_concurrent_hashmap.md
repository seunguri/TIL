 김영한님의 '스프링 핵심 원리 - 기본편 11강 회원 도메인 개발'을 듣고 작성 

 
 이번 강의에서 생성하는 클래스, 인터페이스의 파일 구조를 유심히 봤음.

 #  인터페이스와 구현체를 같은 위치에 두는 것은 좋지 않음.
 ├── MemoryMemberRepository
 └── MemberRepository
 🐸그럼 어떻게 두어야 좋은 건가요?

# 동시성 이슈가 있으므로 MemberRepository의 구현체에서 Map이 아닌 ConcurrentHashMap을 사용해야함.

**Hashtable**
주요 메소드(put, get 등)에 synchronized 키워드가 선언되어 있음. key, value에 null을 허용하지 않음

> **synchronized**
> 언제?
> 스레드간 서로 공유하고 수정할 수 있는 data가 있는데 스레드간 동기화가 되지 않은 상태에서 멀티스레드 프로그램을 돌리면, data의 안정성과 신뢰성을 보장할 수 없음.
> 무언인가?
> 여러 개의 스레드가 한 개의 자원을 사용하고 할 때, 현재 데이터를 사용하고 있는 해당 스레드를 제외하고 나머지 스레들은 데이터에 접근할 수 없도록 막는 개념.
> 단점?
> 자바 내부적으로 메서드나 변수에 동기화를 하기 위해 block과 unblock을 처리하므로 남발하면 성능저하.

**HashMap**
synchronized 없음, null 가능

**ConcurrentHashMap**
- HashMap을 thread-safe 하도록 만든 클래스
- key, value에 null 불가
- putIfAbsent()
키 값이 존재하면 기존의 값을 반환하고 없다면 입력한 값을 저장한 뒤 반환

**Map Common method**
clear()  
해당 콜렉션의 데이터를 초기화 합니다.
containsKey(key)
해당 콜렉션에 입력 받은 key를 가지고 있는지 체크합니다.
containsValue(value)
해당 콜렉션에 입력 받은 value를 가지고 있는지 체크합니다.
remove(key)
해당 콜렉션에 입력 받은 key의 데이터(key도 포함)를 제거합니다.
isEmpty()
해당 콜렉션이 비어 있는지 체크합니다.
size()
해당 콜렉션의 엔트리(Entry) 또는 세그먼트(Segment) 사이즈를 반환합니다.

_동기화 테스트시, synchronized 키워드가 없는 HashMap은 동기화가 이루어지지 않아 엔트리 사이즈가 비정상적으로 출력된다. 동시성 이슈 발생_