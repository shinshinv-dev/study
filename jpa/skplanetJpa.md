# [토크ON세미나] JPA 프로그래밍 기본기 다지기 1강 - JPA 소개
- 객체를 자바 컬렉션에 저장하듯이 DB에 저장할 수는 없을까? 라는 고민에서 나옴
- JPA(Java Persistence API) : 자바진영의 ORM 표준
- ORM(Object Relational Mapping) : 객체는 객체대로, DB는 DB대로 설계하고 ORM 프레임워크가 중간에서 매핑
- JPA 성능 최적화 기능
>- 1차캐시와 동일성 보장
>- 트랜잭션을 지원하는 쓰기 지연 - INSERT ( 모았다가 한번에 Commit) >> 설정필요
>- 지연 로딩과 즉시 로딩 >> 설정 필요

# [토크ON세미나] JPA 프로그래밍 기본기 다지기 2강 - JPA 기초와 매핑
- java application에 직접코딩
```java
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

# [토크ON세미나] JPA 프로그래밍 기본기 다지기 3강 - 필드와 컬럼 매핑
- 데이터 베이스 스키마 자동 생성하기
>- DDL을 애플리케이션 실행 시점에 자동생성 (이렇게 생성된것은 개발에서만 사용권고)
>- hibernate.hbm2ddl.auto
>>- create/create-drop/update/validate/none
- 매핑 어노테이션
>- @Column
```java
@Column(name = "USERNAME")
private String name;
```
>- @Temporal
>>- 날짜타입매핑
>>- 어플리케이션에서 사용하지만 DB 에는 저장하지 않을 필드
>- @Enumerated(EnumType.STRING) 
>>- 현업에서는 무조건 STRING, ODINAL일 경우 숫자가 DB 에 저장
>- @Lob
>>- String 타입에 쓰면 CLOB, Byte 타입에 쓰면 BLOB
>- @Transient
- 식별자 매핑
>- @Id(직접 매핑)
>- @GeneratedValue(strategy = GenerationType.IDENTITY)
>>- IDENTITY : DB 에 위임
>>- SEQUENCE : 데이터베이스 시퀀스 오브젝트 사용
>>- TABLE : 키 생성용 테이블 사용
>>- AUTO: 방언에 따라 자동 지정
>- 권장 : Long + 대체키 + 키 생성전략 사용 (비지니스키에서 선택하지 않음)

# [토크ON세미나] JPA 프로그래밍 기본기 다지기 4강 - 연관관계 매핑
- 단방향매핑
```java
@Id @GeneratedValue
private Long id;
private String name;
private int age;

@ManyToOne
//@ManyToOne(fetch = FetchType.EAGER)
//@ManyToOne(fetch = FetchType.LAZY)
@JoinColumn(name = "TEAM_ID")
private Team team;
```
- LAZY로 바르는걸 권장


