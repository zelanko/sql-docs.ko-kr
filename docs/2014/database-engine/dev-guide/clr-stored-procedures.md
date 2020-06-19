---
title: CLR 저장 프로시저 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- database objects [CLR integration], stored procedures
- stored procedures [CLR integration]
- common language runtime [SQL Server], stored procedures
- building database objects [CLR integration], stored procedures
- output parameters [CLR integration]
- tabular results
ms.assetid: bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 4998058d55cd49c0eecfdecce2edc609a4d62c1f
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933732"
---
# <a name="clr-stored-procedures"></a>CLR 저장 프로시저
  저장 프로시저는 스칼라 식에서 사용할 수 없는 루틴입니다. 스칼라 함수와 달리 저장 프로시저는 테이블 형식의 결과와 메시지를 클라이언트에 반환하고 DDL(데이터 정의 언어) 및 DML(데이터 조작 언어) 문을 호출하고 출력 매개 변수를 반환할 수 있습니다. CLR 통합의 장점 및 관리 코드와 관리 코드를 선택 하는 방법에 대 한 자세한 내용은 [!INCLUDE[tsql](../../includes/tsql-md.md)] [Clr 통합 개요](../../relational-databases/clr-integration/clr-integration-overview.md)를 참조 하세요.  
  
## <a name="requirements-for-clr-stored-procedures"></a>CLR 저장 프로시저에 대한 요구 사항  
 CLR (공용 언어 런타임)에서 저장 프로시저는 어셈블리의 클래스에 대 한 공용 정적 메서드로 구현 됩니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] . 정적 메서드는 void로 선언되거나 정수 값을 반환할 수 있습니다. 정적 메서드가 정수 값을 반환하는 경우 반환되는 정수는 프로시저의 반환 코드로 취급됩니다. 다음은 그 예입니다.  
  
 `EXECUTE @return_status = procedure_name`  
  
 @return_status변수에는 메서드에서 반환 된 값이 포함 됩니다. 메서드가 void로 선언된 경우에는 반환 코드가 0입니다.  
  
 메서드가 매개 변수를 사용하는 경우 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 구현의 매개 변수 수가 저장 프로시저의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 선언에 사용된 매개 변수 수와 같아야 합니다.  
  
 관리 코드에 해당 형식이 있는 모든 네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 형식의 매개 변수를 CLR 저장 프로시저에 전달할 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문으로 프로시저를 만들려면 이러한 형식을 지정할 때 가장 가까운 네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 형식을 사용해야 합니다. 형식 변환에 대 한 자세한 내용은 [CLR 매개 변수 데이터 매핑](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)을 참조 하세요.  
  
### <a name="table-valued-parameters"></a>테이블 반환 매개 변수  
 프로시저 또는 함수로 전달되는 사용자 정의 테이블 형식인 TVP(테이블 반환 매개 변수)를 사용하면 여러 개의 데이터 행을 서버로 편리하게 전달할 수 있습니다. TVP는 매개 변수 배열과 유사한 기능을 제공하지만 더 유연하며 [!INCLUDE[tsql](../../includes/tsql-md.md)]과 더 밀접하게 통합됩니다. 또한 성능도 향상될 수 있습니다. TVP는 또한 서버와의 왕복 횟수를 줄이는 데 도움이 될 수 있습니다. 스칼라 매개 변수 목록과 같이 서버로 여러 개의 요청을 보내는 대신 서버에 데이터를 TVP로 보낼 수 있습니다. 사용자 정의 테이블 형식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스에서 실행 중인 관리되는 저장 프로시저 또는 함수에 테이블 반환 매개 변수로 전달되거나 이러한 저장 프로시저 또는 함수에서 테이블 반환 매개 변수로 반환될 수 없습니다. Tvp에 대 한 자세한 내용은 [데이터베이스 엔진&#41;&#40;테이블 반환 매개 변수 사용 ](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)을 참조 하세요.  
  
## <a name="returning-results-from-clr-stored-procedures"></a>CLR 저장 프로시저에서 결과 반환  
 출력 매개 변수, 테이블 형식 결과 및 메시지 등의 여러 가지 방법으로 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 저장 프로시저에서 정보를 반환할 수 있습니다.  
  
### <a name="output-parameters-and-clr-stored-procedures"></a>OUTPUT 매개 변수 및 CLR 저장 프로시저  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저와 마찬가지로 OUTPUT 매개 변수를 사용하여 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 저장 프로시저에서 정보를 반환할 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 만드는 데 사용하는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] DML 구문은 [!INCLUDE[tsql](../../includes/tsql-md.md)]로 작성된 저장 프로시저를 만드는 데 사용하는 구문과 같습니다. 구현 코드의 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 클래스에 있는 해당 매개 변수는 참조 전달(pass-by-reference) 매개 변수를 인수로 사용해야 합니다. Visual Basic는 c #에서와 동일한 방식으로 출력 매개 변수를 지원 하지 않습니다. 다음과 같이 매개 변수를 참조로 지정 하 고 \<Out()> 특성을 적용 하 여 출력 매개 변수를 나타내야 합니다.  
  
```vb
Imports System.Runtime.InteropServices  
...  
Public Shared Sub PriceSum ( <Out()> ByRef value As SqlInt32)  
```  
  
 다음 코드는 OUTPUT 매개 변수를 통해 정보를 반환하는 저장 프로시저를 보여 줍니다.  
  
```csharp  
using System;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void PriceSum(out SqlInt32 value)  
   {  
      using(SqlConnection connection = new SqlConnection("context connection=true"))   
      {  
         value = 0;  
         connection.Open();  
         SqlCommand command = new SqlCommand("SELECT Price FROM Products", connection);  
         SqlDataReader reader = command.ExecuteReader();  
  
         using (reader)  
         {  
            while( reader.Read() )  
            {  
               value += reader.GetSqlInt32(0);  
            }  
         }           
      }  
   }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
Imports System.Runtime.InteropServices  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Executes a query and iterates over the results to perform a summation.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub PriceSum( <Out()> ByRef value As SqlInt32)  
  
        Using connection As New SqlConnection("context connection=true")  
           value = 0  
           Connection.Open()  
           Dim command As New SqlCommand("SELECT Price FROM Products", connection)  
           Dim reader As SqlDataReader  
           reader = command.ExecuteReader()  
  
           Using reader  
              While reader.Read()  
                 value += reader.GetSqlInt32(0)  
              End While  
           End Using  
        End Using          
    End Sub  
End Class  
```  
  
 위의 CLR 저장 프로시저가 포함 된 어셈블리를 서버에서 작성 하 고 만든 후에는 다음을 [!INCLUDE[tsql](../../includes/tsql-md.md)] 사용 하 여 데이터베이스에 프로시저를 만들고 *SUM* 을 OUTPUT 매개 변수로 지정 합니다.  
  
```sql
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
-- if StoredProcedures class was inside a namespace, called MyNS,  
-- you would use:  
-- AS EXTERNAL NAME TestStoredProc.[MyNS.StoredProcedures].PriceSum  
```  
  
 *Sum* 은 `int` SQL Server 데이터 형식으로 선언 되 고, clr 저장 프로시저에 정의 된 *값* 매개 변수는 clr 데이터 형식으로 지정 됩니다 `SqlInt32` . 호출 프로그램에서 CLR 저장 프로시저를 실행 하면에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `SqlInt32` clr 데이터 형식을 자동으로 `int` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식으로 변환 합니다.  변환할 수 있는 CLR 데이터 형식에 대 한 자세한 내용은 [Clr 매개 변수 데이터 매핑](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)을 참조 하세요.  
  
### <a name="returning-tabular-results-and-messages"></a>테이블 형식 결과 및 메시지 반환  
 테이블 형식 결과 및 메시지를 클라이언트에 반환하려면 `SqlPipe` 개체를 사용합니다. 이 개체는 `Pipe` 클래스의 `SqlContext` 속성을 사용하여 가져옵니다. `SqlPipe` 개체에는 `Send` 메서드가 있습니다. `Send` 메서드를 호출하여 데이터를 파이프를 통해 호출 애플리케이션으로 전송할 수 있습니다.  
  
 `SqlPipe.Send`를 보내는 메서드와 단순히 텍스트 문자열을 보내는 다른 메서드를 포함하여 `SqlDataReader` 메서드의 오버로드가 여러 개 있습니다.  
  
###### <a name="returning-messages"></a>메시지 반환  
 `SqlPipe.Send(string)`를 사용하여 메시지를 클라이언트 애플리케이션에 보낼 수 있습니다. 메시지 텍스트는 8000자로 제한되며 8000자를 초과하면 잘립니다.  
  
###### <a name="returning-tabular-results"></a>테이블 형식 결과 반환  
 쿼리 결과를 직접 클라이언트로 보내려면 `Execute` 메서드 오버로드 중 하나를 `SqlPipe` 개체에 사용합니다. 이 방법이 결과 집합을 가장 효율적으로 클라이언트에 반환하는 방법입니다. 그 이유는 데이터가 관리되는 메모리에 복사되지 않고 네트워크 버퍼로 전송되기 때문입니다. 다음은 그 예입니다.  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   /// <summary>  
   /// Execute a command and send the results to the client directly.  
   /// </summary>  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void ExecuteToClient()  
   {  
   using(SqlConnection connection = new SqlConnection("context connection=true"))   
   {  
      connection.Open();  
      SqlCommand command = new SqlCommand("select @@version", connection);  
      SqlContext.Pipe.ExecuteAndSend(command);  
      }  
   }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Execute a command and send the results to the client directly.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub ExecuteToClient()  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT @@VERSION", connection)  
            SqlContext.Pipe.ExecuteAndSend(command)  
        End Using  
    End Sub  
End Class  
```  
  
 앞서 실행한 쿼리 결과를 in-process 공급자를 통해 보내거나 사용자 지정 `SqlDataReader` 구현을 사용하여 데이터를 미리 처리하려면 `Send`를 사용하는 `SqlDataReader` 메서드의 오버로드를 사용합니다. 이 방법은 앞에서 설명한 직접적인 방법보다 조금 느리기는 하지만 데이터를 클라이언트로 보내기 전에 조작할 수 있다는 융통성이 있습니다.  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   /// <summary>  
   /// Execute a command and send the resulting reader to the client  
   /// </summary>  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void SendReaderToClient()  
   {  
      using(SqlConnection connection = new SqlConnection("context connection=true"))   
      {  
         connection.Open();  
         SqlCommand command = new SqlCommand("select @@version", connection);  
         SqlDataReader r = command.ExecuteReader();  
         SqlContext.Pipe.Send(r);  
      }  
   }  
}  
```  
 
```vb  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Execute a command and send the results to the client directly.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub SendReaderToClient()  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT @@VERSION", connection)  
            Dim reader As SqlDataReader  
            reader = command.ExecuteReader()  
            SqlContext.Pipe.Send(reader)  
        End Using  
    End Sub  
End Class  
```  
  
 동적 결과 집합을 만들어 결과 집합을 채운 후 클라이언트로 보내려면 현재 연결에서 레코드를 만든 다음 `SqlPipe.Send`를 사용하여 보냅니다.  
  
```csharp  
using System.Data;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
using System.Data.SqlTypes;  
  
public class StoredProcedures   
{  
   /// <summary>  
   /// Create a result set on the fly and send it to the client.  
   /// </summary>  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void SendTransientResultSet()  
   {  
      // Create a record object that represents an individual row, including it's metadata.  
      SqlDataRecord record = new SqlDataRecord(new SqlMetaData("stringcol", SqlDbType.NVarChar, 128));  
  
      // Populate the record.  
      record.SetSqlString(0, "Hello World!");  
  
      // Send the record to the client.  
      SqlContext.Pipe.Send(record);  
   }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Create a result set on the fly and send it to the client.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub SendTransientResultSet()  
        ' Create a record object that represents an individual row, including it's metadata.  
        Dim record As New SqlDataRecord(New SqlMetaData("stringcol", SqlDbType.NVarChar, 128) )  
  
        ' Populate the record.  
        record.SetSqlString(0, "Hello World!")  
  
        ' Send the record to the client.  
        SqlContext.Pipe.Send(record)          
    End Sub  
End Class   
```  
  
 다음은 `SqlPipe`를 통해 테이블 형식 결과와 메시지를 보내는 예입니다.  
  
```csharp  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void HelloWorld()  
   {  
      SqlContext.Pipe.Send("Hello world! It's now " + System.DateTime.Now.ToString()+"\n");  
      using(SqlConnection connection = new SqlConnection("context connection=true"))   
      {  
         connection.Open();  
         SqlCommand command = new SqlCommand("SELECT ProductNumber FROM ProductMaster", connection);  
         SqlDataReader reader = command.ExecuteReader();  
         SqlContext.Pipe.Send(reader);  
      }  
   }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Execute a command and send the results to the client directly.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub HelloWorld()  
        SqlContext.Pipe.Send("Hello world! It's now " & System.DateTime.Now.ToString() & "\n")  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT ProductNumber FROM ProductMaster", connection)  
            Dim reader As SqlDataReader  
            reader = command.ExecuteReader()  
            SqlContext.Pipe.Send(reader)  
        End Using  
    End Sub  
End Class   
```  
  
 첫 번째 `Send`는 클라이언트에 메시지를 보내고 두 번째 Send는 `SqlDataReader`를 사용하여 테이블 형식 결과를 보냅니다.  
  
 이러한 예는 이해를 돕기 위한 목적으로만 사용되었습니다. 계산을 많이 수행하는 애플리케이션의 경우 단순한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문보다 CLR 함수가 적합합니다. 앞의 예와 거의 비슷한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저는 다음과 같습니다.  
  
```sql
CREATE PROCEDURE HelloWorld() AS  
BEGIN  
PRINT('Hello world!')  
SELECT ProductNumber FROM ProductMaster  
END;  
```  
  
> [!NOTE]  
>  클라이언트 애플리케이션에서는 메시지와 결과 집합이 다른 방식으로 검색됩니다. 예를 들어 결과 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 집합은 **결과** 뷰에 나타나고 메시지는 메시지 창에 표시 됩니다 **Messages** .  
  
 위의 Visual C# 코드를 MyFirstUdp.cs 파일에 저장한 경우 다음 코드를 사용하여 컴파일합니다.  
  
```console
csc /t:library /out:MyFirstUdp.dll MyFirstUdp.cs   
```  
  
 또는 위의 Visual Basic 코드를 MyFirstUdp.vb 파일에 저장한 경우 다음 코드를 사용하여 컴파일합니다.  
  
```console
vbc /t:library /out:MyFirstUdp.dll MyFirstUdp.vb   
```  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터 `/clr:pure`로 컴파일된 Visual C++ 데이터베이스 개체(예: 저장 프로시저)의 실행은 지원되지 않습니다.  
  
 결과 어셈블리를 등록한 후 다음 DDL을 사용하여 진입점을 호출할 수 있습니다.  
  
```sql
CREATE ASSEMBLY MyFirstUdp FROM 'C:\Programming\MyFirstUdp.dll';  
CREATE PROCEDURE HelloWorld  
AS EXTERNAL NAME MyFirstUdp.StoredProcedures.HelloWorld;  
EXEC HelloWorld;  
```  
  
## <a name="see-also"></a>참고 항목  
 [CLR 사용자 정의 함수](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [CLR 사용자 정의 형식](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [CLR 트리거](../../../2014/database-engine/dev-guide/clr-triggers.md)  
  
  
