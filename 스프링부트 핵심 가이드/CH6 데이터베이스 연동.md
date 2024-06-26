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

### 엔티티 클래스

- Spring Data JPA를 사용하면 데이터베이스에 테이블을 생성하기 위해 직접 쿼리를 작성할 필요가 없음. → 이 기능을 가능하게 하는 것이 엔티티
- JPA에서의 엔티티
    - 데이터베이스의 테이블에 대응하는 클래스
    - 엔티티에는 데이터베이스에 쓰일 테이블과 칼럼을 정의함
    - 엔티티에 어노테이션을 사용하면 테이블 간의 연관 관계 정의 가능

- 엔티티 클래스로 구현하기
    - `data.entity` 패키지를 생성하고 그 안에 `Product`  엔티티 클래스를 생성
        ![](https://velog.velcdn.com/images/dlgkdis801/post/79672226-6b68-481a-8cc3-ac64468e3428/image.png)
  
    - data/entity/Product.java
      ```java
      package com.springboot.api.data.entity;

      import javax.persistence.*;
      import java.time.LocalDateTime;

      @Entity
      @Table(name = "product")
      public class Product {

          @Id
          @GeneratedValue(strategy = GenerationType.IDENTITY)
          private Long number;

          @Column(nullable = false)
          private String name;

          @Column(nullable = false)
          private Integer price;

          @Column(nullable = false)
          private Integer stock;

          private LocalDateTime createdAt;
          private LocalDateTime updatedAt;

      }
      ```

    ![](https://velog.velcdn.com/images/dlgkdis801/post/6cec027a-e928-40d6-9fe3-1b2a4303b23c/image.png)

    
    - 위와 같이 클래스를 생성하고 `application.properties` 에 정의한 `spring.jpa.hibernate.ddl-auto` 의 값을 `create` 같은 테이블을 생성하는 옵션으로 설정 → 쿼리문을 작성하지 않아도 데이터베이스에 테이블이 자동으로 만들어짐.

<br>

### 엔티티 관련 기본 어노테이션

- 엔티티 작성 시 어노테이션을 많이 사용!
    - 테이블과 매핑하기 위해 사용하는 어노테이션
    - 다른 테이블과의 연관관계를 정의하기 위해 사용하는 어노테이션
    - 자동으로 값을 주입하기 위한 어노테이션

- `@Entity`
    - 해당 클래스가 엔티티임을 명시하기 위한 어노테이션
    - 클래스 자체는 테이블과 일대일로 매칭
    - 해당 클래스의 인스턴스는 매핑되는 테이블에서 하나의 레코드를 의미
    
- `@Table`
    - 엔티티 클래스는 테이블과 매핑 → 특별한 경우가 아니면 `@Table`  어노테이션이 필요하지 않음.
    - `@Table` 어노테이션을 사용할 때는 클래스의 이름과 테이블의 이름을 다르게 지정해야 하는 경우임.
    - 이 어노테이션을 명시하지 않는 경우 → 테이블의 이름과 클래스의 이름이 동일하다는 의미
        - 서로 다른 이름을 사용하려면? `@Table(name = 값)` 형태로 데이터베이스의 테이블명 명시
    - 대체로 자바 명명법과 데이터베이스가 사용하는 명명법이 달라 자주 사용됨.

- `@Id`
    - 엔티티 클래스의 필드는 테이블의 칼럼과 매핑됨.
    - 이 어노테이션이 선언된 필드 → 테이블의 기본 값 역할로 사용됨.
    - 모든 엔티티는 이 어노테이션 필요

- `@GeneraatedValue`
    - 일반적으로 `@Id` 어노테이션과 함께 사용됨.
    - 이 어노테이션은 해당 필드의 값을 어떤 방식으로 자동으로 생성할지 결정할 때 사용됨.
    
    > 값 생성 방식
    > 
    > - GeneratedValue를 사용하지 않는 방식(=직접 할당)
    >     - 애플리케이션에서 자체적으로 고유한 기본값을 생성할 경우 사용하는 방식
    >     - 내부에 정해진 규칙에 의해 기본값을 생성하고 식별자로 사용됨
    > 
    > - AUTO
    >     - `@GeneratedValue` 의 기본 설정 값
    >     - 기본값을 사용하는 데이터베이스에 맞게 자동 생성
    > 
    > - IDENTITY
    >     - 기본값 생성을 데이터베이스에 위임하는 방식
    >     - 데이터베이스의 `AUTO_INCREMENT` 를 사용해 기본값을 생성
    > 
    > - SEQUENCE
    >     - `@SequenceGenerator` 어노테이션으로 식별자 생성기를 설정하고 이를 통해 값을 자동 주입 받음.
    >     - `@SequenceGenerator` 를 정의할 때는 name, sequencceName, allocationSize를 활용
    >     - `@GeneratedValue` 에 생서기를 설정
    > 
    > - TABLE
    >     - 어떤 DBMS를 사용하더라도 동일하게 동작하기를 원할 경우 사용
    >     - 식별자로 사용할 숫자의 보관 테이블을 별도로 생성해서 엔티티를 생성할 때마다 값을 갱신해 사용
    >     - `@TableGenerator` 어노테이션으로 테이블 정보 설정

- `@Column`
    - 엔티티 클래스의 필드는 자동으로 테이블 칼럼으로 매핑
    - 별다른 설정을 하지 않을 예정이라면 이 어노테이션을 명시하지 않아도 됨.
    - `@Column` 어노테이션은 필드에 몇 가지 설정을 더할 때 사용함.
        
        ```java
        // Column 어노테이션의 요소 목록
        
        public @interface Column {
        	String name() default "";
        	
        	boolean unique() default false;
        	
        	boolean nullable() default true;
        	
        	boolean insertable() default true;
        	
        	boolean updatetable() default true;
        	
        	String columnDefinition() default "";
        	
        	String table() default "";
        	
        	int length() default 255;
        	
        	int precision() default 0;
        	
        	int scale() default 0;
        
        }	
        ```
        
    - 많이 사용하는 요소
        - name: 데이터베이스의 칼럼명을 설정하는 속성. 명시하지 않으면 필드명으로 지정
        - nullable: 레코드를 생성할 때 칼럼 값에 null 처리가 가능한지를 명시하는 속성
        - length: 데이터베이스에 저장하는 데이터의 최대 길이를 설정
        - unique: 해당 칼럼을 유니크로 설정

- `@Transient`
    - 엔티티 클래스에는 선언돼 있는 필드지만, 데이터베이스에서는 필요 없을 경우 이 어노테이션을 사용해 데이터베이스에서 이용하지 않게 할 수 있음.

<br>
<br>

## 💭 리포지토리 인터페이스 설계

- Spring Data JPA는 `JpaRepository` 를 기반으로 더욱 쉽게 데이터베이스를 사용할 수 있는 아키텍처를 제공
- 스프링 부트로 `JpaRepository` 를 상속하는 인터페이스 생성 → 기존의 다양한 메서드 손쉽게 활용 가능

### 리포지토리 인터페이스 생성

- 여기에서의 Repository : Spring Data JPA가 제공하는 인터페이스
- 엔티티를 데이터베이스의 테이블과 구조를 생성하는 데 사용했다면 리포지토리는 엔티티가 생성한 테이터베이스에 접근하는 데 사용됨

- Repository 생성
    - 접근하려는 테이블과 매핑되는 엔티티에 대한 인터페이스를 생성 + `JpaRepository`  상속받기
        - `ProductRepository` 가 `JpaRepository` 상속받을 때는 대상 엔티티와 기본값 타입을 지정해야 함.
        - 대상 엔티티를 `Product` 로 설정하고, 해당 엔티티의 `@Id`  필드 타입인 Long을 설정
            
            ```java
            package com.springboot.api.data.repository;
            
            import com.springboot.api.data.entity.Product;
            import org.springframework.data.jpa.repository.JpaRepository;
            
            public interface ProductRepository extends JpaRepository<Product, Long> {
            
            }
            ```

- 생성된 Repository는 `JpaRepository` 를 상속받으면서 별도의 메서드 구현 없이도 많은 기능 제공
    - `JpaRepository` 의 상속 구조
        - 타 Repository에서 만들어진 메서드는 모두 앞에서 생성한 `ProductRepository` 에서도 사용 가능
        ![](https://velog.velcdn.com/images/dlgkdis801/post/6d704498-9eb3-4ee9-8bcc-d0e5c13732a3/image.png)


<br>

### 리포지토리 메서드의 생성 규칙

- 일반적으로 CRUD(Create, Read, Update, Delete)에서 따로 생성해서 사용하는 메서드는 대부분 Read 부분에 해당하는 Select 쿼리뿐
    - 엔티티 저장, 갱신, 삭제 → 별도의 규칙이 필요하지 않음.
    - 다만 리포지토리에서 기본 제공하는 조회 메서드는 기본값으로 단일 조회하거나 전체 엔티티 조회하는 것만 지원(필요에 따라 다른 조회 메서드 필요)
    
- 메서드에 이름을 붙일 때는 첫 단어를 제외한 이후 단어들의 첫 글자를 대문자로 설정해야 JPA에서 정상적 인식 및 쿼리 자동 생성 가능
    
    > **조회 메서드(find)에 조건으로 붙일 수 있는 몇 가지 기능**
    > 
    > - FindBy
    >     - SQL문의 where절 역할을 수행하는 구문
    >     - findBy 뒤에 엔티티의 필드값을 입력해 사용
    >     - ex) findByName(String name)
    >     
    > - AND, OR
    >     - 조건을 여러 개 설정하기 위해 사용
    >     - ex) findBynameAndEmail(Stirng name, String email)
    >     
    > - Like / NotLike
    >     - SQL문의 like와 동일한 긴으 수행
    >     - 특정 문자를 포함하는지 여부를 조건으로 추가
    >     - 비슷한 키워드 : Containing, Contains, isContaing
    >     
    > - StartsWith / StartingWith
    >     - 특정 키워드로 시작하는 문자열 조건 설정
    >     
    > - EndsWith / EndingWith
    >     - 특정 키워드로 끝나는 문자열 조건 설정
    >     
    > - IsNull / IsNotNull
    >     - 레코드 값이 Null이거나 Null이 아닌 값을 검색
    >     
    > - True / False
    >     - Boolean 타입의 레코드를 검색할 때 사용
    >     
    > - Before / After
    >     - 시간을 기준으로 값을 검색
    >     
    > - LessThan / GreaterThan
    >     - 특정 값(숫자)를 기준으로 대소 비교 할 때 사용
    >     
    > - Between
    >     - 두 값(숫자) 사이의 데이터 조회

<br>
<br>

## 💭 DAO 설계

### DAO(Data Access Object)

- 데이터베이스에 접근하기 위한 로직을 관리하기 위한 객체
- 비즈니스 로직의 동작 과정에서 데이터를 조작하는 기능 → DAO 객체가 수행
- 다만, 스프링 데이터 JPA에서 DAO의 개념은 리포지토리가 대체

- 규모가 작은 서비스
    - DAO를 별도로 설계하지 않고 바로 서비스 레이어에서 데이터베이스에 접근해서 구현하기도 함.
    - 그러나, 이 책에서는 DAO를 서비스 레이어와 리포지토리의 중간 계층을 구성하는 역할로 사용할 예정
    - 서비스 레이어에서 리포지토리의 메서드 호출 + 그 결과 처리 가능
        - 그러나 비즈니스 로직을 수행하는 과정에서 데이터베이스에 관한 작업을 처리하는 것은 기능을 분리하고 관리하기 좋은 코드로 볼 수 X


> 📣 DAO vs Repository
> - Repository는 Spring Data JPA에서 제공하는 기능이기 때문에 기존의 스프링 프레임워크나 스프링 MVC의 사용자는 `Repostory 대신 DAO 객체로 데이터베이스에 접근`함.
> - 이러한 측면에서 각 컴포넌트의 역할을 고민하는 시간을 가지면 좋을 것 같음.

<br>

### DAO 클래스 생성

- 인터페이스 설계
    - 📁 data/dao/ProductDAO.java
        
        ```java
        package com.springboot.api.data.dao;
        
        import com.springboot.api.data.entity.Product;
        
        public interface ProductDAO {
            Product insertProduct(Product product);
        
            Product selectProduct(Long number);
        
            Product updateProductName(Long number, String name) throws Exception;
        
            void deleteProduct(Long number) throws Exception;
        };
        
        ```
        

- 일반적으로 데이터베이스에 접근하는 메서드는 리턴 값으로 데이터 객체를 전달
    - 데이터 객체를 엔티티 객체로 전달 vs DTO 객체로 전달할지에 대해 의견 분분
    - 일반적 설계 원칙 → 엔티티 객체는 데이터베이스에 접근하는 계층에서만 사용하도록 정의
    - 다른 계층으로 데이터를 전달할 때는 DTO 객체를 사용

- 인터페이스 구현체 클래스 작성
    - 📁 data/dao/impl/ProductDAOImpl.java
    ```java
        package com.springboot.api.data.dao.impl;
        
        import com.springboot.api.data.dao.ProductDAO;
        import com.springboot.api.data.entity.Product;
        import com.springboot.api.data.repository.ProductRepository;
        import org.springframework.beans.factory.annotation.Autowired;
        import org.springframework.stereotype.Component;
        
        import java.time.LocalDateTime;
        import java.util.Optional;
        
        @Component
        public class ProductDAOImpl implements ProductDAO {
        
            private final ProductRepository productRepository;
        
            @Autowired
            public ProductDAOImpl(ProductRepository productRepository){
                this.productRepository = productRepository;
            }
        
            //Product 엔티티를 데이터베이스에 저장하는 기능 수행
            @Override
            public Product insertProduct(Product product){
                Product savedProduct = productRepository.save(product);
                return savedProduct;
            }
        
            //조회
            @Override
            public Product selectProduct(Long number){
                Product selectProduct = productRepository.getById(number);
                return selectProduct;
            }
        
            //업데이트
            @Override
            public Product updateProductName(Long number, String name) throws Exception {
                Optional<Product> selectedProduct = productRepository.findById(number);
        
                Product updatedProduct;
                if(selectedProduct.isPresent()) {
                    Product product = selectedProduct.get();
        
                    product.setName(name);
                    product.setUpdatedAt(LocalDateTime.now());
        
                    updatedProduct = productRepository.save(product);
                } else {
                    throw new Exception();
                }
        
                return updatedProduct;
            }
        
            //삭제
            @Override
            public void deleteProduct(Long number) throws Exception {
                Optional<Product> selectedProduct = productRepository.findById(number);
        
                if(selectedProduct.isPresent()){
                    Product product = selectedProduct.get();
        
                    productRepository.delete(product);
                } else {
                    throw new Exception();
                }
            }
        }
    ```
        
    > **getById()**
    > 
    > - 내부적으로 EntityManager와 getReference() 메서드를 호출함.
    > - getReference() 메서드를 호출하면 프록시 객체를 리턴
    >     - 실제 쿼리는 프록시 객체를 통해 최초로 데이터에 접근하는 시점에 실행
    >     - 이때 데이터가 존재하지 않는 경우 → EntityNotFoundException이 발생
    >     - JpaRepository의 실제 구현체인 SimpleJpaRepository의 getById() 메서드
    >         
    >         ```java
    >         //SimpleJpaRepository의 getById() 메서드
    >         @Override
    >         public T getById(ID id) {
    >         	Assert.notNull(id, ID_MUST_NOT_BE_NULL);
    >         	return em.getReference(getDomainClass(), id);
    >         }
    >         ```
    >         

    > **findById()**
    > 
    > - 내부적으로 EntityManager의 find() 메서드를 호출
    > - 이 메서드는 영속성 컨텍스트의 캐시에서 값을 조회한 후 영속성 컨텍스트에 값이 존재하지 않는다면 → 실제 데이터베이스에서 데이터를 조회
    > - 리턴 값으로 Optional 객체를 전달
    >     
    >     ```java
    >     // SimpleJpaRepository의 findById() 메서드
    >     
    >     @Override
    >     public Optional<T> findById(ID id) {
    >     	
    >     	Assert.notNull(id, ID_MUST_NOT_BE_NULL);
    >     	
    >     	Class<T> domainType = getDomainClass();
    >     	
    >     	if (metadata == null) {
    >     		return Optional.ofNullable(em.find(domainType, id));
    >     	}
    >     	
    >     	LockModeType type = metadata.getLockModeType();
    >     	
    >     	Map<String, Object> hints = new Hashmap<>();
    >     	getQueryHints().withFetchGraphs(em).forEach(hints::put);
    >     	
    >     	return Optional.ofNullable(type == null ? em.find(domainType, id, hints) : em.find(domainType, id, type, hints));
    >     }
    >     ```
    >     
    
    > **JPA에서 데이터의 값을 변경할 때는 다른 메서드와는 다른 점이 있음**
    > 
    > - JPA : 값을 갱신할 때 update라는 키워드 사용 X → 영속성 컨텍스트를 활용해 값을 갱신
    > - find() 메서드를 통해 데이터베이스에서 값을 가져오면 가져온 객체가 영속성 컨텍스트에 추가됨.
    > - 영속성 컨텍스트가 유지되는 상황에서 객체의 값을 변경하고 다시 save()를 실행 → JPA에서는 **Dirty Check**라고 하는 변경 감지를 수행함.
    >     - `@Transactional` 어노테이션이 지정돼 있으면 → 메서드 내 작업을 마칠 경우 자동으로 `flush()` 메서드를 실행함.
    >     - 이 과정에서 변경이 감지되면 → 대상 객체에 해당하는 데이터베이스의 레코드를 업데이트하는 쿼리가 실행됨.
    > 
    > ```java
    > //SimpleJpaRepository의 save() 메서드
    > 
    > @Transactional
    > @Override
    > public <S extends T> S save(S entity) {
    > 	
    > 	Assert.notNull(entity, "Entity must not be null.");
    > 	
    > 	if(entityInformation.isNew(entity) {
    > 		em.persist(entity);
    > 		return entity;
    > 	} else {
    > 		return em.merge(entity);
    > 	}
    > }
    > ```
    > 
    
    > **데이터베이스의 레코드를 삭제하기 위해서는 삭제하고자 하는 레코드와 매핑된 영속 객체를 영속성 컨텍스트에 가져와야 함.**
    > 
    > - `deleteProduct()` 메서드는 `findById()` 메서드를 통해 객체를 가져오는 작업을 수행하고 `delete()` 메서드를 통해 해당 객체의 삭제 요청을 함.
    >     - `delete()` 메서드로 전달받은 엔티티가 영속성 컨ㅌ텍스트에 있는지 파악하고, 해당 엔티티를 영속성 컨텍스트에 영속화하는 작업을 거쳐 데이터베이스의 레코드와 매핑
    >     - 매핑된 영속 객체를 대상으로 삭제 요청을 수행하는 메서드를 실행해 작업을 마치고 commit 단계에서 삭제를 진행
    > 
    > ```java
    > // SimpleJpaRepository의 delete() 메서드
    > 
    > @Override
    > @Transactional
    > @SuppressWarnings("unchecked")
    > 
    > public void delete(T entity) {
    > 	
    > 	Assert.notNull(entity, "Entity must not be null!");
    > 	
    > 	if(entityInformation.isNew(entity) {
    > 		return;
    > 	}
    > 	
    > 	Class<?> type = ProxyUtils.getUserClass(entity);
    > 	
    > 	T existing = (T) em.find(type, entityInformation.getId(entity));
    > 	
    > 	//if the entity to be deleted doesn't exist, delete is a NOOP
    > 	if(existing == null) {
    > 		return;
    > 	}
    > 	
    > 	em.remove(em.contains(entity) ? entity : em.merge(entity);
    > ```
    >

<br>
<br>

## 💭 DAO 연동을 위한 컨트롤러와 서비스 설계

### 서비스 클래스 만들기

- 서비스 레이어에서는 도메인 모델(Domain Model)을 활용해 애플리케이션에서 제공하는 핵심 기능을 제공

- 서비스 인터페이스를 작성하기 전에 필요한 DTO 클래스 생성하기
    - 📁 data/dto/ProductDTO.java
        
        ```java
        package com.springboot.api.data.dto;
        
        public class ProductDTO {
        
            private String name;
            private int price;
            private int stock;
        
            public ProductDTO(String name, int price, int stock){
                this.name = name;
                this.price = price;
                this.stock = stock;
            }
        
            public String getName() {
                return name;
            }
        
            public void setName(String name){
                this.name = name;
            }
        
            public int getPrice() {
                return price;
            }
        
            public void setPrice(int price) {
                this.price = price;
            }
        
            public int getStock() {
                return stock;
            }
        
            public void setStock(int stork){
                this.stock = stock;
            }
        }
        ```
        
    - 📁 data/dto/ProductResponseDTO.java
        
        ```java
        package com.springboot.api.data.dto;
        
        public class ProductResponseDTO {
        
            private Long number;
            private String name;
            private int price;
            private int stock;
        
            public ProductResponseDTO(Long number, String name, int price, int stock){
                this.number = number;
                this.name = name;
                this.price = price;
                this.stock = stock;
            }
        
            public Long getNumber() {
                return number;
            }
        
            public void setNumber(Long number){
                this.number = number;
            }
        
            public String getName() {
                return name;
            }
        
            public void setName(String name){
                this.name = name;
            }
        
            public int getPrice(){
                return price;
            }
        
            public void setPrice(int price){
                this.price = price;
            }
        
            public int getStock(){
                return stock;
            }
        
            public void setStock(int stock){
                this.stock = stock;
            }
        }
        ```
        

- 서비스 인터페이스 작성
    - 기본적인 CRUD 기능 호출을 위해 간단히 메서드 정의
    - 📁 service/ProductService.java
        
        ```java
        package com.springboot.api.service;
        
        import com.springboot.api.data.dto.ProductDTO;
        import com.springboot.api.data.dto.ProductResponseDTO;
        import com.springboot.api.data.entity.Product;
        
        public interface ProductService {
            ProductResponseDTO getProduct(Long number);
            ProductResponseDTO saveProduct(ProductDTO productDTO);
        
            ProductResponseDTO changeProductName(Long number, String name) throws Exception;
        
            void deleteProduct(Long number) throws Exception;
        
        }
        ```
        
        - 설계 방법
            - DAO에서 구현한 기능을 서비스 인터페이스에서 호출해 결괏값을 가져오는 작업을 수행하도록 설계
            - 서비스: 클라이언트가 요청한 데이터를 적절하게 가공해 컨트롤러에게 넘기는 역할
            - 이 과정에서 여러 메서드 사용 → 지금은 간단하게 CRUD만 구현(다소 코드가 간단해 보일 수 있음)
            
    - 리턴 타입이 DTO?
        - DAO 객체에서 엔티티 타입을 사용하는 것을 고려 → 서비스 레이어에서 DTO 객체와 엔티티 객체를 각 레이어에 변환해서 전달하는 역할도 수행한다고 볼 수 있음
    
    - 데이터베이스와 밀접한 관련이 있는 데이터 액세스 레이어까지는 엔티티 객체를 사용
    - 클라이언트와 가까워지는 다른 레이어에서는 데이터를 교환하는 데 DTO 객체를 사용하는 것이 일반적
    
- 스프링부트 애플리케이션의 구조
    ![](https://velog.velcdn.com/images/dlgkdis801/post/f075cab6-8fa3-4acf-8874-18cd855763bf/image.png)

- 서비스 인터페이스 구현체 클래스
    - 📁 service/lmpl/ProductServicelmpl.java
        
        ```java
        package com.springboot.api.service.Impl;
        
        import com.springboot.api.data.dao.ProductDAO;
        import com.springboot.api.data.dto.ProductDTO;
        import com.springboot.api.data.dto.ProductResponseDTO;
        import com.springboot.api.service.ProductService;
        import org.springframework.beans.factory.annotation.Autowired;
        import org.springframework.stereotype.Service;
        
        @Service
        public class ProductServiceImpl implements ProductService {
            private final ProductDAO productDAO;
        
            @Autowired
            public ProductServiceImpl(ProductDAO productDAO){
                this.productDAO = productDAO;
            }
        
            @Override
            public ProductResponseDTO getProduct(Long number){
                return null;
            }
        
            @Override
            public ProductResponseDTO saveProduct(ProductDTO productDTO){
                return null;
            }
        
            @Override
            public ProductResponseDTO changeProductName(Long number, String name) throws Exception {
                return null;
            }
        
            @Override
            public void deleteProduct(Long number) throws Exception {
        
            }
        }
        ```
        

- 오류 발생
    - 'ProductResponseDTO(java.lang.Long, java.lang.String, int, int)' in 'com.springboot.api.data.dto.ProductResponseDTO' cannot be applied to '()’
    
    ```java
    package com.springboot.api.service.Impl;
    
    import com.springboot.api.data.dao.ProductDAO;
    import com.springboot.api.data.dto.ProductDTO;
    import com.springboot.api.data.dto.ProductResponseDTO;
    import com.springboot.api.data.entity.Product;
    import com.springboot.api.service.ProductService;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.stereotype.Service;
    
    import java.time.LocalDateTime;
    
    @Service
    public class ProductServiceImpl implements ProductService {
        private final ProductDAO productDAO;
    
        @Autowired
        public ProductServiceImpl(ProductDAO productDAO){
            this.productDAO = productDAO;
        }
    
        // getProduct() 메서드 구현
        @Override
        public ProductResponseDTO getProduct(Long number){
            Product product = productDAO.selectProduct(number);
    
            ProductResponseDTO productResponseDto = new ProductResponseDTO();
            productResponseDto.setNumber(product.getNumber());
            productResponseDto.setName(product.getName());
            productResponseDto.setPrice(product.getPrice());
            productResponseDto.setStock(product.getStock());
    
            return productResponseDto;
        }
    
        @Override
        public ProductResponseDTO saveProduct(ProductDTO productDTO){
            Product product = new Product();
            product.setName(productDTO.getName());
            product.setPrice(productDTO.getPrice());
            product.setStock(productDTO.getStock());
            product.setCreatedAt(LocalDateTime.now());
            product.setUpdatedAt(LocalDateTime.now());
    
            Product savedProduct = productDAO.insertProduct(product);
    
            ProductResponseDTO productResponseDTO = new ProductResponseDTO();
            productResponseDTO.setNumber(savedProduct.getNumber());
            productResponseDTO.setName(savedProduct.getName());
            productResponseDTO.setPrice(savedProduct.getPrice());
            productResponseDTO.setStock(savedProduct.getStock());
    
            return productResponseDTO;
        }
    
        @Override
        public ProductResponseDTO changeProductName(Long number, String name) throws Exception {
            Product changedProduct = productDAO.updateProductName(number, name);
    
            ProductResponseDTO productResponseDTO = new ProductResponseDTO();
            productResponseDTO.setNumber(changedProduct.getNumber());
            productResponseDTO.setName(changedProduct.getName());
            productResponseDTO.setPrice(changedProduct.getPrice());
            productResponseDTO.setStock(changedProduct.getStock());
    
            return productResponseDTO;
        }
    
        @Override
        public void deleteProduct(Long number) throws Exception {
            productDAO.deleteProduct(number);
        }
    }
    ```
    
    - 코드 수정
        - set 메서드를 사용하지 않고, 기존 생성자를 이용해서 ProductResponseDTO 객체 생성
        
        ```java
        package com.springboot.api.service.Impl;
        
        import com.springboot.api.data.dao.ProductDAO;
        import com.springboot.api.data.dto.ProductDTO;
        import com.springboot.api.data.dto.ProductResponseDTO;
        import com.springboot.api.data.entity.Product;
        import com.springboot.api.service.ProductService;
        import org.springframework.beans.factory.annotation.Autowired;
        import org.springframework.stereotype.Service;
        
        import java.time.LocalDateTime;
        
        @Service
        public class ProductServiceImpl implements ProductService {
            private final ProductDAO productDAO;
        
            @Autowired
            public ProductServiceImpl(ProductDAO productDAO){
                this.productDAO = productDAO;
            }
        
            // getProduct() 메서드 구현
            @Override
            public ProductResponseDTO getProduct(Long number){
                Product product = productDAO.selectProduct(number);
        
                return new ProductResponseDTO(product.getNumber(), product.getName(), product.getPrice(), product.getStock());
            }
        
            @Override
            public ProductResponseDTO saveProduct(ProductDTO productDTO){
                Product product = new Product();
                product.setName(productDTO.getName());
                product.setPrice(productDTO.getPrice());
                product.setStock(productDTO.getStock());
                product.setCreatedAt(LocalDateTime.now());
                product.setUpdatedAt(LocalDateTime.now());
        
                Product savedProduct = productDAO.insertProduct(product);
        
                return new ProductResponseDTO(savedProduct.getNumber(), savedProduct.getName(), savedProduct.getPrice(), savedProduct.getStock());
            }
        
            @Override
            public ProductResponseDTO changeProductName(Long number, String name) throws Exception {
                Product changedProduct = productDAO.updateProductName(number, name);
        
                return new ProductResponseDTO(changedProduct.getNumber(), changedProduct.getName(), changedProduct.getPrice(), changedProduct.getStock());
            }
        
            @Override
            public void deleteProduct(Long number) throws Exception {
                productDAO.deleteProduct(number);
            }
        }
        ```
        

### 컨트롤러 생성

- 컨트롤러는 클라이언트로부터 요청을 받고 해당 요청에 대해 서비스 레이어에 구현된 적절한 메서드를 호출해 결과값을 받음.
    - 📁 controller/ProductController.java
        
        ```java
        package com.springboot.api.controller;
        
        import com.springboot.api.data.dto.ChangeProductNameDTO;
        import com.springboot.api.data.dto.ProductDTO;
        import com.springboot.api.data.dto.ProductResponseDTO;
        import com.springboot.api.data.repository.ProductRepository;
        import com.springboot.api.service.ProductService;
        import org.springframework.beans.factory.annotation.Autowired;
        import org.springframework.http.HttpStatus;
        import org.springframework.http.ResponseEntity;
        import org.springframework.web.bind.annotation.*;
        
        @RestController
        @RequestMapping("/product")
        public class ProductController {
            private final ProductService productService;
        
            @Autowired
            public ProductController(ProductService productService){
                this.productService = productService;
            }
        
            @GetMapping()
            public ResponseEntity<ProductResponseDTO> getProduct(Long number){
                ProductResponseDTO productResponseDTO = productService.getProduct(number);
        
                return ResponseEntity.status(HttpStatus.OK).body(productResponseDTO);
            }
        
            @PostMapping()
            public ResponseEntity<ProductResponseDTO> createProduct(@RequestBody ProductDTO productDTO){
                ProductResponseDTO productResponseDTO = productService.saveProduct(productDTO);
        
                return ResponseEntity.status(HttpStatus.OK).body(productResponseDTO);
            }
        
            @PutMapping()
            public ResponseEntity<ProductResponseDTO> changeProductName(
                    @RequestBody ChangeProductNameDTO changeProductNameDTO) throws Exception{
                ProductResponseDTO productResponseDTO = productService.changeProductName(
                        changeProductNameDTO.getNumber(),
                        changeProductNameDTO.getName());
        
                return ResponseEntity.status(HttpStatus.OK).body(productResponseDTO);
            }
        
            @DeleteMapping(produces = "text/plain;charset=UTF-8")
            public ResponseEntity<String> deleteProduct(Long number) throws Exception {
                productService.deleteProduct(number);
        
                return ResponseEntity.status(HttpStatus.OK).body("정상적으로 삭제되었습니다.");
            }
        }
        
        ```


<br>

### Swagger API를 통한 동작 확인

- Post API
    - error
        
        ```java
        com.fasterxml.jackson.databind.exc.InvalidDefinitionException: Cannot construct instance of com.springboot.api.data.dto.ProductDTO (no Creators, like default constructor, exist): cannot deserialize from Object value (no delegate- or property-based Creator)
         at [Source: (org.springframework.util.StreamUtils$NonClosingInputStream); line: 2, column: 3]
        ```
        
    - 해결
        - ProductDTO의 기본 생성자 지정
            
            ```java
            package com.springboot.api.data.dto;
            
            public class ProductDTO {
            
                private String name;
                private int price;
                private int stock;
            
                public ProductDTO(){
                }
            
            ...
            ```
            
    
    ![](https://velog.velcdn.com/images/dlgkdis801/post/e6892a25-829a-491d-be72-5b85808d3bd9/image.png)

    ![](https://velog.velcdn.com/images/dlgkdis801/post/8e53b0ed-ab98-4135-9af8-d61b22815642/image.png)

    ![](https://velog.velcdn.com/images/dlgkdis801/post/5f6d04a2-61a0-4a8b-bc56-fffecbd1953a/image.png)

    ![](https://velog.velcdn.com/images/dlgkdis801/post/603411ae-afd0-4d6d-bbd1-28e8a39f8163/image.png)


- GET API
    
    ![](https://velog.velcdn.com/images/dlgkdis801/post/62097f8b-d14a-45dd-972d-920964d2424b/image.png)

    ![](https://velog.velcdn.com/images/dlgkdis801/post/555edaee-e4b0-4ccc-8aab-2778c4ae0324/image.png)

    
- PUT API
    
    ![](https://velog.velcdn.com/images/dlgkdis801/post/6ed114df-f463-435d-a74f-e231bda3c566/image.png)

    ![](https://velog.velcdn.com/images/dlgkdis801/post/b4afd3bc-7936-478a-8a8c-2c86fb5fa2d6/image.png)

    ![](https://velog.velcdn.com/images/dlgkdis801/post/ab5f2520-9550-4b96-b5e2-a6c28a134ac3/image.png)

    
- DELETE API
    ![](https://velog.velcdn.com/images/dlgkdis801/post/d6131787-2bc3-48cc-9e7e-d98477560904/image.png)

    ![](https://velog.velcdn.com/images/dlgkdis801/post/07ca15b7-80d8-4ff4-8b60-6ee152ba29e1/image.png)

    
    - 참고: Swagger 출력 한글 깨짐 현상 해결
        - DeleteMapping에 produces로 UTF-8 설정해주기
        
        ```java
        // ProductController.java
        
        ...
        
        @DeleteMapping(produces = "text/plain;charset=UTF-8")
        
        ...
        ```
        ![](https://velog.velcdn.com/images/dlgkdis801/post/b2ab9a89-8faf-474b-ad55-d2af567f53b5/image.png)

<br>
<br>

## 💭 [한걸음 더] 반복되는 코드의 작성을 생략하는 방법 - 롬복

### Lombok

- 데이터(모델) 클래스를 생성할 때 반복적으로 사용하는 getter/setter 같은 메서드를 어노테이션으로 대체하는 기능을 제공하는 라이브러리
- 자바에서 데이터 클래스를 작성하면 대게 많은 멤버 변수를 선언
- 각 멤버 변수별로 getter/setter 메서드를 만듦 → 코드가 길어지고 가독성 down

- Lombok의 장점
    - 어노테이션 기반 코드 자동 생성 → 생산성 UP
    - 반복되는 코드를 생략할 수 있음 → 가독성 UP
    - 롬복을 안다면 간단히 코드 유추 가능 → 유지보수 용이

- Lombok의 단점
    - 어노테이션이 자동 생성됨 → 메서드를 개발자 의도대로 정확히 구현하지 못하는 경우 발생

### Lombok 설치

- pom.xml(build.gradle) 파일에 다음 코드가 추가되어 있는지 확인
    
    ```java
    <dependencies>
    	...
    	<dependency>
    		<groupId>org.projectlombok</groupId>
    		<artifactId>lombok</artifactId>
    		<optional>true</optional>
    	</dependency>
    	...
    </dependencies>
    ```
    
    - build.gradle의 경우
        
        ```java
        ...
        
        dependencies {
        	//Lombok
        	compileOnly 'org.projectlombok:lombok'
        	runtimeOnly 'com.mysql:mysql-connector-j'
        	annotationProcessor 'org.projectlombok:lombok'
        
        	...
        }
        
        ...
        ```
        
    
- Lombok 플러그인 설치
    - settings > Plugins에서 Lombok 검색 후 설치
    ![](https://velog.velcdn.com/images/dlgkdis801/post/3afbe91e-6e8a-441b-946c-6cb8838e44a0/image.png)

    ![](https://velog.velcdn.com/images/dlgkdis801/post/f8759788-975f-4275-ba58-e12a9157b433/image.png)

<br>

### Lombok 적용

- Product.java
    
    ```java
    package com.springboot.api.data.entity;
    
    import lombok.*;
    
    import javax.persistence.*;
    import java.time.LocalDateTime;
    
    @Entity
    @Getter
    @Setter
    @NoArgsConstructor
    @AllArgsConstructor
    @EqualsAndHashCode
    @ToString(exclude = "name")
    @Table(name = "product")
    public class Product {
    
        @Id
        @GeneratedValue(strategy = GenerationType.IDENTITY)
        private Long number;
    
        @Column(nullable = false)
        private String name;
    
        @Column(nullable = false)
        private Integer price;
    
        @Column(nullable = false)
        private Integer stock;
    
        private LocalDateTime createdAt;
        private LocalDateTime updatedAt;
    
    }
    
    ```
    

- 적용 확인 방법
    - Refactor > Delombok > All Lombok annotations
        
        ![](https://velog.velcdn.com/images/dlgkdis801/post/0ff9417c-0f43-4b6c-b439-961c9061a11e/image.png)

        
        - 롬복 어노테이션이 실제 코드로 리팩토링됨.
            
            ```java
            package com.springboot.api.data.entity;
            
            import javax.persistence.*;
            import java.time.LocalDateTime;
            
            @Entity
            @Table(name = "product")
            public class Product {
            
                @Id
                @GeneratedValue(strategy = GenerationType.IDENTITY)
                private Long number;
            
                @Column(nullable = false)
                private String name;
            
                @Column(nullable = false)
                private Integer price;
            
                @Column(nullable = false)
                private Integer stock;
            
                private LocalDateTime createdAt;
                private LocalDateTime updatedAt;
            
                public Product(Long number, String name, Integer price, Integer stock, LocalDateTime createdAt, LocalDateTime updatedAt) {
                    this.number = number;
                    this.name = name;
                    this.price = price;
                    this.stock = stock;
                    this.createdAt = createdAt;
                    this.updatedAt = updatedAt;
                }
            
                public Product() {
                }
            
                public Long getNumber() {
                    return this.number;
                }
            
                public String getName() {
                    return this.name;
                }
            
                public Integer getPrice() {
                    return this.price;
                }
            
                public Integer getStock() {
                    return this.stock;
                }
            
                public LocalDateTime getCreatedAt() {
                    return this.createdAt;
                }
            
                public LocalDateTime getUpdatedAt() {
                    return this.updatedAt;
                }
            
                public void setNumber(Long number) {
                    this.number = number;
                }
            
                public void setName(String name) {
                    this.name = name;
                }
            
                public void setPrice(Integer price) {
                    this.price = price;
                }
            
                public void setStock(Integer stock) {
                    this.stock = stock;
                }
            
                public void setCreatedAt(LocalDateTime createdAt) {
                    this.createdAt = createdAt;
                }
            
                public void setUpdatedAt(LocalDateTime updatedAt) {
                    this.updatedAt = updatedAt;
                }
            
                public boolean equals(final Object o) {
                    if (o == this) return true;
                    if (!(o instanceof Product)) return false;
                    final Product other = (Product) o;
                    if (!other.canEqual((Object) this)) return false;
                    final Object this$number = this.getNumber();
                    final Object other$number = other.getNumber();
                    if (this$number == null ? other$number != null : !this$number.equals(other$number)) return false;
                    final Object this$name = this.getName();
                    final Object other$name = other.getName();
                    if (this$name == null ? other$name != null : !this$name.equals(other$name)) return false;
                    final Object this$price = this.getPrice();
                    final Object other$price = other.getPrice();
                    if (this$price == null ? other$price != null : !this$price.equals(other$price)) return false;
                    final Object this$stock = this.getStock();
                    final Object other$stock = other.getStock();
                    if (this$stock == null ? other$stock != null : !this$stock.equals(other$stock)) return false;
                    final Object this$createdAt = this.getCreatedAt();
                    final Object other$createdAt = other.getCreatedAt();
                    if (this$createdAt == null ? other$createdAt != null : !this$createdAt.equals(other$createdAt)) return false;
                    final Object this$updatedAt = this.getUpdatedAt();
                    final Object other$updatedAt = other.getUpdatedAt();
                    if (this$updatedAt == null ? other$updatedAt != null : !this$updatedAt.equals(other$updatedAt)) return false;
                    return true;
                }
            
                protected boolean canEqual(final Object other) {
                    return other instanceof Product;
                }
            
                public int hashCode() {
                    final int PRIME = 59;
                    int result = 1;
                    final Object $number = this.getNumber();
                    result = result * PRIME + ($number == null ? 43 : $number.hashCode());
                    final Object $name = this.getName();
                    result = result * PRIME + ($name == null ? 43 : $name.hashCode());
                    final Object $price = this.getPrice();
                    result = result * PRIME + ($price == null ? 43 : $price.hashCode());
                    final Object $stock = this.getStock();
                    result = result * PRIME + ($stock == null ? 43 : $stock.hashCode());
                    final Object $createdAt = this.getCreatedAt();
                    result = result * PRIME + ($createdAt == null ? 43 : $createdAt.hashCode());
                    final Object $updatedAt = this.getUpdatedAt();
                    result = result * PRIME + ($updatedAt == null ? 43 : $updatedAt.hashCode());
                    return result;
                }
            
                public String toString() {
                    return "Product(number=" + this.getNumber() + ", price=" + this.getPrice() + ", stock=" + this.getStock() + ", createdAt=" + this.getCreatedAt() + ", updatedAt=" + this.getUpdatedAt() + ")";
                }
            }
            ```
            
    - 다시 적용 상태로 되돌리기
        - command + z



<br>

### Lombok의 주요 어노테이션

`@Getter` , `@Setter`

- 클래스에 선언되어 있는 필드에 대한 getter/setter 메서드 생성
- Product 클래스에서 쓰인 @Getter, @Setter를 실제 코드로 추출한 결과
    
    ```java
    public Long getNumber() {
            return this.number;
        }
    
        public String getName() {
            return this.name;
        }
    
        public Integer getPrice() {
            return this.price;
        }
    
        public Integer getStock() {
            return this.stock;
        }
    
        public LocalDateTime getCreatedAt() {
            return this.createdAt;
        }
    
        public LocalDateTime getUpdatedAt() {
            return this.updatedAt;
        }
    
        public void setNumber(Long number) {
            this.number = number;
        }
    
        public void setName(String name) {
            this.name = name;
        }
    		
    		public void setPrice(Integer price) {
            this.price = price;
        }
    
        public void setStock(Integer stock) {
            this.stock = stock;
        }
    
        public void setCreatedAt(LocalDateTime createdAt) {
            this.createdAt = createdAt;
        }
    
        public void setUpdatedAt(LocalDateTime updatedAt) {
            this.updatedAt = updatedAt;
        }
    ```
    

`생성자 자동 생성 어노테이션`

- 데이터 클래스 초기화를 위한 생성자를 자동으로 만들어주는 어노테이션 3가지
    - `NoArgsConstructor`
        - 매개변수가 없는 생성자를 자동 생성
    - `AllArgsConstructor`
        - 모든 필드를 매개변수로 갖는 생성자를 자동 생성
    - `RequiredArgsConstructor`
        - 필드 중 final이나 @NotNull이 설정된 변수를 매개변수로 갖는 생성자를 자동 생성

- 현재 Product 클래스에는 @RequiredArgsConstructor로 정의될 필드가 없기 때문에 다른 두 개의 어노테이션을 Delombok해서 나온 코드
    
    ```java
    public Product(Long number, String name, Integer price, Integer stock, LocalDateTime createdAt, LocalDateTime updatedAt) {
    	this.number = number;
    	this.name = name;
    	this.price = price;
    	this.stock = stock;
    	this.createdAt = createdAt;
    	this.updatedAt = updatedAt;
    }
    
    public Product() {
    }
    ```
    

`@ToString`

- toString() 메서드를 생성하는 어노테이션
- Product 클래스에 @toString()을 적용해 Delombok 수행
    
    ```java
    public String toString() {
    	return "Product(number=" + this.getNumber() + ", name=" + this.getName() + ", price="
    		+ this.getPrice() + ", stock=" + this.getStock() + ", createdAt=" this.getCreatedAt()
    		+", updatedAt=" + this.getUpdatedAt() + ")";
    }
    ```
    

`@ToString 어노테이션의 exclude 속성 활용` 

- @ToString 어노테이션이 제공하는 exclude 속성을 사용해 특정 필드를 자동 생성에서 제외할 수 있음
    
    ```java
    @ToString(exclude = "name")
    @Table(name = "product")
    public class Product {
    ...(생략)
    }
    ```
    

`@EqualsAndHashCode`

- 객체의 동등성(Equality)과 동일성(Identity)을 비교하는 연산 메서드를 생성
- Product 클래스에 @EqualsAndHashCode 어노테이션을 적용한 후 Delombok을 수행
    - equals : 두 객체의 내용이 같은지 동등성을 비교
    - hashcode : 두 객체가 같은 객체인지 동일성을 비교
    
    ```java
    public boolean equals(final Object o) {
            if (o == this) return true;
            if (!(o instanceof Product)) return false;
            final Product other = (Product) o;
            if (!other.canEqual((Object) this)) return false;
            final Object this$number = this.getNumber();
            final Object other$number = other.getNumber();
            if (this$number == null ? other$number != null : !this$number.equals(other$number)) return false;
            final Object this$name = this.getName();
            final Object other$name = other.getName();
            if (this$name == null ? other$name != null : !this$name.equals(other$name)) return false;
            final Object this$price = this.getPrice();
            final Object other$price = other.getPrice();
            if (this$price == null ? other$price != null : !this$price.equals(other$price)) return false;
            final Object this$stock = this.getStock();
            final Object other$stock = other.getStock();
            if (this$stock == null ? other$stock != null : !this$stock.equals(other$stock)) return false;
            final Object this$createdAt = this.getCreatedAt();
            final Object other$createdAt = other.getCreatedAt();
            if (this$createdAt == null ? other$createdAt != null : !this$createdAt.equals(other$createdAt)) return false;
            final Object this$updatedAt = this.getUpdatedAt();
            final Object other$updatedAt = other.getUpdatedAt();
            if (this$updatedAt == null ? other$updatedAt != null : !this$updatedAt.equals(other$updatedAt)) return false;
            return true;
        }
    
        protected boolean canEqual(final Object other) {
            return other instanceof Product;
        }
    
        public int hashCode() {
            final int PRIME = 59;
            int result = 1;
            final Object $number = this.getNumber();
            result = result * PRIME + ($number == null ? 43 : $number.hashCode());
            final Object $name = this.getName();
            result = result * PRIME + ($name == null ? 43 : $name.hashCode());
            final Object $price = this.getPrice();
            result = result * PRIME + ($price == null ? 43 : $price.hashCode());
            final Object $stock = this.getStock();
            result = result * PRIME + ($stock == null ? 43 : $stock.hashCode());
            final Object $createdAt = this.getCreatedAt();
            result = result * PRIME + ($createdAt == null ? 43 : $createdAt.hashCode());
            final Object $updatedAt = this.getUpdatedAt();
            result = result * PRIME + ($updatedAt == null ? 43 : $updatedAt.hashCode());
            return result;
        }
    ```
    
    - 부모 클래스가 있어 상속을 받는 상황이라면?
        - 부모 클래스의 필드까지 비교할 필요가 있는 경우도 발생
        - @EqualsAndHashCode에서 제공하는 callSuper 속성 설정 시 부모 클래스의 필드를 비교 대상에 포함할 수 있음.
            - callSuper 기본값은 false, true일 경우 부모 객체의 값도 비교 대상에 포함
            
            ```java
            @Entity
            @EqualsAndHashCode(callSuper = true)
            @Table(name = "product")
            public class Product entends BaseEntity {
            	..(생략)
            }
            ```
            

`@Data`

- 앞의 @Getter, @Setter, @RequiredArgsConstructor, @ToString, @EqualsAndHashCode를 모두 포괄하는 어노테이션
- 각각의 어노테이션에서 생성하는 대부분의 코드가필요하다면 @Data 어노테이션으로 앞의 코드를 전부 한번에 생성 가능
