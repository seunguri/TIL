크리스 리처드슨의 마이크로서비스패턴을 읽고 작성

# Pattern

> 특정 상황에서 발생하는 문제를 해결하는, 재사용 가능한 솔루션
> 

패턴의 진면목은 **솔루션의 장단점을 모두 따져 보고** 제대로 구현하려면 어떤 문제점을 해결해야 하는지 기술하는 것이다.

# 책 구성

### 1장

모놀리식 애플리케이션이 모놀리식 아키텍처라는 옷이 맞지 않을 정도로 커졌을 때 나타나는 **모놀리식 지옥의 징후**와 이 지옥을 **마이크로서비스 아키텍처를 도입해서 탈출하는 방안을** 모색합니다. 이 책 지면을 대부분 할애한 마이크로서비스 아키텍처 패턴 언어란 무엇인지 소개합니다.

- [마이크로서비스 패턴 언어란 무언인가](../msa/1_what_is_microservicespattrens.md) 

### 2장

소프트웨어 아키텍처의 중요성과 애플리케이션을 여러 서비스로 **분해하는 패턴**, 분해하는 과정에서 맞닥뜨리는 갖가지 장애를 극복하는 방법을 설명합니다.

### 3장

마이크로서비스 아키텍처에서 견고한 서비스 간 통신을 하기 위해 필요한 패턴을 소개하고,  **메시지 기반의 비동기 통신**이 최적인 이유를 설명합니다.

### 4장

**사가 패턴**을 이용하여 서비스 간 **데이터 일관성을 유지**하는 방법을 성명합니다 사가는 비동기 메시징을 통해 편성한 일련의 로컬 트랜잭션입니다.

### 5장

**도메인 주도 설계(DDD)**의 애그리거트 및 도메인 이벤트 패턴을 응용하여 서비스 비즈니스 로직을 어떻게 설계하는지 설명합니다.

### 6장

5장에 이어 **이벤트 소싱 패턴**으로 비즈니스 로직을 개발하는 방법을 설명합니다. 이벤트 소싱은 이벤트를 중심으로 비즈니스 로직을 구성하고 도메인 객체를 저장하는 패턴입니다.

### 7장

**API 조합 패턴, 커맨드 쿼리 책임 분산(CQRS) 패턴**을 이용하여 여러 서비스에 분산된 데이터 조회 쿼리를 구현하는 방법을 설명합니다.

### 8장

모바일 앱, 브라우저에서 작동되는 자바스크립트 애플리케이션, 서드파티 애플리케이션 등 다양한 **외부 클라이언트 요청을 외부 API 패턴으로 처리**하는 방법을 다룹니다.

### 9장

**마이크로서비스 아키텍처의 자동화 테스트 기법**을 소개합니다. 내용이 많아 9장과 10장, 두 장에 걸쳐 이야기합니다. 테스트 피라미드는 테스트 유형별 상대적인 비율을 나타낸 개념입니다. 테스트 피라미드의 하부를 떠받치고 있는 **단위 테스트**를 어떻게 작성하는지 설명합니다.

### 10장

9장에 이어 테스트 피라미드에 있는 **다른 유형의 테스트**(통합 테스트, 컨슈머 주도 계약 테스트, 컴포넌트 테스트)의 작성 방법을 알려 드립니다.

### 11장

보안, 외부화 구성 패턴, 서비스 관측성 패턴 등 **프로덕션 레디 서비스 개발**에 관한 여러가지 주제를 이야기합니다. 서비스 관측성 패턴은 로그 수집, 애플리케이션 지표, 분산 추적을 포함한 개념입니다.

### 12장

가상 머신, 컨테이너, 서버리스 등 **서비스 배포 시 사용 가능한 다양한 개발 패턴**을 살펴봅니다. **서비스 메시**는 마이크로서비스 아키텍처에서 통신을 조정하는 네트워킹 소프트웨어 계층입니다, 서비스 메시를 사용하면 어떤 혜택이 있는지 설명합니다.

### 13장

**스트랭글러 애플리케이션 패턴**에 따라 모놀리식 아키텍처를 마이크로서비스 아키텍처로 단계적으로 리팩터링하는 방법을 소개합니다. 이 스트랭글러 패턴은 새 기능을 서비스로 구현하고 모놀리스에서 모듈을 추출하여 각각 서비스로 전환하는 애플리케이션 개발 패턴입니다.