---
title: SQL 삽입 | Microsoft 문서
description: SQL 삽입 공격의 작동 방식에 대해 알아봅니다. SQL Server에서 입력의 유효성을 검사하고 SQL 삽입 코드를 검토하여 이러한 공격을 완화합니다.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: security, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- SQL Injection
ms.assetid: eb507065-ac58-4f18-8601-e5b7f44213ab
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ea1d2300b2ff2431d58b8fb2d6139ecad130a965
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97432421"
---
# <a name="sql-injection"></a>SQL 삽입
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  SQL 삽입은 구문 분석 및 실행을 위해 나중에 SQL Server의 인스턴스로 전달된 문자열에 악성 코드를 삽입한 공격입니다. SQL Server는 구문상 유효한 모든 수신 쿼리를 실행하므로 SQL 문을 생성하는 모든 프로시저에 삽입과 관련한 취약성이 있는지 확인해야 합니다. 매개 변수가 있는 데이터도 숙련된 전문 공격자에 의해 조작될 수 있습니다.  
  
## <a name="how-sql-injection-works"></a>SQL 삽입의 작동 방식  
 기본적으로 SQL 삽입에서는 SQL 명령과 연결되어 실행되는 사용자 입력 변수에 코드를 직접 삽입합니다. 간접적인 공격에서는 테이블에 스토리지할 문자열에 또는 메타데이터로 악의적인 코드를 주입합니다. 이후에 저장된 문자열이 동적 SQL 명령에 연결되고 악성 코드가 실행됩니다.  
  
 삽입 프로세스는 텍스트 문자열을 미리 종료하고 새 명령을 덧붙이는 방법으로 수행됩니다. 삽입된 명령에는 실행 전에 덧붙여진 추가 문자열이 있을 수 있으므로 공격자는 주입된 문자열을 주석 표시인 "--"으로 종료합니다. 실행 시 이후 텍스트는 무시됩니다.  
  
 다음 스크립트에서는 간단한 SQL 삽입을 보여 줍니다. 이 스크립트는 하드 코딩된 문자열과 사용자가 입력한 문자열을 연결하여 SQL 쿼리를 만듭니다.  
  
```csharp
var Shipcity;  
ShipCity = Request.form ("ShipCity");  
var sql = "select * from OrdersTable where ShipCity = '" + ShipCity + "'";  
```  
  
 사용자에게 도시 이름의 입력을 요청하는 프롬프트가 표시됩니다. `Redmond`를 입력할 경우 이 쿼리는 다음과 유사한 스크립트로 조합됩니다.  
  
```sql
SELECT * FROM OrdersTable WHERE ShipCity = 'Redmond'  
```  
  
 그러나 사용자가 다음을 입력했다고 가정해 봅니다.  
  
```sql
Redmond'; drop table OrdersTable--  
```  
  
 이 경우 스크립트로 조합된 쿼리는 다음과 같습니다.  
  
```sql
SELECT * FROM OrdersTable WHERE ShipCity = 'Redmond';drop table OrdersTable--'  
```  
  
 세미콜론(;)은 한 쿼리의 끝과 다른 쿼리의 시작을 나타냅니다. 또한 이중 하이픈(--)은 현재 줄의 나머지 부분이 주석이므로 무시해야 함을 나타냅니다. 수정된 코드가 구문상 정확할 경우 이 코드는 서버에서 실행될 것입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 이 문을 처리할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 먼저 `OrdersTable` 에서 `ShipCity` 가 `Redmond`인 레코드를 모두 선택합니다. 그런 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 `OrdersTable`을 삭제합니다.  
  
 삽입된 SQL 코드가 구문상 정확하기만 하면 프로그래밍 방식으로 변조를 감지할 수 없습니다. 따라서 모든 사용자 입력의 유효성을 검사하고 생성된 SQL 명령을 사용 중인 서버에서 실행하는 코드를 주의 깊게 검토해야 합니다. 이 항목의 다음 섹션에서는 가장 적절한 일부 코딩 방법을 설명합니다.  
  
## <a name="validate-all-input"></a>모든 입력에 대한 유효성 검사  
 형식, 길이, 서식 및 범위를 테스트하여 항상 사용자 입력의 유효성을 검사합니다. 악의적인 입력을 사전에 막는 방법을 구현할 때는 애플리케이션의 아키텍처 및 배포 시나리오를 고려하십시오. 보안 환경에서 실행하도록 설계된 프로그램을 비보안 환경으로 복사할 수도 있습니다. 가장 적절한 방법을 구현하려면 다음 제안 사항을 고려해야 합니다.  
  
-   애플리케이션이 수신한 데이터의 크기, 형식 또는 내용을 정확히 합니다. 예를 들어 다음과 같은 사항을 평가해야 합니다.  
  
    -   잘못된 또는 악의적인 사용자가 애플리케이션의 우편 번호 입력 위치에 10MB의 MPEG 파일을 입력할 경우 애플리케이션의 작동 방법  
  
    -   텍스트 필드에 `DROP TABLE` 문을 포함하는 경우 애플리케이션의 작동 방법  
  
-   입력의 크기 및 데이터 형식을 테스트하고 적합한 제한 조치를 수행합니다. 그러면 의도적인 버퍼 오버런을 방지할 수 있습니다.  
  
-   문자열 변수의 내용을 테스트하고 예상 값만 허용합니다. 이진 데이터, 이스케이프 시퀀스 및 주석 문자를 포함하는 항목은 거부합니다. 그러면 스크립트 삽입을 방지하고 일부 악의적인 버퍼 오버런으로부터 보호할 수 있습니다.  
  
-   XML 문서 작업에서는 입력한 스키마에 대해 모든 데이터의 유효성을 검사합니다.  
  
-   사용자 입력에서 직접 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 만들지 않습니다.  
  
-   저장 프로시저를 사용하여 사용자 입력의 유효성을 검사합니다.  
  
-   다중 계층 환경에서는 신뢰할 수 있는 영역으로 들어가기 전에 모든 데이터의 유효성을 검사해야 합니다. 유효성 검사 프로세스를 통과하지 못한 데이터를 거부하고 이전 계층으로 오류를 반환해야 합니다.  
  
-   여러 계층의 유효성 검사를 구현합니다. 보통 수준의 악의적인 사용자에 대한 예방 조치는 전문 공격자에 대해서는 효과적이지 못할 수도 있습니다. 가장 적절한 방법은 사용자 인터페이스에서 입력의 유효성을 검사한 후 신뢰 경계를 넘는 모든 후속 지점에서 유효성을 검사하는 것입니다.   
    예를 들어 클라이언트 쪽 애플리케이션에서의 데이터 유효성 검사는 단순한 스크립트 삽입을 방지할 수 있지만 다음 계층에서 이 입력에 대해 유효성 검사가 이미 수행되었다고 가정하게 되면 클라이언트를 통과할 수 있는 악의적인 사용자가 시스템에 무제한으로 액세스할 수 있게 됩니다.  
  
-   유효성 검사를 수행하지 않은 사용자 입력을 연결하지 않습니다. 문자열 연결은 스크립트 삽입이 발생하는 주요 진입점입니다.  
  
-   파일 이름을 생성하는 데 사용될 수 있는 필드에는 AUX, CLOCK$, COM1~COM8, CON, CONFIG$, LPT1~LPT8, NUL, PRN과 같은 문자열을 허용하지 않습니다.  
  
 가능한 경우 다음 문자가 포함된 입력을 거부합니다.  
  
|입력 문자|Transact-SQL에서의 의미|  
|---------------------|------------------------------|  
|**;**|쿼리 구분 기호|  
|**'**|문자 데이터 문자열 구분 기호|  
|**--**|문자 데이터 문자열 구분 기호<br />.|  
|**/\**_ ... _*\*/**|주석 구분 기호. **/\* *_와 _* \*/** 사이의 텍스트는 서버에서 평가되지 않습니다.|  
|**xp_**|`xp_cmdshell`과 같이 카탈로그 확장 저장 프로시저의 이름 첫 자로 사용됩니다.|  
  
### <a name="use-type-safe-sql-parameters"></a>형식 안정적 SQL 매개 변수 사용  
 **의** Parameters [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컬렉션은 형식 검사와 길이 유효성 검사를 제공합니다. **Parameters** 컬렉션을 사용할 경우 입력은 실행 코드가 아닌 리터럴 값으로 처리됩니다. 또한 **Parameters** 컬렉션을 사용하면 형식 및 길이 검사도 강제 실행할 수 있다는 장점이 있습니다. 범위 밖의 값에 대해서는 예외가 발생합니다. 다음 코드 조각에서는 **Parameters** 컬렉션을 사용하는 방법을 보여 줍니다.  
  
```csharp
SqlDataAdapter myCommand = new SqlDataAdapter("AuthorLogin", conn);  
myCommand.SelectCommand.CommandType = CommandType.StoredProcedure;  
SqlParameter parm = myCommand.SelectCommand.Parameters.Add("@au_id",  
     SqlDbType.VarChar, 11);  
parm.Value = Login.Text;  
```  
  
 이 예에서는 `@au_id` 매개 변수가 실행 코드 대신 리터럴 값으로 처리됩니다. 이 값의 형식과 길이를 검사합니다. `@au_id` 값이 지정한 형식 및 길이 제약 조건에 부합하지 않을 경우 예외가 발생합니다.  
  
### <a name="use-parameterized-input-with-stored-procedures"></a>저장 프로시저에서 매개 변수가 있는 입력 사용  
 저장 프로시저가 필터링되지 않은 입력을 사용할 경우 SQL 삽입에 노출되기 쉽습니다. 예를 들면 다음 코드는 취약성이 있습니다.  
  
```csharp
SqlDataAdapter myCommand =   
new SqlDataAdapter("LoginStoredProcedure '" +   
                               Login.Text + "'", conn);  
```  
  
 저장 프로시저를 사용할 경우 입력으로 매개 변수를 사용합니다.  
  
### <a name="use-the-parameters-collection-with-dynamic-sql"></a>동적 SQL에서 Parameters 컬렉션 사용  
 저장 프로시저를 사용할 수 없는 경우에도 다음 코드 예와 같이 매개 변수를 사용할 수 있습니다.  
  
```csharp
SqlDataAdapter myCommand = new SqlDataAdapter(  
"SELECT au_lname, au_fname FROM Authors WHERE au_id = @au_id", conn);  
SQLParameter parm = myCommand.SelectCommand.Parameters.Add("@au_id",   
                        SqlDbType.VarChar, 11);  
Parm.Value = Login.Text;  
```  
  
### <a name="filtering-input"></a>필터링 입력  
 필터링 입력은 이스케이프 문자를 제거하므로 SQL 삽입으로부터 시스템을 보호할 수는 있지만 문자 수가 너무 많아 문제를 일으킬 수 있으므로 신뢰할 수 있는 방어책은 아닙니다. 다음 예에서는 문자열 구분 기호를 검색합니다.  
  
```csharp
private string SafeSqlLiteral(string inputSQL)  
{  
  return inputSQL.Replace("'", "''");  
}  
```  
  
### <a name="like-clauses"></a>LIKE 절  
 `LIKE` 절을 사용할 경우에도 와일드카드 문자를 이스케이프 처리해야 합니다.  
  
```csharp
s = s.Replace("[", "[[]");  
s = s.Replace("%", "[%]");  
s = s.Replace("_", "[_]");  
```  
  
## <a name="reviewing-code-for-sql-injection"></a>SQL 삽입에 대한 코드 검토  
 `EXECUTE`, `EXEC`또는 `sp_executesql`을 호출 하는 모든 코드를 검토해야 합니다. 다음과 유사한 쿼리를 사용하여 이러한 문을 포함하는 프로시저를 식별할 수 있습니다. 이 쿼리는 `EXECUTE` 또는 `EXEC`단어 뒤에 오는 1, 2, 3, 4개의 공백을 검사합니다.  
  
```sql
SELECT object_Name(id) FROM syscomments  
WHERE UPPER(text) LIKE '%EXECUTE (%'  
OR UPPER(text) LIKE '%EXECUTE  (%'  
OR UPPER(text) LIKE '%EXECUTE   (%'  
OR UPPER(text) LIKE '%EXECUTE    (%'  
OR UPPER(text) LIKE '%EXEC (%'  
OR UPPER(text) LIKE '%EXEC  (%'  
OR UPPER(text) LIKE '%EXEC   (%'  
OR UPPER(text) LIKE '%EXEC    (%'  
OR UPPER(text) LIKE '%SP_EXECUTESQL%';  
```  
  
### <a name="wrapping-parameters-with-quotename-and-replace"></a>QUOTENAME() 및 REPLACE()에서 매개 변수 래핑  
 선택한 각 저장 프로시저에서 동적 Transact-SQL에 사용된 모든 변수가 제대로 처리되는지 확인합니다. 저장 프로시저의 입력 매개 변수에서 가져온 데이터 또는 테이블에서 읽어 온 데이터는 QUOTENAME() 또는 REPLACE()에서 래핑되어야 합니다. QUOTENAME()에 전달되는 @variable의 값은 sysname이며 최대 길이는 128자입니다.  
  
|\@variable|권장 래퍼|  
|---------------|-------------------------|  
|보안 개체 이름|`QUOTENAME(@variable)`|  
|128자 이하의 문자열|`QUOTENAME(@variable, '''')`|  
|128자보다 큰 문자열|`REPLACE(@variable,'''', '''''')`|  
  
 이 방법을 사용하는 경우 SET 문을 다음과 같이 수정할 수 있습니다.  
  
```sql
-- Before:  
SET @temp = N'SELECT * FROM authors WHERE au_lname ='''   
 + @au_lname + N'''';  
  
-- After:  
SET @temp = N'SELECT * FROM authors WHERE au_lname = '''   
 + REPLACE(@au_lname,'''','''''') + N'''';  
```  
  
### <a name="injection-enabled-by-data-truncation"></a>데이터 잘림으로 활성화되는 삽입  
 변수에 할당되는 모든 동적 [!INCLUDE[tsql](../../includes/tsql-md.md)] 은 해당 변수에 할당된 버퍼보다 클 경우 잘립니다. 문 잘림을 수행할 수 있는 공격자는 예기치 않게 긴 문자열을 저장 프로시저에 전달하여 결과를 조작할 수 있습니다. 예를 들어 다음 스크립트로 만든 저장 프로시저는 잘림으로 활성화되는 삽입에 취약합니다.  
  
```sql
CREATE PROCEDURE sp_MySetPassword  
@loginname sysname,  
@old sysname,  
@new sysname  
AS  
-- Declare variable.  
-- Note that the buffer here is only 200 characters long.   
DECLARE @command varchar(200)  
-- Construct the dynamic Transact-SQL.  
-- In the following statement, we need a total of 154 characters   
-- to set the password of 'sa'.   
-- 26 for UPDATE statement, 16 for WHERE clause, 4 for 'sa', and 2 for  
-- quotation marks surrounded by QUOTENAME(@loginname):  
-- 200 - 26 - 16 - 4 - 2 = 154.  
-- But because @new is declared as a sysname, this variable can only hold  
-- 128 characters.   
-- We can overcome this by passing some single quotation marks in @new.  
SET @command= 'update Users set password='   
    + QUOTENAME(@new, '''') + ' where username='   
    + QUOTENAME(@loginname, '''') + ' AND password = '   
    + QUOTENAME(@old, '''')  
  
-- Execute the command.  
EXEC (@command)  
GO  
```  
  
 공격자는 128자 버퍼에 154자를 전달하여 이전 암호를 몰라도 sa에 새 암호를 설정할 수 있습니다.  
  
```sql
EXEC sp_MySetPassword 'sa', 'dummy',   
'123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012'''''''''''''''''''''''''''''''''''''''''''''''''''   
```  
  
 따라서 명령 변수에 큰 버퍼를 사용하거나 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 내부에서 동적 `EXECUTE` 을 직접 실행해야 합니다.  
  
### <a name="truncation-when-quotenamevariable--and-replace-are-used"></a>QUOTENAME(@variable, '''') 및 REPLACE() 사용 시 잘림  
 QUOTENAME() 및 REPLACE()에 의해 반환되는 문자열은 할당된 공간을 초과할 경우 자동으로 잘립니다. 다음 예에서 만든 저장 프로시저는 발생할 수 있는 동작을 보여 줍니다.  
  
```sql
CREATE PROCEDURE sp_MySetPassword  
    @loginname sysname,  
    @old sysname,  
    @new sysname  
AS  
  
-- Declare variables.  
    DECLARE @login sysname  
    DECLARE @newpassword sysname  
    DECLARE @oldpassword sysname  
    DECLARE @command varchar(2000)  
  
-- In the following statements, the data stored in temp variables  
-- will be truncated because the buffer size of @login, @oldpassword,  
-- and @newpassword is only 128 characters, but QUOTENAME() can return  
-- up to 258 characters.  
    SET @login = QUOTENAME(@loginname, '''')  
    SET @oldpassword = QUOTENAME(@old, '''')  
    SET @newpassword = QUOTENAME(@new, '''')  
  
-- Construct the dynamic Transact-SQL.  
-- If @new contains 128 characters, then @newpassword will be '123... n  
-- where n is the 127th character.   
-- Because the string returned by QUOTENAME() will be truncated,   
-- it can be made to look like the following statement:  
-- UPDATE Users SET password ='1234. . .[127] WHERE username=' -- other stuff here  
    SET @command = 'UPDATE Users set password = ' + @newpassword   
     + ' where username =' + @login + ' AND password = ' + @oldpassword;  
  
-- Execute the command.  
EXEC (@command);  
GO  
```  
  
 따라서 다음 문은 모든 사용자의 암호를 이전 코드에서 전달된 값으로 설정합니다.  
  
```sql
EXEC sp_MyProc '--', 'dummy', '12345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678'  
```  
  
 REPLACE()를 사용하는 경우 할당된 버퍼 공간을 초과하여 문자열 잘림을 수행할 수 있습니다. 다음 예에서 만든 저장 프로시저는 발생할 수 있는 동작을 보여 줍니다.  
  
```sql
CREATE PROCEDURE sp_MySetPassword  
    @loginname sysname,  
    @old sysname,  
    @new sysname  
AS  
  
-- Declare variables.  
    DECLARE @login sysname  
    DECLARE @newpassword sysname  
    DECLARE @oldpassword sysname  
    DECLARE @command varchar(2000)  
  
-- In the following statements, data will be truncated because   
-- the buffers allocated for @login, @oldpassword and @newpassword   
-- can hold only 128 characters, but QUOTENAME() can return   
-- up to 258 characters.   
    SET @login = REPLACE(@loginname, '''', '''''')  
    SET @oldpassword = REPLACE(@old, '''', '''''')  
    SET @newpassword = REPLACE(@new, '''', '''''')  
  
-- Construct the dynamic Transact-SQL.  
-- If @new contains 128 characters, @newpassword will be '123...n   
-- where n is the 127th character.   
-- Because the string returned by QUOTENAME() will be truncated, it  
-- can be made to look like the following statement:  
-- UPDATE Users SET password='1234...[127] WHERE username=' -- other stuff here   
    SET @command= 'update Users set password = ''' + @newpassword + ''' where username='''   
     + @login + ''' AND password = ''' + @oldpassword + '''';  
  
-- Execute the command.  
EXEC (@command);  
GO  
```  
  
 QUOTENAME()과 마찬가지로 REPLACE()로 발생하는 문자열 잘림은 모든 경우에 알맞는 크기의 임시 변수를 선언하여 방지할 수 있습니다. 가능한 경우 동적 [!INCLUDE[tsql](../../includes/tsql-md.md)]내부에서 QUOTENAME() 또는 REPLACE()를 직접 호출해야 합니다. 그렇지 않으면 다음과 같이 필요한 버퍼 크기를 계산할 수 있습니다. `@outbuffer = QUOTENAME(@input)`의 경우 `@outbuffer` 의 크기는 `2*(len(@input)+1)`이어야 합니다. 이전 예에서와 같이 `REPLACE()` 와 큰따옴표를 사용하는 경우 `2*len(@input)` 크기의 버퍼를 사용하면 충분합니다.  
  
 다음 계산은 모든 경우에 적용됩니다.  
  
```sql
WHILE LEN(@find_string) > 0, required buffer size =  
ROUND(LEN(@input)/LEN(@find_string),0) * LEN(@new_string)   
 + (LEN(@input) % LEN(@find_string))  
```  
  
### <a name="truncation-when-quotenamevariable--is-used"></a>QUOTENAME(@variable, ']')을 사용할 때 잘림  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안 개체의 이름이 `QUOTENAME(@variable, ']')`형식을 사용하는 문에 전달되는 경우 잘릴 수 있습니다. 다음 예에서는 이러한 방법을 보여 줍니다.  
  
```sql
CREATE PROCEDURE sp_MyProc  
    @schemaname sysname,  
    @tablename sysname,  
AS  
  
-- Declare a variable as sysname. The variable will be 128 characters.  
-- But @objectname actually must allow for 2*258+1 characters.   
DECLARE @objectname sysname  
SET @objectname = QUOTENAME(@schemaname)+'.'+ QUOTENAME(@tablename)   
-- Do some operations.  
GO  
```  
  
 sysname 형식의 값을 연결할 때는 값당 최대 128자를 포함할 수 있는 크기의 임시 변수를 사용해야 합니다. 가능한 경우 동적 `QUOTENAME()` 내부에서 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 직접 호출합니다. 그렇지 않으면 이전 섹션에서 설명한 대로 필요한 버퍼 크기를 계산할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [REPLACE&#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)   
 [QUOTENAME&#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)   
 [sp_executesql&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md)   
 [SQL Server 보안 설정](../../relational-databases/security/securing-sql-server.md)  
  
  
