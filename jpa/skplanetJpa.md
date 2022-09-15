# [토크ON세미나] JPA 프로그래밍 기본기 다지기 1강 - JPA 소개 | T아카데미
- 객체를 자바 컬렉션에 저장하듯이 DB에 저장할 수는 없을까? 라는 고민에서 나옴
- JPA(Java Persistence API) : 자바진영의 ORM 표준
- ORM(Object Relational Mapping) : 객체는 객체대로, DB는 DB대로 설계하고 ORM 프레임워크가 중간에서 매핑
- JPA 성능 최적화 기능
>- 1차캐시와 동일성 보장
>- 트랜잭션을 지원하는 쓰기 지연 - INSERT ( 모았다가 한번에 Commit) >> 설정필요
>- 지연 로딩과 즉시 로딩 >> 설정 필요

# [토크ON세미나] JPA 프로그래밍 기본기 다지기 2강 - JPA 기초와 매핑 | T아카데미
- java application에 직접코딩
```
psvm
  EntityManagerFactory emf = Persistence.createEntityManagerFactory("hello"); // 설정가져오기
  EntityManager em = emf.createEntityManager();
  EntityTransaction tx = em.getTransaction();
  tx.begin()
  Member member = new Member();
  member.setId(100L);
  member.setName("KSK");
  em.persist(member);
  tx.commit();
  em.close();
  emf.close();
```
- 엔티티 매니저 팩토리는 하나만 생성해서 해플리케이션 전체에서 공유
- 엔티티 매니저는 쓰레드간 공유하면 안된다(사용하고 버려야 한다)
- JPA의 모든 데이터 변경은 트랜잭션 안에서 실행

# [토크ON세미나] JPA 프로그래밍 기본기 다지기 3강 - 필드와 컬럼 매핑 | T아카데미
