## 💭 ORM

- Object Relational Mapping: 객체 관계 매핑
    - 객체지향 언어에서 의미하는 객체와 RDB의 테이블을 자동으로 매핑하는 방법
    - 객체지향 언어에서의 객체 → 클래스를 의미
    - 클래스는 데이터베이스의 테이블과 매핑하기 위해 만들어진 것이 X → RDB 테이블과 불일치 존재

- 이 둘의 불일치와 제약사항을 해결하는게 바로 <span style='background-color: #dcffe4'>ORM</span>
    - 애플리케이션의 클래스와 데이터베이스의 테이블을 매핑하는 것
    - ORM 이용 시 쿼리문 작성이 아닌 코드(메서드)로 데이터 조작 가능
        ![](https://velog.velcdn.com/images/dlgkdis801/post/b9866add-d3fe-4e8e-a303-116b5ff4bf04/image.png)

- ORM 장점
    - ORM을 사용하면서 데이터베이스 쿼리를 객체지향적으로 조작할 수 있음
        - 쿼리문을 작성하는 양이 현저히 줄어듦 → 개발 비용 감소
        - 객체지향적으로 데이터베이스에 접근할 수 O → 코드 가독성 UP
    - 재사용 및 유지보수가 편함
        - ORM을 통해 매핑된 객체는 모두 독립적으로 작성되어 있어 재사용 용이
        - 객체들은 각 클래스로 나뉘어 있어 유지보수 수월
    - 데이터베이스에 대한 종속성 감소
        - ORM을 통해 자동 생성된 SQL문 → 객체 기반으로 데이터베이스 테이블을 관리하기 때문에 데이터베이스에 종속적이지 않음
        - 데이터베이스를 교체하는 상황에서도 비교적 적은 리스크 부담

- ORM 단점
    - ORM만으로 온전한 서비스 구현에는 한계
        - 복잡한 서비스의 경우 직접 쿼리를 구현하지 않고 코드로 구현하기 어려움
        - 복잡한 쿼리를 정확한 설계 없이 ORM만으로 구성하게 되면 속도 저하 등의 성능 문제 발생
    - 애플리케이션의 객체 관점과 데이터베이스의 관계 관점의 불일치 발생
        - Granularity(세분성)
            - ORM의 자동 설계 방법에 따라 데이터베이스에 있는 테이블 수와 애플리케이션의 Entity 클래스의 수가 다른 경우가 생김(=클래스가 테이블의 수보다 많아질 수 있음)
        - Inheritance(상속성)
            - RDBMS에는 상속 개념이 없음
        - Identity(식별성)
            - RDBMS는 기본키(primary key)로 동일성 정의 → 자바는 두 객체의 값이 같아도 다르다고 판단할 수 있음
            - 식별과 동일성의 문제
        - Associations(연관성)
            - 객체지향 언어
                - 객체를 참조함으로써 연관성을 나타냄
                - 객체 참조 시 방향성 존재
            - RDBMS
                - 외래키(foreign key)를 삽입함으로써 연관성을 표현
                - 외래키를 삽입하는 것은 양방향의 관계를 가지기 때문에 방향성 X
        - Navigation(탐색)
            - 자바와 RDBMS는 어떤 값(객체)에 접근하는 방식이 다름
                - 자바
                    - 특정 값에 접근하기 위해 객체 참조 같은 연결 수단 활용
                    - 객체를 연결하고 또 연결해서 접근하는 그래프 형태의 접근 방식
                    - 예: 어떤 멤버의 회사 주소를 구하기 위해  `member.getOrganization().getAddress()` 와 같이 접근할 수 있음
                - RDBMS
                    - 쿼리를 최소화하고 JOIN을 통해 여러 테이블을 로드하고 값을 추출하는 접근 방식을 채택하고 있음

<br>
<br>

## 💭 JPA

- Java Persistence API
    - 자바 진영의 ORM 기술 표준으로 채택된 인터페이스의 모음
    - ORM이 큰 개념이라면 JPA는 더 구체화된 스펙을 포함
    - 즉, JPA 또한 실제로 동작하는 것이 아니고 어떻게 동작해야 하는지 메커니즘을 정리한 표준 명세로 생각하면 됨
        ![](https://velog.velcdn.com/images/dlgkdis801/post/e28577a5-a70f-4105-af78-2e8c6d0f4cb8/image.png)

- JPA의 메커니즘
    - 내부적으로 JDBC를 사용
    - 개발자가 직접 JDBC를 구현하면 SQL에 의존하게 되는 문제가 있어 개발 효율성이 떨어짐
    - JPA는 이러한 문제점을 보완해 개발자 대신 적절한 SQL을 생성하고 데이터베이스를 조작해 객체를 자동 매핑하는 역할을 수행

- JPA 기반의 구현체 3가지
    - ⭐️하이버네이트(Hibernate)⭐️
    - 이클립스 링크(EclipseLink)
    - 데이터 뉴클리어스(DataNucleus)
        ![](https://velog.velcdn.com/images/dlgkdis801/post/ecca36d2-b259-4d2f-b8cb-f955ba9ccf62/image.png)

<br>
<br>

## 💭 하이버네이트

- Hibernate
    - 자바의 ORM 프레임워크
    - JPA가 정의하는 인터페이스를 구현하고 있는 JPA 구현체 중 하나
    - Spring Data JPA 활용 → 이 책에서는 JPA 자체를 직접 사용할 일은 거의 X

- Spirng Data JPA
    - JPA를 편리하게 사용할 수 있도록 지원하는 스프링 하위 프로젝트 중 하나
    - CRUD 처리에 필요한 인터페이스를 제공
    - 하이버네이트의 엔티티 매니저(EntityManager)를 직접 다루지 않고 리포지토리를 정의해 사용 → 스프링이 적합한 쿼리를 동적으로 생성하는 방식으로 데이터베이스 조작
    - 하이버네이트에서 자주 사용되는 기능을 더 쉽게 사용할 수 있게 구현한 라이브러리
        ![](https://velog.velcdn.com/images/dlgkdis801/post/8d5d8e75-92b8-4a04-b4ea-47a6b680424e/image.png)

<br>
<br>

## 💭 영속성 컨텍스트

### Persistence Context

- 애플리케이션과 데이터베이스 사이에서 엔티티와 레코드의 괴리를 해소하는 기능과 객체를 보관하는 기능 수행
- 엔티티 객체가 영속성 컨텍스트에 들어오면 → JPA는 엔티티 객체의 매핑 정보를 데이터베이스에 반영하는 작업 수행
- 엔티티 객체가 영속성 컨텍스트에 들어와 JPA의 관리 대상이 되는 시점부터는 해당 객체를 영속 객체(Persistence Object)라고 부름

- 애플리케이션과 데이터베이스와의 관계
    ![](https://velog.velcdn.com/images/dlgkdis801/post/6118fa4c-8a76-4da1-9e20-87dba8f0ad84/image.png)

- 영속성 컨텍스트의 특징
    - 세션 단위의 생명주기를 가짐
    - 데이터베이스에 접근하기 위한 세션이 생성되면 영속성 컨텍스트가 만들어짐
    - 세션이 종료되면 영속성 컨텍스트도 없어짐
    - 엔티티 매니저는 이러한 일련의 과정에서 영속성 컨텍스트에 접근하기 위한 수단으로 사용됨

<br>

### 엔티티 매니저

- 엔티티를 관리하는 객체
- 데이터베이스에 접근해서 CRUD 작업을 수행
- Spring Data JPA를 사용하면 레포지터리를 사용해 데이터베이스에 접근 → 실제 내부 구현체인 `SimpleJpaRepository`가 레포지터리에서 엔티티 매니저를 사용하는 것을 알 수 있음.

```java
// SimpleJpaRepository의 EntityManager 의존성 주입 코드
public SimpleJpaRepository(JpaEntityInformation<T, ?> entityInformation, EntityManagerentityManager) {
	Assert.notNull(entityInformation, "JpaEntityInformation must not be null!");
	Assert.notNull(entityManager, "EntityManager must not be null!");
	
	this.entityInformation = entityInformation;
	this.em = entityManager;
	this.provider = PersistenceProvider.fromEntityManager(entityManager);
}
```

- 엔티티 매니저는 엔티티 매니저 팩토리(EntityManagerFactory)가 만듦.
    - 엔티티 매니저 팩토리는 데이터베이스에 대응하는 객체로서 스프링부트에서는 자동 설정 기능이 있음
        - `application.properties`에서 작성한 최소한의 설정만으로도 동작하지만, JPA의 구현체 중 하나인 하이버네이트에서는 `persistaence.xml`이라는 설정 파일을 구성하고 사용해야 하는 객체
    - 엔티티 매니저 팩토리는 애플리케이션에서 단 하나만 생성, 모든 엔티티가 공유해서 사용
    - 엔티티 매니저 팩토리로 생성된 엔티티 매니저는 엔티티를 영속성 컨텍스트에 추가해 영속 객체로 만드는 작업을 수행
    - 영속성 컨텍스트와 데이터베이스를 비교하며 실제 데이터베이스를 대상으로 작업을 수행

```java
// 엔티티 매니저 팩토리 사용을 위한 persistence.xml 파일 설정

<?xml version="1.0" encoding="UTF-8" ?>

<persistence xmlns="http://xmlns.jcp.org/xml/ns/persistence"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/persistence/persistence_2_1/xsd"
	version="2.1">
	
	<persistence=unit name="entity_manager_factory" transaction-type="RESOURCE_LOCAL">
	
		<properties>
			<property name="javax.persistence.jdbc.driver" value="org.mariadb.jdbc.Driver" />
			<property name="javax.persistence.jdbc.user" value="root" />
			<property name="javax.persistence.jdbc.password" value="password" />
			<property name="javax.persistence.jdbc.url" value="jdbc:mariadb://localhost:3306/springboot" />
			<property name="hibernate.dialect" value="org.hibernate.dialect.MariaDB103Dialect" />
			
			<property name="hibernate.show_sql" value="true" />
			<property name="hibernate.format_sql" value="true" />
		
		</properties>

	</persistence-unit>
	
</persistence>
```

<br>

### 엔티티의 생명주기

- 비영속(New) : 영속성 컨텍스트에 추가되지 않은 엔티티 객체의 상태를 의미
- 영속(Managed) : 영속성 컨텍스트에 의해 엔티티 객체가 관리되는 상태
- 준영속(Detached) : 영속성 컨텍스트에 의해 관리되던 엔티티 객체가 컨텍스트와 분리된 상태
- 삭제(Removed) : 데이터베이스에서 레코드를 삭제하기 위해 영속성 컨텍스트에 삭제 요청을 한 상태

<br>
<br>

## 💭 데이터베이스 연동 - 교재와 달리 MySQL 사용함!

> 📣 Trobleshooting 참고 링크
- https://growingarchive.tistory.com/253
- [https://velog.io/@milkim0818/DB-Mac에서-MySQL설치-터미널로-접속하기](https://velog.io/@milkim0818/DB-Mac%EC%97%90%EC%84%9C-MySQL%EC%84%A4%EC%B9%98-%ED%84%B0%EB%AF%B8%EB%84%90%EB%A1%9C-%EC%A0%91%EC%86%8D%ED%95%98%EA%B8%B0)

<br>

### 프로젝트 생성

- [SwaggerConfig.java](http://SwaggerConfig.java) 내용 수정

```java
...

    public Docket restAPI() {
        return new Docket(DocumentationType.SWAGGER_2)
                .groupName("groupName1")
                .select()
                .apis(RequestHandlerSelectors.
                        basePackage("com.springboot.jpa"))

...
```

- [application.properties](http://application.properties) 데이터베이스 설정 추가

```java
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/springboot?serverTimezone=Asia/Seoul
spring.datasource.username=root
spring.datasource.password={비밀번호}

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
```

- build.gradle에 다음 의존성 추가

```java
...

//MySQL
	implementation 'org.springframework.boot:spring-boot-starter-data-jdbc'
	implementation 'org.springframework.boot:spring-boot-starter-data-jpa'

	//Lombok
	compileOnly 'org.projectlombok:lombok'
	runtimeOnly 'com.mysql:mysql-connector-j'
	annotationProcessor 'org.projectlombok:lombok'
	
	...
```

- 연동 되었는지 확인
    - 첫 실행 시 데이터베이스를 MysqlWorkbench에서 생성했음에도 다음과 같은 오류 발생 가능
        ![](https://velog.velcdn.com/images/dlgkdis801/post/b76609bb-89ce-4675-b29f-e3add5b6bc39/image.png)

    - 터미널 환경에서 접속해서 만들어주면 해결됨.
        ![](https://velog.velcdn.com/images/dlgkdis801/post/e2315fcf-045b-4cc3-943e-d2e4e551c77c/image.png)

    - 재실행 시 잘 실행되는 모습
        ![](https://velog.velcdn.com/images/dlgkdis801/post/5f3041d6-5151-48e2-82ed-6b15dd491301/image.png)

<br>

> 📣 참고1: MySQL 실행
- `mysql.server start`
    - 종료 시 : `mysql.server stop`
        ![](https://velog.velcdn.com/images/dlgkdis801/post/643c50bc-58c9-4cb7-8c8c-3fd127d84c06/image.png)

<br>

> 📣 참고2: properties 환경변수 설정
![](https://velog.velcdn.com/images/dlgkdis801/post/122dfd85-4ce9-4c47-94b7-7e9ffcc5d280/image.png)
![](https://velog.velcdn.com/images/dlgkdis801/post/522e1365-0fb2-44cd-bb40-dd9d119875ff/image.png)
>
> > 환경변수를 넣는 부분이 안보인다면?
> >
> > - Modify options > Environment variables 설정해주기!
> > ![](https://velog.velcdn.com/images/dlgkdis801/post/e562bbd2-05be-4986-bd0e-e3a3fe6aa1db/image.png)
> > ![](https://velog.velcdn.com/images/dlgkdis801/post/5c4c2025-c837-4a65-a5cb-b7a573c76980/image.png)
>
> - 환경변수 내용 작성 및 저장
    ![](https://velog.velcdn.com/images/dlgkdis801/post/17299751-78ea-48ae-b750-d603b028301e/image.png)

<br>

> 📣 참고3: 설정파일 ignore
> - 다음 링크 참고 : [https://velog.io/@dlgkdis801/.gitignore-미적용-문제-발생-시-해결방법](https://velog.io/@dlgkdis801/.gitignore-%EB%AF%B8%EC%A0%81%EC%9A%A9-%EB%AC%B8%EC%A0%9C-%EB%B0%9C%EC%83%9D-%EC%8B%9C-%ED%95%B4%EA%B2%B0%EB%B0%A9%EB%B2%95)

<br>
<br>

### 하이버네이트의 활성화 선택

- 5가지 분류
    - create : 애플리케이션이 가동되고 SessionFactory가 실행될 때, 기존 테이블을 지우고 새로 생성
    - create-drop : create와 동일한 기능을 수행하나 애플리케이션을 종료하는 시점에 테이블을 지움
    - update : SessionFactory가 실행될 때 객체를 검사해서 변경된 스키마를 갱신. 기존에 저장된 데이터는 유지됨
    - validate : update처럼 객체를 검사하지만 스키마는 건드리지 않음. 검사 과정에서 데이터베이스의 테이블 정보와 객체의 정보가 다르면 에러 발생
    - none : ddl-auto 기능을 사용하지 않음

- 운영 환경에서는 create, create-drop, update 기능은 사용하지 않음.
    - 데이터베이스에 축적된 데이터를 지워버릴 수도 있고, 사람의 실수로 객체의 정보가 변경되었을 경우 운영 환경의 데이터베이스 정보까지 변경될 수 있기 때문
    - 운영 환경에서는 대체로 validate나 none을 사용함

- 개발 환경에서는 create 또는 update를 사용하는 편

- show-sql
    - 로그에 하이버네이트가 생성한 쿼리문을 출력하는 옵션
    - 아무 설정이 없으면 저장에 용이한 형태로 출력되기 때문에 사람이 보기에는 불편하게 한 줄로 출력됨.
    - format_sql 옵션으로 보기 좋게 포맷팅까지 해주기!

<br>
<br>

## 💭 엔티티 설계

- 

<br>
<br>

## 💭 리포지토리 인터페이스 설계

- 

<br>
<br>

## 💭 DAO 설계

- 

<br>
<br>

## 💭 DAO 연동을 위한 컨트롤러와 서비스 설계

- 

<br>
<br>

## 💭 [한걸음 더] 반복되는 코드의 작성을 생략하는 방법 - 롬복

-
