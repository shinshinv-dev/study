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
- 단방향 매핑
>- LAZY로 바르는걸 권장
```java
// class Member
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
- 양방향 매핑
>- Team 에서 Member 접근
```java
// class Team
@Id @GeneratedValue
private Long id;
private String name;

@OneToMany(mappedBy = "team")
List<Member> mebers = new ArrayList<Member>();

```

# [토크ON세미나] JPA 프로그래밍 기본기 다지기 5강 - 양방향 매핑 | T아카데미
- 양방향 매핑 규칙 (연관관걔의 주인)
>- 객체의 두 관계중 하나를 연관관걔의 주인으로 지정
>- 연관관계의 주인만이 외래 키를 관리(등록, 수정)
>- 주인이 아닌쪽은 읽기만 가능
>- 주인은 mappedBy 속성 사용 X
>- 주인이 아니면 mappedBy 속성으로 주인 지정
- 누구를 주인으로?
>- 외래키가 있는 곳을 주인으로 정해라
>- 여기서는 Member.team이 연관관계의 주인
- 왠만하면 단반향 매핑으로 설계하고 필요시만 양방향 사용
- 양방향 매핑시 연관관계의 주인에 값을 입력해야 함
>- 순수한 객체 관계를 고려하면 항상 양쪽다 값을 입력해야함
- 양방향 매핑의 장점
>- 단방향 매핑만으로도 이미 연관관계 매핑은 완료
>- 양방향 매핑은 반대 방향으로 조회(객체 그래프 탐색) 기능이 추가된 것 뿐
>- JPQL에서 역방향으로 탐색할 일이 많음
>- 단반향 매핑을 잘 하고 양방향은 필요할 때 추가해도 됨(테이블에 영향 X)









