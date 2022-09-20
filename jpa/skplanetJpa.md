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

# [토크ON세미나] JPA 프로그래밍 기본기 다지기 5강 - 양방향 매핑
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
- 연관관계 매핑 어노테이션
```java
@ManyToOne
@OneToMany
@OneToOne
@ManyToMany
@JoinColumn
@JoinTable
```
- 상속관계 매핑 어노테이션
```java
@Inheritance
@DiscriminatorColumn
@DiscriminatorValue
@MappedSuperclass
```
- 복합키 어노테이션
```java
@IdClass
@Embeddedld
@Embeddable
@MapsId
```

# [토크ON세미나] JPA 프로그래밍 기본기 다지기 6강 - JPA 내부구조
- 영속성 컨텍스트
>- : 엔티티를 영구 저장하는 환경
>- 논리적인 개념
>- 눈에 보이지 않음
>- 엔티티 매니저를 통해서 영속성 컨텍스트에 접근
```java
// 객체를 생성한 상태(비영속)
Member member = new Member();
member.setId("member1");
member.setUsername("admin");

// 객태를 저장한 상태(영속)
// 1차 캐시에 저장
em.persist(member);

// 1차 캐시에서 조회
Member findMember = em.find(Member.class, "member1");
// DB에서 조회해서 1차 캐시에 저장
Member findMember = em.find(Member.class, "member2");

```
- 1차 캐시에서 관리되는 상태를 영속상태라고 부름
- 쓰기 지연 SQL 저장소가 있어서 한꺼번에 커밋함
- 엔티티 수정 - 변경감지(Dirty Checking)
```java
Member memberA = em.find(Member.class, "memberA");

memberA.setUsername("hi");

// em.update(member) > 이런 코드 필요 없음

transaction.commit();
```
- 엔티티 삭제
```java
em.remove(memberA);
```
- 영속성 컨텍스트를 플러시하는 방법
>- em.flush() - 직접호출
>- 트랜잭션 커밋 - 플러시 자동 호출
>- JPQL 쿼리 실행 - 플러시 자동 호출
- 플러시
>- 영속성 컨텍스트를 비우지 않음
>- 영속성 컨텍스트의 변경내용을 데이터베이스에 동기화
>- 트랜잭션이라는 작업단위가 중요 > 커밋 직전에만 동기화 하면 됨
- 준영속 상태
>- 영속 > 준영속
>- 영속 상태의 엔티티가 영속성 컨텍스트에서 분리(detached)
>- 영속성 컨텍스트가 제공하는 기능을 사용 못함
- 준영속 상태로 만드는 방법
```java
// 특정 엔티티만 준영속 상태로 전환
em.detach(entity)

// 영속성 컨텍스트를 완전히 초기화
em.clear()

// 영속성 컨텍스트를 종료
em.close()

```
- 지연로딩 LAZY를 사용하면 연관된 엔티티를 프록시 객체로 만들어지고 실제 사용할때 다시 가져옴
- 프록시와 즉시로딩 주의
>- 가급적 지연 로딩을 사용
>- 즉시 로딩을 적용하면 예상하지 못한 SQL이 발생
>- 즉시 로딩은 JPQL에서 N+1 문제를 일으킴
>- @ManyToOne, @OneToOne은 기본이 즉시 로딩 > LAZY로 설정
>- @OneToMany, @ManyToMany는 기본이 지연로딩

# [토크ON세미나] JPA 프로그래밍 기본기 다지기 7강 - JPA 객체지향쿼리 | T아카데미
- 다양한 쿼리 방법을 지원
>- JPQL
>- JPA Criteria
>- QueryDSL
>- 네이티브 SQL
>- JDBC API 직접사용, MyBatis, SpringJdbcTemplate 함께 사용
- 이슈
>- 문제는 검색쿼리
>- 검색을 할때도 테이블이 아닌 엔티티 객체를 대상으로 검색
>- 모든 DB 데이터를 객체로 변환해서 검색하는 것은 불가능
>- 애플리케이션이 필요한 데이터만 DB 에서 불러오려면 결국 검색 조건이 포함된 SQL이 필요
- JPQL
>- 테이블이 아닌 객체를 대상으로 검색하는 객체 지향 쿼리
>- SQL 을 추상화해서 특정 DB SQL에 의존X
>- JPQL을 한마디로 정의하면 객체지향 SQL
>- 조인, 페치조인 가능
```java
String jpql = "select m From Member m where m.name like '%hello%'";
List<Member> result = em.createQuery(jpql, Member.class).getResultList();

// 파라미터 바인딩
String jpql = "select m From Member m where m.name =:name";
query.setParameter("name", nameParam);
```
- LAZY 로 설정했을때 갯수만큼 쿼리를 도는 문제가 "N+1" 문제
>- 해결방안이 페치조인
- Named 쿼리 - 어노테이션
>- 어플리케이션 로딩시점에 오류 확인가능

# [토크ON세미나] JPA 프로그래밍 기본기 다지기 8강 - Spring Data JPA와 QueryDSL 이해
- Spring Data JPA
>- 지루하게 반복되는 CRUD 문제를 세련된 방법으로 해결
>- 개발자는 인터페이스만 작성
>- 스프링 데이터 JPA가 구현 객체를 동적으로 생성해서 주입
>- 특정필드로 검색, 정렬, 페이징이 가능
>- @Query를 사용해서 직접 JPQL 지정 가능
```java
@Query("select m from Member where m.username = ?1")
Member findByUsername(String username, Pageable pageable);
```








#
