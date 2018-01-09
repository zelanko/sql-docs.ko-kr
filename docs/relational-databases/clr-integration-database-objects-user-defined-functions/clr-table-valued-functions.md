---
title: "CLR 테이블 반환 함수 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- Transact-SQL table-valued functions
- table-valued functions [CLR integration]
- TVFs [CLR integration]
ms.assetid: 9a6133ea-36e9-45bf-b572-1c0df3d6c194
caps.latest.revision: "88"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 220c83c7378e634745a7edc71f521d30c3f812b6
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="clr-table-valued-functions"></a>CLR 테이블 반환 함수
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]테이블 반환 함수는 테이블을 반환 하는 사용자 정의 함수가입니다.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 모든 관리 언어에서 테이블 반환 함수를 정의할 수 있도록 하여 테이블 반환 함수의 기능을 확장하고 있습니다. 데이터를 통해 테이블 반환 함수에서 반환 되는 **IEnumerable** 또는 **IEnumerator** 개체입니다.  
  
> [!NOTE]  
>  테이블 반환 함수에 대 한 반환 테이블 형식의 열에서는 타임 스탬프 열 또는 비유니코드 문자열 데이터 형식 열 포함할 수 없습니다 (예: **char**, **varchar**, 및 **텍스트**). NOT NULL 제약 조건은 지원되지 않습니다.  
  
 CLR 테이블 반환 함수에 대 한 자세한 내용은 체크 아웃 MSSQLTips' [소개 SQL Server CLR 테이블 반환된 함수!](https://www.mssqltips.com/sqlservertip/2582/introduction-to-sql-server-clr-table-valued-functions/)  
  
## <a name="differences-between-transact-sql-and-clr-table-valued-functions"></a>Transact-SQL과 CLR 테이블 반환 함수의 차이  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 테이블 반환 함수는 함수 호출의 결과를 중간 테이블로 구체화합니다. TVF는 중간 테이블을 사용하므로 결과에 대해 제약 조건 및 고유 인덱스를 지원할 수 있습니다. 이러한 기능은 대규모의 결과가 반환할 때 매우 유용합니다.  
  
 반면 CLR 테이블 반환 함수는 스트리밍 방식을 사용합니다. 전체 결과 집합을 단일 테이블로 구체화할 필요가 없습니다. **IEnumerable** 는 결과 사용 하 여 증분 방식에서 및 관리 되는 함수에서 반환 된 개체를 직접 테이블 반환 함수를 호출 하는 쿼리의 실행 계획에서 호출 됩니다. 이 스트리밍 모델은 전체 테이블이 채워질 때까지 기다리지 않고 첫 번째 행을 사용할 수 있게 된 직후부터 결과를 사용할 수 있도록 합니다. 반환되는 행의 수가 매우 많은 경우에도 이러한 행을 메모리에서 전체적으로 구체화할 필요가 없는 이 방법이 더 효율적입니다. 예를 들어 관리 테이블 반환 함수는 텍스트 파일을 구문 분석하고 각 줄을 하나의 행으로 반환하는 데 사용할 수 있습니다.  
  
## <a name="implementing-table-valued-functions"></a>테이블 반환 함수 구현  
 테이블 반환 함수를 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 어셈블리 클래스의 메서드로 구현합니다. 테이블 반환 함수 코드를 구현 해야 합니다는 **IEnumerable** 인터페이스입니다. **IEnumerable** 인터페이스는.NET Framework에서 정의 됩니다. 나타내는 형식의 배열 및.NET Framework에서에서 컬렉션에 이미 구현 된 **IEnumerable** 인터페이스입니다. 따라서 컬렉션 또는 배열을 결과 집합으로 변환하는 테이블 반환 함수를 손쉽게 작성할 수 있습니다.  
  
## <a name="table-valued-parameters"></a>테이블 반환 매개 변수  
 테이블 반환 매개 변수는 프로시저 또는 함수로 전달되는 사용자 정의 테이블 형식이며 여러 개의 데이터 행을 서버로 편리하게 전달할 수 있습니다. 테이블 반환 매개 변수는 매개 변수 배열과 유사한 기능을 제공하지만 더 유연하며 [!INCLUDE[tsql](../../includes/tsql-md.md)]과 더 밀접하게 통합됩니다. 또한 성능도 향상될 수 있습니다. 또한 테이블 반환 매개 변수는 서버와의 왕복 횟수를 줄이는 데 도움이 될 수 있습니다. 스칼라 매개 변수 목록과 같이 서버로 여러 개의 요청을 보내는 대신 서버에 데이터를 테이블 반환 매개 변수로 보낼 수 있습니다. 사용자 정의 테이블 형식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스에서 실행 중인 관리되는 저장 프로시저 또는 함수에 테이블 반환 매개 변수로 전달되거나 이러한 저장 프로시저 또는 함수에서 테이블 반환 매개 변수로 반환될 수 없습니다. 테이블 반환 매개 변수에 대 한 자세한 내용은 참조 [테이블 반환 매개 변수 &#40; 데이터베이스 엔진 &#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)합니다.  
  
## <a name="output-parameters-and-table-valued-functions"></a>출력 매개 변수와 테이블 반환 함수  
 테이블 반환 함수에서 출력 매개 변수를 사용하여 정보를 반환할 수 있습니다. 구현 코드의 테이블 반환 함수에 있는 해당 매개 변수는 참조 전달(pass-by-reference) 매개 변수를 인수로 사용해야 합니다. Visual Basic은 Visual C#과 같은 방식으로 출력 매개 변수를 지원하지 않습니다. 적용 하 고 참조로 매개 변수를 지정 해야는 \<out () > 특성을 다음과 같이 출력 매개 변수를 나타냅니다.  
  
```vb  
Imports System.Runtime.InteropServices  
…  
Public Shared Sub FillRow ( <Out()> ByRef value As SqlInt32)  
```  
  
### <a name="defining-a-table-valued-function-in-transact-sql"></a>Transact-SQL에서 테이블 반환 함수 정의  
 CLR 테이블 반환 함수를 정의 하기 위한 구문은 유사 하지만 한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 추가 하 여 테이블 반환 함수는 **외부 이름** 절. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```  
CREATE FUNCTION GetEmpFirstLastNames()  
RETURNS TABLE (FirstName NVARCHAR(4000), LastName NVARCHAR(4000))  
EXTERNAL NAME MyDotNETAssembly.[MyNamespace.MyClassname]. GetEmpFirstLastNames;  
```  
  
 테이블 반환 함수는 다음과 같은 쿼리에서 추가 처리를 위해 관계형 형식으로 데이터를 나타내는 데 사용됩니다.  
  
```  
select * from function();  
select * from tbl join function() f on tbl.col = f.col;  
select * from table t cross apply function(t.column);  
```  
  
 테이블 반환 함수는 다음 경우 테이블을 반환할 수 있습니다.  
  
-   스칼라 입력 인수에서 만들어지는 경우. 예: 쉼표로 구분된 숫자 문자열을 받아 이를 테이블로 피벗하는 테이블 반환 함수  
  
-   외부 데이터에서 생성되는 경우. 예: 이벤트 로그를 읽고 이를 테이블로 노출하는 테이블 반환 함수  
  
 **참고** 테이블 반환 함수를 통해 데이터 액세스에만 수행할 수는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에서 쿼리는 **InitMethod** 메서드를 아니라는 **FillRow** 메서드. **InitMethod** 로 표시 해야는 **SqlFunction.DataAccess.Read** 경우 특성의 속성은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리가 실행 됩니다.  
  
## <a name="a-sample-table-valued-function"></a>예제 테이블 반환 함수  
 다음 테이블 반환 함수는 시스템 이벤트 로그의 정보를 반환합니다. 함수는 읽을 이벤트 로그의 이름을 포함하는 단일 문자열 인수를 받습니다.  
  
###### <a name="sample-code"></a>예제 코드  
  
```csharp  
using System;  
using System.Data.Sql;  
using Microsoft.SqlServer.Server;  
using System.Collections;  
using System.Data.SqlTypes;  
using System.Diagnostics;  
  
public class TabularEventLog  
{  
    [SqlFunction(FillRowMethodName = "FillRow")]  
    public static IEnumerable InitMethod(String logname)  
    {  
        return new EventLog(logname).Entries;    }  
  
    public static void FillRow(Object obj, out SqlDateTime timeWritten, out SqlChars message, out SqlChars category, out long instanceId)  
    {  
        EventLogEntry eventLogEntry = (EventLogEntry)obj;  
        timeWritten = new SqlDateTime(eventLogEntry.TimeWritten);  
        message = new SqlChars(eventLogEntry.Message);  
        category = new SqlChars(eventLogEntry.Category);  
        instanceId = eventLogEntry.InstanceId;  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Data.Sql  
Imports Microsoft.SqlServer.Server  
Imports System.Collections  
Imports System.Data.SqlTypes  
Imports System.Diagnostics  
Imports System.Runtime.InteropServices  
  
Public Class TabularEventLog  
    <SqlFunction(FillRowMethodName:="FillRow")> _  
    Public Shared Function InitMethod(ByVal logname As String) As IEnumerable  
        Return New EventLog(logname).Entries  
    End Function  
  
    Public Shared Sub FillRow(ByVal obj As Object, <Out()> ByRef timeWritten As SqlDateTime, <Out()> ByRef message As SqlChars, <Out()> ByRef category As SqlChars, <Out()> ByRef instanceId As Long)  
        Dim eventLogEnTry As EventLogEntry = CType(obj, EventLogEntry)  
        timeWritten = New SqlDateTime(eventLogEnTry.TimeWritten)  
        message = New SqlChars(eventLogEnTry.Message)  
        category = New SqlChars(eventLogEnTry.Category)  
        instanceId = eventLogEnTry.InstanceId  
    End Sub  
End Class  
```  
  
###### <a name="declaring-and-using-the-sample-table-valued-function"></a>예제 테이블 반환 함수 선언 및 사용  
 예제 테이블 반환 함수가 컴파일되면 다음과 같이 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 선언할 수 있습니다.  
  
```  
use master;  
-- Replace SQL_Server_logon with your SQL Server user credentials.  
GRANT EXTERNAL ACCESS ASSEMBLY TO [SQL_Server_logon];   
-- Modify the following line to specify a different database.  
ALTER DATABASE master SET TRUSTWORTHY ON;  
  
-- Modify the next line to use the appropriate database.  
CREATE ASSEMBLY tvfEventLog   
FROM 'D:\assemblies\tvfEventLog\tvfeventlog.dll'   
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
GO  
CREATE FUNCTION ReadEventLog(@logname nvarchar(100))  
RETURNS TABLE   
(logTime datetime,Message nvarchar(4000),Category nvarchar(4000),InstanceId bigint)  
AS   
EXTERNAL NAME tvfEventLog.TabularEventLog.InitMethod;  
GO  
```  
  
 /clr:pure로 컴파일된 Visual C++ 데이터베이스 개체는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 실행할 수 없습니다. 예를 들어 이러한 데이터베이스 개체에는 테이블 반환 함수가 포함됩니다.  
  
 예제를 테스트하려면 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드를 사용하십시오.  
  
```  
-- Select the top 100 events,  
SELECT TOP 100 *  
FROM dbo.ReadEventLog(N'Security') as T;  
go  
  
-- Select the last 10 login events.  
SELECT TOP 10 T.logTime, T.Message, T.InstanceId   
FROM dbo.ReadEventLog(N'Security') as T  
WHERE T.Category = N'Logon/Logoff';  
go  
```  
  
## <a name="sample-returning-the-results-of-a-sql-server-query"></a>예제: SQL Server 쿼리 결과 반환  
 다음 예제에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 쿼리하는 테이블 반환 함수를 보여줍니다. 이 예제에서는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에서 AdventureWorks Light 데이터베이스를 사용합니다. 참조 [http://www.codeplex.com/sqlserversamples](http://go.microsoft.com/fwlink/?LinkId=87843) AdventureWorks 다운로드에 대 한 자세한 내용은 합니다.  
  
 원본 코드 파일 FindInvalidEmails.cs 또는 FindInvalidEmails.vb를 지정하십시오.  
  
```csharp  
using System;  
using System.Collections;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
  
using Microsoft.SqlServer.Server;  
  
public partial class UserDefinedFunctions {  
   private class EmailResult {  
      public SqlInt32 CustomerId;  
      public SqlString EmailAdress;  
  
      public EmailResult(SqlInt32 customerId, SqlString emailAdress) {  
         CustomerId = customerId;  
         EmailAdress = emailAdress;  
      }  
   }  
  
   public static bool ValidateEmail(SqlString emailAddress) {  
      if (emailAddress.IsNull)  
         return false;  
  
      if (!emailAddress.Value.EndsWith("@adventure-works.com"))  
         return false;  
  
      // Validate the address. Put any more rules here.  
      return true;  
   }  
  
   [SqlFunction(  
       DataAccess = DataAccessKind.Read,  
       FillRowMethodName = "FindInvalidEmails_FillRow",  
       TableDefinition="CustomerId int, EmailAddress nvarchar(4000)")]  
   public static IEnumerable FindInvalidEmails(SqlDateTime modifiedSince) {  
      ArrayList resultCollection = new ArrayList();  
  
      using (SqlConnection connection = new SqlConnection("context connection=true")) {  
         connection.Open();  
  
         using (SqlCommand selectEmails = new SqlCommand(  
             "SELECT " +  
             "[CustomerID], [EmailAddress] " +  
             "FROM [AdventureWorksLT2008].[SalesLT].[Customer] " +  
             "WHERE [ModifiedDate] >= @modifiedSince",  
             connection)) {  
            SqlParameter modifiedSinceParam = selectEmails.Parameters.Add(  
                "@modifiedSince",  
                SqlDbType.DateTime);  
            modifiedSinceParam.Value = modifiedSince;  
  
            using (SqlDataReader emailsReader = selectEmails.ExecuteReader()) {  
               while (emailsReader.Read()) {  
                  SqlString emailAddress = emailsReader.GetSqlString(1);  
                  if (ValidateEmail(emailAddress)) {  
                     resultCollection.Add(new EmailResult(  
                         emailsReader.GetSqlInt32(0),  
                         emailAddress));  
                  }  
               }  
            }  
         }  
      }  
  
      return resultCollection;  
   }  
  
   public static void FindInvalidEmails_FillRow(  
       object emailResultObj,  
       out SqlInt32 customerId,  
       out SqlString emailAdress) {  
      EmailResult emailResult = (EmailResult)emailResultObj;  
  
      customerId = emailResult.CustomerId;  
      emailAdress = emailResult.EmailAdress;  
   }  
};  
```  
  
```vb  
Imports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Public Partial Class UserDefinedFunctions  
   Private Class EmailResult  
      Public CustomerId As SqlInt32  
      Public EmailAdress As SqlString  
  
      Public Sub New(customerId__1 As SqlInt32, emailAdress__2 As SqlString)  
         CustomerId = customerId__1  
         EmailAdress = emailAdress__2  
      End Sub  
   End Class  
  
   Public Shared Function ValidateEmail(emailAddress As SqlString) As Boolean  
      If emailAddress.IsNull Then  
         Return False  
      End If  
  
      If Not emailAddress.Value.EndsWith("@adventure-works.com") Then  
         Return False  
      End If  
  
      ' Validate the address. Put any more rules here.  
      Return True  
   End Function  
  
   <SqlFunction(DataAccess := DataAccessKind.Read, FillRowMethodName := "FindInvalidEmails_FillRow", TableDefinition := "CustomerId int, EmailAddress nvarchar(4000)")> _  
   Public Shared Function FindInvalidEmails(modifiedSince As SqlDateTime) As IEnumerable  
      Dim resultCollection As New ArrayList()  
  
      Using connection As New SqlConnection("context connection=true")  
         connection.Open()  
  
         Using selectEmails As New SqlCommand("SELECT " & "[CustomerID], [EmailAddress] " & "FROM [AdventureWorksLT2008].[SalesLT].[Customer] " & "WHERE [ModifiedDate] >= @modifiedSince", connection)  
            Dim modifiedSinceParam As SqlParameter = selectEmails.Parameters.Add("@modifiedSince", SqlDbType.DateTime)  
            modifiedSinceParam.Value = modifiedSince  
  
            Using emailsReader As SqlDataReader = selectEmails.ExecuteReader()  
               While emailsReader.Read()  
                  Dim emailAddress As SqlString = emailsReader.GetSqlString(1)  
                  If ValidateEmail(emailAddress) Then  
                     resultCollection.Add(New EmailResult(emailsReader.GetSqlInt32(0), emailAddress))  
                  End If  
               End While  
            End Using  
         End Using  
      End Using  
  
      Return resultCollection  
   End Function  
  
   Public Shared Sub FindInvalidEmails_FillRow(emailResultObj As Object, ByRef customerId As SqlInt32, ByRef emailAdress As SqlString)  
      Dim emailResult As EmailResult = DirectCast(emailResultObj, EmailResult)  
  
      customerId = emailResult.CustomerId  
      emailAdress = emailResult.EmailAdress  
   End Sub  
End ClassImports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Public Partial Class UserDefinedFunctions  
   Private Class EmailResult  
      Public CustomerId As SqlInt32  
      Public EmailAdress As SqlString  
  
      Public Sub New(customerId__1 As SqlInt32, emailAdress__2 As SqlString)  
         CustomerId = customerId__1  
         EmailAdress = emailAdress__2  
      End Sub  
   End Class  
  
   Public Shared Function ValidateEmail(emailAddress As SqlString) As Boolean  
      If emailAddress.IsNull Then  
         Return False  
      End If  
  
      If Not emailAddress.Value.EndsWith("@adventure-works.com") Then  
         Return False  
      End If  
  
      ' Validate the address. Put any more rules here.  
      Return True  
   End Function  
  
   <SqlFunction(DataAccess := DataAccessKind.Read, FillRowMethodName := "FindInvalidEmails_FillRow", TableDefinition := "CustomerId int, EmailAddress nvarchar(4000)")> _  
   Public Shared Function FindInvalidEmails(modifiedSince As SqlDateTime) As IEnumerable  
      Dim resultCollection As New ArrayList()  
  
      Using connection As New SqlConnection("context connection=true")  
         connection.Open()  
  
         Using selectEmails As New SqlCommand("SELECT " & "[CustomerID], [EmailAddress] " & "FROM [AdventureWorksLT2008].[SalesLT].[Customer] " & "WHERE [ModifiedDate] >= @modifiedSince", connection)  
            Dim modifiedSinceParam As SqlParameter = selectEmails.Parameters.Add("@modifiedSince", SqlDbType.DateTime)  
            modifiedSinceParam.Value = modifiedSince  
  
            Using emailsReader As SqlDataReader = selectEmails.ExecuteReader()  
               While emailsReader.Read()  
                  Dim emailAddress As SqlString = emailsReader.GetSqlString(1)  
                  If ValidateEmail(emailAddress) Then  
                     resultCollection.Add(New EmailResult(emailsReader.GetSqlInt32(0), emailAddress))  
                  End If  
               End While  
            End Using  
         End Using  
      End Using  
  
      Return resultCollection  
   End Function  
  
   Public Shared Sub FindInvalidEmails_FillRow(emailResultObj As Object, customerId As SqlInt32, emailAdress As SqlString)  
      Dim emailResult As EmailResult = DirectCast(emailResultObj, EmailResult)  
  
      customerId = emailResult.CustomerId  
      emailAdress = emailResult.EmailAdress  
   End Sub  
End Class  
```  
  
 원본 코드를 DLL로 컴파일한 다음 C 드라이브의 루트 디렉터리에 이 DLL을 복사한 후  다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 실행합니다.  
  
```  
use AdventureWorksLT2008;  
go  
  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'FindInvalidEmails')  
   DROP FUNCTION FindInvalidEmails;  
go  
  
IF EXISTS (SELECT name FROM sys.assemblies WHERE name = 'MyClrCode')  
   DROP ASSEMBLY MyClrCode;  
go  
  
CREATE ASSEMBLY MyClrCode FROM 'C:\FindInvalidEmails.dll'  
WITH PERMISSION_SET = SAFE -- EXTERNAL_ACCESS;  
GO  
  
CREATE FUNCTION FindInvalidEmails(@ModifiedSince datetime)   
RETURNS TABLE (  
   CustomerId int,  
   EmailAddress nvarchar(4000)  
)  
AS EXTERNAL NAME MyClrCode.UserDefinedFunctions.[FindInvalidEmails];  
go  
  
SELECT * FROM FindInvalidEmails('2000-01-01');  
go  
```  
  
  
