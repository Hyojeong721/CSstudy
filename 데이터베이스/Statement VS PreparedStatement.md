# Statement VS PreparedStatement

 *Statement* 와 *PreparedStatement* 모두 SQL 쿼리를 실행하는 데 사용한다.

**PreparedStatement 와 Statement의 가장 큰 차이점**은 캐시(cache) 사용여부이다.

1) 쿼리 문장 분석
2) 컴파일
3)  실행



Statement를 사용하면 매번 쿼리를 수행할 때마다 1) ~ 3) 단계를 거치게 되고, 

PreparedStatement는 처음 한 번만 세 단계를 거친 후 캐시에 담아 재사용을 한다는 것이다. 

만약 동일한 쿼리를 반복적으로 수행한다면 PreparedStatment가 DB에 훨씬 적은 부하를 주며, 성능도 좋다.

<hr>

#### Statement

DB를 연결하기 위한 일반적인 목적으로 사용된다.

고정적인 쿼리를 실행할때 유용하며 매개변수를 받을 수 없다.

SQL문이 달라지더라도 한개만 생성해서 재사용이 가능하다.



```
Statement stmt = conn.createStatement(); // 생성
stmt.execute(sql); //실행
```



#### PreparedStatement

쿼리를 자주 사용할 때 이용된다. 

실행시간에 매개변수를 받을 수 있다.

Statement에 비해 반복적인 SQL문을 사용할 경우 더 빠르다. 

DB컬럼타입과 관계없이 하나로 표시하면 되기 때문에 개발자가 혼동하지 않고 사용가능하며

SQL문마다 PreparedStatement객체를 각각 생성해야 하기 때문에 재사용이 불가능하다.



```
PreparedStatement pstmt = conn.prepareStatement(sql); // 생성
pstmt.execute(); // 실행
```



<hr>

##### Statement를 반드시 사용해야 하는 경우

1. Dynamic SQL을 사용할 경우

Dynamic SQL을 사용한다면 매번 조건절이 달라지기 때문에 Statement가 더 낫다! + 코딩도 훨씬 편함.



##### 참고 ( Static SQL / Dynamic SQL )

`Static SQL`이란, String형 변수(값)를 담지않고 코드 사이에 직접 기술한 SQL문을 말한다.
다른 말로 'Embedded SQL', 

아래 예시처럼 SQL문을 String 변수에 담지 않고 마치 예약된 키워드처럼 C/C++코드 사이에 섞어서 기술하고 있다. Static SQL이든 Dynamic SQL이든 PreCompile 단계를 거치고 나면 String 변수에 담기기는 마찬가지지만 Static SQL은 런타임시에 절대 변하지 않으므로 PreCompile 단계에서 구문 분석, 유효 오브젝트 여부, 오브젝트 액세스 권한 등을 체크하는 것이 가능하다.

```
Init main()
\{
	Printf("사번입력하셈:");
	Scanf("%d", &empno);
	EXEC SQL WHENEVER NOT FOUND GOTO notfound;
	EXEC SQL SELECT ENAME INTO : ename
				FROM EMP
				WHERE EMPNO = :	empno;
  	Printf("사원명 : %s.\n", name);
Notfound:
	Printf("%d는 존재하지 않는 사번입니다.\n", empno);
\}

```

`Dynamic SQL`이란 String형 변수에 담아서 기술하는 SQL문을 말한다.
String 변수를 사용하므로 조건에 따라 SQL문을 동적으로 바꿀 수 있고, 
런타임 시에 사용자로부터 SQL문의 일부 또는 전부를 입력받아서 실행할 수도 있다.
따라서 preCompile 시 systax, semantics 체크가 불가능하다.



<hr>



출처: https://devbox.tistory.com/entry/Comporison [장인개발자를 꿈꾸는 :: 기록하는 공간:티스토리]

출처 : https://blog.daum.net/ipajama/133 [Static SQL / Dynamic SQL ]









## 2. JDBC API 인터페이스

 *Statement* 와 *PreparedStatement* 모두 SQL 쿼리를 실행하는 데 사용할 수 있습니다. 이러한 인터페이스는 매우 유사해 보입니다. 그러나 기능 및 성능면에서 서로 크게 다릅니다. 

- *명령문* – **문자열 기반 SQL** **쿼리 를 실행하는 데 사용됩니다.**
- *PreparedStatement* – **매개변수화된 SQL 쿼리를 실행하는 데 사용됩니다.**

예제에서 *Statement* 및 *PreparedStatement* 를 사용할 수 있도록 *pom.xml* 파일 에서 *h2* JDBC 커넥터를 종속성으로 선언 합니다.

```xml
<dependency>
  <groupId>com.h2database</groupId>
  <artifactId>h2</artifactId>
  <version>1.4.200</version>
</dependency>
```

이 문서 전체에서 사용할 엔터티를 정의해 보겠습니다.

```java
public class PersonEntity {
    private int id;
    private String name;

    // standard setters and getters
}
```

## 3. Statement

첫째, *Statement* 인터페이스 는 문자열을 SQL 쿼리로 받아들입니다. 따라서 SQL 문자열 을 연결할 때 **코드 가독성이 떨어집니다 .**

```java
public void insert(PersonEntity personEntity) {
    String query = "INSERT INTO persons(id, name) VALUES(" + personEntity.getId() + ", '"
      + personEntity.getName() + "')";

    Statement statement = connection.createStatement();
    statement.executeUpdate(query);
}
```

둘째, **[SQL 인젝션](https://www.baeldung.com/cs/sql-injection)** **에 취약하다** . 다음 예는 이러한 약점을 보여줍니다.

첫 번째 줄에서 업데이트는 모든 행의 " *name " 열을 "* *hacker* "로 설정합니다. "—" 이후의 모든 항목은 SQL에서 주석으로 해석되고 업데이트 문의 조건은 무시됩니다. *두 번째 줄에서 " name* " 열의 따옴표가 이스케이프 처리되지 않았기 때문에 삽입이 실패합니다 .

```java
dao.update(new PersonEntity(1, "hacker' --"));
dao.insert(new PersonEntity(1, "O'Brien"))
```

셋째, **JDBC는 인라인 값이 있는 쿼리를 데이터베이스에 전달합니다** . 따라서 쿼리 최적화가 없으며 가장 중요한 것은 **데이터베이스 엔진이 모든 검사를 보장해야 한다는 것** 입니다. 또한 쿼리는 데이터베이스에 동일하게 표시되지 않으며 **캐시 사용을 방지합니다** . 마찬가지로 일괄 업데이트는 별도로 실행해야 합니다.

```java
public void insert(List<PersonEntity> personEntities) {
    for (PersonEntity personEntity: personEntities) {
        insert(personEntity);
    }
}
```

넷째, **Statement** ***인터페이스\* 는 CREATE , ALTER 및 DROP 과 같은 DDL 쿼리 에 적합합니다** .

```java
public void createTables() {
    String query = "create table if not exists PERSONS (ID INT, NAME VARCHAR(45))";
    connection.createStatement().executeUpdate(query);
}
```

마지막으로 **Statement** ***인터페이스\*** **는 파일과 배열을 저장하고 검색하는 데 사용할 수 없습니다** .





## 4. *PreparedStatement*

첫째, *PreparedStatement* *는 Statement* 인터페이스를 확장합니다 . 파일 및 배열을 포함하여 **다양한 개체 유형을 바인딩하는 메서드가 있습니다.** 따라서 **코드** **를 이해하기 쉬워** 집니다 .

```java
public void insert(PersonEntity personEntity) {
    String query = "INSERT INTO persons(id, name) VALUES( ?, ?)";

    PreparedStatement preparedStatement = connection.prepareStatement(query);
    preparedStatement.setInt(1, personEntity.getId());
    preparedStatement.setString(2, personEntity.getName());
    preparedStatement.executeUpdate();
}
```

둘째, 제공된 모든 매개변수 값에 대한 텍스트를 이스케이프 처리하여 **SQL 주입으로부터 보호합니다 .**

```java
@Test 
void whenInsertAPersonWithQuoteInText_thenItNeverThrowsAnException() {
    assertDoesNotThrow(() -> dao.insert(new PersonEntity(1, "O'Brien")));
}

@Test 
void whenAHackerUpdateAPerson_thenItUpdatesTheTargetedPerson() throws SQLException {

    dao.insert(Arrays.asList(new PersonEntity(1, "john"), new PersonEntity(2, "skeet")));
    dao.update(new PersonEntity(1, "hacker' --"));

    List<PersonEntity> result = dao.getAll();
    assertEquals(Arrays.asList(
      new PersonEntity(1, "hacker' --"), 
      new PersonEntity(2, "skeet")), result);
}
```

셋째, ***PreparedStatement\*** **는 사전 컴파일을 사용** 합니다. 데이터베이스는 쿼리를 받자마자 쿼리를 미리 컴파일하기 전에 캐시를 확인합니다. 따라서 **캐시되지 않은 경우 데이터베이스 엔진은 다음 사용을 위해 이를 저장합니다.**

또한 이 기능 은 SQL이 아닌 바이너리 프로토콜을 통해 **데이터베이스와 JVM 간의 통신 속도를 높 입니다.** 즉, 패킷에 데이터가 적으므로 서버 간의 통신이 더 빨라집니다.

넷째, ***PreparedStatement\*** **는 단일 데이터베이스 연결 동안 [일괄](https://www.baeldung.com/jdbc-batch-processing)** 실행을 제공합니다 . 이것을 실제로 봅시다:

```java
public void insert(List<PersonEntity> personEntities) throws SQLException {
    String query = "INSERT INTO persons(id, name) VALUES( ?, ?)";
    PreparedStatement preparedStatement = connection.prepareStatement(query);
    for (PersonEntity personEntity: personEntities) {
        preparedStatement.setInt(1, personEntity.getId());
        preparedStatement.setString(2, personEntity.getName());
        preparedStatement.addBatch();
    }
    preparedStatement.executeBatch();
}
```

다음으로, ***PreparedStatement\*** ***는 BLOB\*** **및** ***CLOB\*** **데이터 유형** **을 사용하여 파일을 저장하고 검색하는 쉬운 방법을 제공합니다** . 같은 맥락에서 *java.sql.Array* 를 SQL Array로 변환하여 목록을 저장하는 데 도움이 됩니다.

마지막으로 *PreparedStatement* 는 반환된 결과에 대한 정보를 포함하는 *getMetadata()* 와 같은 메서드를 구현합니다 .

## 5. 결론

*이 자습서에서는 PreparedStatement* 와 *Statement* 의 주요 차이점을 제시했습니다 . 두 인터페이스 모두 SQL 쿼리를 실행하는 메서드를 제공하지만 DDL 쿼리 에는 *Statement 를 사용하고 DML 쿼리에는* *PreparedStatement* 를 사용하는 것이 더 적합 합니다.





<hr>

출처 : https://www.baeldung.com/java-statement-preparedstatement

