#SQL

### SQL이란
>SQL은 데이터베이스에 엑세스 하기 위한 표준언어이다. 

<br><br><br>



##  데이터 출력

`select` * `from` ***table_name***

***table_name*** 에 있는 모든(*) 데이터를 가져오라는 문장입니다.


<br>
##  조건에 맞는 모든 테이터 출력

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