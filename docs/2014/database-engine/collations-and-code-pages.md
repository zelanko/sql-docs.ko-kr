---
title: 데이터 정렬 및 코드 페이지 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c626dcac-0474-432d-acc0-cfa643345372
author: stevestein
ms.author: sstein
ms.openlocfilehash: 96eea051fbf4a34257d61ff8eaf4f796debf49a6
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936014"
---
# <a name="collations-and-code-pages"></a>데이터 정렬 및 코드 페이지
  [!INCLUDE[hek_2](../includes/hek-2-md.md)]에는 메모리 최적화 테이블의 (var)char 열에 대해 지원되는 코드 페이지와 인덱스 및 고유하게 컴파일된 저장 프로시저에 사용되는 지원되는 데이터 정렬에 대한 제한 사항이 있습니다.  
  
 (var)char 값에 대한 코드 페이지는 테이블에 저장되는 문자와 바이트 표현 간의 매핑을 결정합니다. 예를 들어 Windows 라틴어 1 코드 페이지(1252, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 기본값)를 사용하는 경우 문자 'a'는 바이트 0x61에 해당합니다.  
  
 (var)char 값의 코드 페이지는 값과 연결된 데이터 정렬에 의해 결정됩니다. 예를 들어 데이터 정렬 SQL_Latin1_General_CP1_CI_AS에는 연결된 코드 페이지 1252가 있습니다.  
  
 값의 데이터 정렬은 데이터베이스 데이터 정렬에서 상속되거나, COLLATE 키워드를 사용하여 명시적으로 지정할 수 있습니다. 메모리 최적화 테이블이나 고유하게 컴파일된 저장 프로시저가 데이터베이스에 포함되어 있는 경우에는 데이터베이스 데이터 정렬을 변경할 수 없습니다. 다음 예에서는 데이터베이스 데이터 정렬을 설정하고 다른 데이터 정렬이 있는 열을 포함하는 테이블을 만듭니다. 데이터베이스에서 대/소문자를 구분하지 않는 라틴어 데이터 정렬을 사용합니다.  
  
 인덱스가 BIN2 데이터 정렬을 사용하는 경우 문자열 열에 대해서만 인덱스를 만들 수 있습니다. LastName 변수는 BIN2 데이터 정렬을 사용합니다. FirstName은 데이터베이스 기본값인 CI_AS(대/소문자 구분 안 함, 악센트 구분)를 사용합니다.  
  
> [!IMPORTANT]  
>  BIN2 데이터 정렬을 사용하지 않는 인덱스 문자열 열에 대해서는 ORDER BY 또는 GROUP BY를 사용할 수 없습니다.  
  
```sql  
CREATE DATABASE IMOLTP  
  
ALTER DATABASE IMOLTP ADD FILEGROUP IMOLTP_mod CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE IMOLTP ADD FILE( NAME = 'IMOLTP_mod' , FILENAME = 'c:\data\IMOLTP_mod') TO FILEGROUP IMOLTP_mod;  
--GO  
  
--  set the database collations  
ALTER DATABASE IMOLTP COLLATE Latin1_General_100_CI_AS  
GO  
  
--  
USE IMOLTP   
GO  
  
-- create a table with collation  
CREATE TABLE Employees (  
  EmployeeID int NOT NULL ,   
  LastName nvarchar(20) COLLATE Latin1_General_100_BIN2 NOT NULL INDEX IX_LastName NONCLUSTERED,   
  FirstName nvarchar(10) NOT NULL ,  
  CONSTRAINT PK_Employees PRIMARY KEY NONCLUSTERED HASH(EmployeeID)  WITH (BUCKET_COUNT=1024)  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY=SCHEMA_AND_DATA)  
GO  
```  
  
 다음 제한 사항은 메모리 최적화 테이블과 고유하게 컴파일된 저장 프로시저에 적용됩니다.  
  
-   메모리 최적화 테이블의 (var)char 열은 코드 페이지 1252와 데이터 정렬을 사용해야 합니다. n(var)char 열에는 이 제한 사항이 적용되지 않습니다. 다음 코드는 모든 1252 데이터 정렬을 검색합니다.  
  
    ```sql  
    -- all supported collations for (var)char columns in memory-optimized tables  
    select * from sys.fn_helpcollations()  
    where collationproperty(name, 'codepage') = 1252;  
    ```  
  
     라틴어가 아닌 문자를 저장해야 하는 경우 n(var)char 열을 사용합니다.  
  
-   (n)(var)char 열의 인덱스는 BIN2 데이터 정렬만 사용하여 지정할 수 있습니다(첫 번째 예 참조). 다음 쿼리는 지원되는 모든 BIN2 데이터 정렬을 검색합니다.  
  
    ```sql  
    -- all supported collations for indexes on memory-optimized tables and   
    -- comparison/sorting in natively compiled stored procedures  
    select * from sys.fn_helpcollations() where name like '%BIN2'  
    ```  
  
     해석된 [!INCLUDE[tsql](../includes/tsql-md.md)]을 통해 테이블에 액세스하는 경우 `COLLATE` 키워드를 사용하여 식 또는 정렬 작업과 연결된 데이터 정렬을 변경할 수 있습니다. 이 작업의 예제를 보려면 마지막 예를 참조하십시오.  
  
-   데이터베이스 데이터 정렬이 코드 페이지 1252 데이터 정렬이 아닌 경우 고유하게 컴파일된 저장 프로시저는 (var)char 형식의 매개 변수, 지역 변수, 또는 문자열 상수를 사용할 수 없습니다.  
  
-   고유하게 컴파일된 저장 프로시저 내의 모든 식과 정렬 작업은 BIN2 데이터 정렬을 사용해야 합니다. 즉, 모든 비교 및 정렬 작업이 문자(이진 표현)의 유니코드 코드 포인트를 기반으로 합니다. 예를 들어 모든 정렬이 대/소문자를 구분합니다('Z'가 'a' 앞에 옴). 필요한 경우 대/소문자를 구분하지 않는 정렬 및 비교를 위해 해석된 [!INCLUDE[tsql](../includes/tsql-md.md)]을 사용합니다.  
  
-   UTF-16 데이터의 잘림은 고유하게 컴파일된 저장 프로시저에서 지원되지 않습니다. 즉, 데이터 정렬에 _SC 속성이 있는 경우 n (var) char (*n*) 값 *을 n (* var) char (*i*) 형식으로 변환할 수 없습니다  <  *n*. 예를 들어 다음은 지원되지 않습니다.  
  
    ```sql  
    -- column definition using an _SC collation  
     c2 nvarchar(200) collate Latin1_General_100_CS_AS_SC not null   
    -- assignment to a smaller variable, requiring truncation  
     declare @c2 nvarchar(100) = '';  
     select @c2 = c2  
    ```  
  
     UTF-16 데이터의 LEN, SUBSTRING, LTRIM 및 RTRIM과 같은 문자열 조작 함수는 고유하게 컴파일된 저장 프로시저 내에서 지원되지 않습니다. 이러한 문자열 조작 함수는 _SC 데이터 정렬이 있는 n(var)char 값에 사용할 수 없습니다.  
  
     충분히 커서 잘림을 방지할 수 있는 형식을 사용하여 변수를 선언합니다.  
  
 다음 예에서는 메모리 내 OLTP의 데이터 정렬 제한 사항이 의미하는 것과 그 해결 방법을 몇 가지 보여 줍니다. 이 예에서는 위에 지정된 Employees 테이블을 사용하여 이 샘플은 모든 직원을 나열 합니다. LastName의 경우 이진 데이터 정렬로 인해 대문자 이름이 소문자 앞에 정렬됩니다. 따라서 대문자에 더 낮은 코드 포인트가 있기 때문에 'Thomas'가 'nolan' 앞에 옵니다. FirstName의 데이터 정렬은 대/소문자를 구분하지 않습니다. 따라서 문자의 코드 포인트가 아니라 영문자 순으로 정렬됩니다.  
  
```sql  
-- insert a number of values  
INSERT Employees VALUES (1,'thomas', 'john')  
INSERT Employees VALUES (2,'Thomas', 'rupert')  
INSERT Employees VALUES (3,'Thomas', 'Jack')  
INSERT Employees VALUES (4,'Thomas', 'annie')  
INSERT Employees VALUES (5,'nolan', 'John')  
GO  
  
-- ===========  
SELECT EmployeeID, LastName, FirstName FROM Employees  
ORDER BY LastName, FirstName  
GO  
  
-- ===========  
-- specify collation: sorting uses case-insensitive collation, thus 'nolan' comes before 'Thomas'  
SELECT * FROM Employees  
ORDER BY LastName COLLATE Latin1_General_100_CI_AS, FirstName  
GO  
  
-- ===========  
-- retrieve employee by Name  
-- must use BIN2 collation for comparison in natively compiled stored procedures  
CREATE PROCEDURE usp_EmployeeByName @LastName nvarchar(20), @FirstName nvarchar(10)  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH   
(  TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
  LANGUAGE = N'us_english'  
)  
  SELECT EmployeeID, LastName, FirstName FROM dbo.Employees  
  WHERE   
    LastName = @LastName AND  
    FirstName COLLATE Latin1_General_100_BIN2 = @FirstName  
  
END  
GO  
  
-- this does not return any rows, as EmployeeID 1 has first name 'john', which is not equal to 'John' in a binary collation  
EXEC usp_EmployeeByName 'thomas', 'John'  
  
-- this retrieves EmployeeID 1  
EXEC usp_EmployeeByName 'thomas', 'john'  
```  
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
