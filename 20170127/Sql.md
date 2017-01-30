#SQL

### SQL이란
>SQL은 데이터베이스에 엑세스 하기 위한 표준언어이다. 

<br><br><br>



##  데이터 검색

`select` * `from` ***table_name***

***table_name*** 에 있는 모든(*) 데이터를 가져오라는 문장입니다.


<br>
##  조건에 맞는 테이터 검색

### 1. where 조건문
`select` * `from` ***table_name***  `where` **조건**
  
>예)`SELECT * FROM Customers WHERE Country='Mexico';`  
> "Customers" 테이블에 있는 "Country" 컬럼에 값이 "Mexico"와 같은 모든 데이터를 가져 온다.  

<br>
### 2. and 조건문

`select` * `from` ***table_name*** `where` **조건1** `and`  **조건2**  

>조건1과 조건2가 모두 충족하는 데이터를 가져 옵니다. 

>예)`SELECT * FROM Customers WHERE Country='Mexico' and Country='Berlin';`
>"Customers" 테이블에 있는 "Country" 컬럼에 값이 "Mexico"와 "Berlin"을 모두 만족하는 데이터를 가져 온다.
 
<br>
### 2. or 조건문

`select` * `from` ***table_name*** `where` **조건1** `or`  **조건2**  

>조건1과 조건2가 두 조건 중 한가지 이상 충족하는 데이터를 가져 옵니다. 

>예)`SELECT * FROM Customers WHERE Country='Mexico' or Country='Berlin';`
>"Customers" 테이블에 있는 "Country" 컬럼에 값이 "Mexico"와 "Berlin" 두가지 조건 중 한가 이상 만족하는 데이터를 가져 온다.


<br>
### 3. ORDER BY 조건문
* 하나 이상의 열을 기준으로 결과 집합을 정렬합니다. 
기본적으로 **오름차순**으로 정렬합니다.

>기본문장  

`SELECT` * `FROM` Customers `ORDER BY` Country;  

`SELECT` * `FROM` Customers `ORDER BY` Country `DESC`;

>응용문장

`SELECT` * `FROM` Customers `ORDER BY` Country, CustomerName;  
 
`SELECT` * `FROM` Customers `ORDER BY` Country `ASC`, CustomerName `DESC`;

<br>
### 4. LIKE 구문
* 열에 포한된 패턴을 검색합니다.  

> 기본문장  

`SELECT` column_name(s)
`FROM` table_name
`WHERE` column_name `LIKE` pattern;
> 응용문장  

`SELECT` * `FROM` Customers `WHERE` City `LIKE` `'s%'`;  
* 문자 "s"로 시작하는 모든  Customers을 선택합니다.
  
`SELECT` * `FROM` Customers `WHERE` City `LIKE` `'%s'`;  
* 문자 "s"로 끝나는 모든 Customers을 선택합니다.

<br>
### 5. BETWEEN 구문
* 연산자는 범위 내의 값을 선택합니다. 값은 숫자, 텍스트 또는 날짜 일 수 있습니다.  

> 기본문장  

`SELECT` column_name(s)
`FROM` table_name
`WHERE` column_name `BETWEEN` value1 `AND` value2;
> 응용문장  

`SELECT` * `FROM` Orders
`WHERE` OrderDate `BETWEEN` #07/04/1996# `AND` #07/09/1996#;    
* 7/04/1996 과  07/09/1996 주문을 선택합니다.

<br>
### 6. 별칭 구문
* 별칭은 데이터베이스 테이블이나 테이블의 열에 **임시 이름**을 제공하는 데 사용됩니다.  

> 기본문장  

`SELECT` column_name `AS` **alias_name** `FROM` table_name;


<br>
### 7. JOIN 구문
* SQL JOIN 절은 두 개 이상의 테이블의 행을 공통 필드를 기준으로 결합하는 데 사용됩니다.  

> 기본문장  

`SELECT` Orders.OrderID, Customers.CustomerName, Orders.OrderDate  
`FROM` Orders  
`INNER JOIN` Customers  
`ON` Orders.CustomerID=Customers.CustomerID;

>각자 다른 Orders 테이블과  Customers 테이블에서  두테이블의 CustomerID 가 일치하는 데이터를 검색한다. 


<br><br>
## 데이터 입력

* 컬럼을 지정하고 입력하는 방법과 지정하지 않고 입력하는 두가지 방법이 있음

>기본문`.1`  

`INSERT INTO` table_name `VALUES` (value1,value2,value3,...);  

>기본문`.2` 

`INSERT INTO` table_name (column1,column2,column3,...)
`VALUES` (value1,value2,value3,...);

<br><br>
## 데이터 수정
`UPDATE` table_name
`SET` column1=value1,column2=value2,...
`WHERE` some_column=some_value;

>**SQL UPDATE 문의 WHERE 절을 주목하십시오! 
WHERE 절은 갱신해야하는 레코드를 지정합니다.   
WHERE 절을 생략하면 모든 레코드가 업데이트됩니다!**



<br><br>
## 데이터 삭제
* DELETE 문은 테이블의 행을 삭제하는 데 사용됩니다.

`DELETE FROM` table_name
`WHERE` some_column=some_value;

>**SQL DELETE 문의 WHERE 절을 주목하십시오! 
WHERE 절은 제될 레코드를 지정합니다.  
WHERE 절을 생략하면 모든 레코드가 삭제됩니다!**


<br><br>
## 데이터베이스 생성 (DATABASE CREATE)
* CREATE DATABASE 문은 데이터베이스를 만드는 데 사용됩니다.

`CREATE DATABASE` my_db;  
> "my_db"라는 데이터베이스를 생성합니다.  


<br><br>
## 테이블 생성 (TABLE CREATE)
* CREATE DATABASE 문은 데이터베이스를 만드는 데 사용됩니다.

> 기본문장  

`CREATE TABLE` table_name  
(  
column_name1 data_type(size),  
column_name2 data_type(size),  
column_name3 data_type(size),  
....  
);   

> 응용문장
 
`CREATE TABLE` Persons  
(  
PersonID int,  
LastName varchar(255),  
FirstName varchar(255),  
Address varchar(255),  
City varchar(255)  
);  

**LastName**, **FirstName**, **Address** 및 **City** 열은 varchar 유형이며 문자를 포함하며이 필드의 최대 길이는 255 자입니다.

<br>
### 1. NOT NULL Constraint
* 열이 NULL 값을 허용하지 않도록합니다.  

> 예제문장  

`CREATE TABLE` PersonsNotNull  
(   
P_Id int `NOT NULL`,  
LastName varchar(255) `NOT NULL`,  
FirstName varchar(255),  
Address varchar(255),  
City varchar(255)  
)  

> NOT NULL이 설정된 열은 새 레코드를 삽입하거나이 필드에 값을 추가하지 않고 레코드를 업데이트 할 수 없습니다. 빈값이면 안됨.