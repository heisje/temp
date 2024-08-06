# Union과 Join

둘 다 데이터의 결합을 위한 것.

### Union은 수직(행+) 결합

수직으로 더하다보니, column이 같음 = 컬럼이 같은 테이블끼리 합친다.

### join은 수평(열+) 결합

수평으로 더하다보니, row가 같음 = row끼리 같은 것(외래키)을 더할 때 사용한다.

## 예시 데이터

### customers

<table><thead><tr><th>CID</th><th>CName</th><th>Country</th></tr></thead><tbody><tr><td>1</td><td>Alfreds</td><td>Germany</td></tr><tr><td>2</td><td>Centro</td><td>Mexico</td></tr><tr><td>3</td><td>Ernst</td><td>Austria</td></tr><tr><td>4</td><td>Island</td><td>UK</td></tr><tr><td>5</td><td>Laughing</td><td>Canada</td></tr></tbody></table>

### Orders

<table><thead><tr><th>OID</th><th>ODate</th><th>CID</th></tr></thead><tbody><tr><td>1</td><td>2023-01-15</td><td>1</td></tr><tr><td>2</td><td>2023-02-20</td><td>2</td></tr><tr><td>3</td><td>2023-03-25</td><td>3</td></tr><tr><td>4</td><td>2023-04-10</td><td>4</td></tr><tr><td>5</td><td>2023-05-05</td><td>1</td></tr><tr><td>6</td><td>2023-05-07</td><td>12</td></tr></tbody></table>

# Join

JOIN은 여러 테이블의 데이터를 수평으로 결합하여 하나의 결과 집합으로 만들어준다.

예시로는 물품코드를 판매코드와 조인해서 물품이름을 구할 때 쓸 수 있다.

조인의 종류는 INNER, LEFT, RIGHT, FULL이 있다.

### JOIN 이해하기

문법 : 처음 보면 어렵다.

```sql
SELECT *
FROM Customers
LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```

조인을 검색해보면 다음과 같은 이미지를 만난다.
FROM의 TABLE이 왼쪽이고, JOIN의 TABLE이 오른쪽이라고 생각하면 이해하기 쉽다. OUTER 키워드는 생략가능

![alt text](image-1.png)
그래서 LEFT OUTER JOIN의 위 쿼리의 경우, 같은 값이 없더라도 A의 값을 출력하며, B는 NULL로 나온다.

### Inner

같은 값이 있는 경우만 출력한다.
![alt text](image.png)

```sql
-- INNER
SELECT *
FROM Customers
INNER JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```

![alt text](image-3.png)

### LEFT

왼쪽을 기준으로 출력한다. (오른쪽에 같은 값이 없더라도 출력)

```sql
-- LEFT
SELECT *
FROM Customers
LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```

![alt text](image-4.png)

### RIGHT

오른쪽을 기준으로 출력한다. (왼쪽에 같은 값이 없더라도 출력)

```sql
-- RIGHT
SELECT *
FROM Customers
RIGHT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```

![alt text](image-5.png)

### FULL

양쪽을 기준으로 출력한다. (양쪽에 같은 값이 없더라도 출력)

```sql
-- FULL
SELECT *
FROM Customers
FULL JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```

![alt text](image-6.png)

### CROSS

모든 경우의 수 곱. 카타시안 곱이 일어난다.
(왼쪽 테이블 행수 x 오른쪽 테이블 행 수)

```sql
-- CROSS
SELECT *
FROM Customers
CROSS JOIN Orders;
```

...

# Union

여러 쿼리문들을 합쳐서 하나의 쿼리문으로 만들어주는 방법이다.
중복된 값을 제거하고 보여준다.

중복된 값을 제거하는 연산이 추가로 수행되기 때문에 UNION ALL보다 속도가 느리다.

### Union All

UNION과 동일하게 여러 쿼리문들을 합쳐서 하나의 쿼리문으로 만들어주는 방법이다.
중복된 값을 모두 보여준다.

### 사용방법

-   컬럼명이 동일해야 한다. (같지 않을 경우 AS 를 이용해서 동일하게 맞춰줘야 한다.)
-   컬럼별로 데이터 타입이 동일해야 한다.
-   출력할 컬럼의 개수가 동일해야 한다.
-   출력할 컬럼명을 차례로 적고, 알리어스(AS) 를 통해 컬럼명을 동일하게 맞춰준다.

```sql
SELECT A AS one, B AS two
FROM TABLE_A
UNION (또는 UNION ALL)
SELECT C AS one, D AS two
FROM TABLE_B
;
```

### 사용 용도:

"재작년 성적과 작년 성적과 이번 성적을 합친 테이블 만들기."
처럼 열이 같은 데이터가 좋다.
