---
title: SqlPipe 개체 | Microsoft Docs
description: SQL Server에서 실행 되는 CLR 데이터베이스 개체의 경우 SqlPipe 개체의 Send 메서드를 사용 하 여 연결 된 파이프에 결과를 보낼 수 있습니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- custom result sets [CLR integration]
- SqlPipe object
- tabular results
ms.assetid: 3e090faf-085f-4c01-a565-79e3f1c36e3b
author: rothja
ms.author: jroth
ms.openlocfilehash: 17a26c5897ff10ce636297151cef9f300f4f3056
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765419"
---
# <a name="sqlpipe-object"></a>SqlPipe 개체
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이전 버전에서는 결과나 출력 매개 변수를 호출 클라이언트로 보내는 저장 프로시저(또는 확장 저장 프로시저)를 작성하는 것이 일반적이었습니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저에서 0개 이상의 행을 반환하는 **SELECT** 문은 결과를 연결된 호출자의 "파이프"로 보냅니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 실행되는 CLR(공용 언어 런타임) 데이터베이스 개체의 경우 **Send** 개체의 **SqlPipe** 메서드를 사용하여 결과를 연결된 파이프로 보낼 수 있습니다. **Pipe** 개체의 **SqlContext** 속성에 액세스하여 **SqlPipe** 개체를 가져옵니다. **SqlPipe** 클래스는 개념상 ASP.NET에 있는 **Response** 클래스와 유사합니다. 자세한 내용은 .NET Framework 소프트웨어 개발 키트의 SqlPipe 클래스 참조 설명서를 참조하십시오.  
  
## <a name="returning-tabular-results-and-messages"></a>테이블 형식 결과 및 메시지 반환  
 **SqlPipe** 에는 3개의 오버로드가 있는 **Send** 메서드가 있습니다. 아래에 이 계정과 키의 예제가 나와 있습니다.  
  
-   `void Send(string message)`  
  
-   `void Send(SqlDataReader reader)`  
  
-   `void Send(SqlDataRecord record)`  
  
 **Send** 메서드는 클라이언트 또는 호출자에게 직접 데이터를 보냅니다. 일반적으로 클라이언트에서 **SqlPipe**의 출력을 사용하지만, 중첩된 CLR 저장 프로시저의 경우 출력 소비자는 저장 프로시저일 수도 있습니다. 예를 들어 Procedure1은 명령 텍스트 "EXEC Procedure2"를 사용하여 SqlCommand.ExecuteReader()를 호출합니다. Procedure2도 관리되는 저장 프로시저입니다. 이제 Procedure2에서 SqlPipe.Send( SqlDataRecord )를 호출하면 행은 호출자가 아닌 Procedure1의 판독기로 보내집니다.  
  
 **Send** 메서드는의 인쇄와 동일 하 게 정보 메시지로 클라이언트에 표시 되는 문자열 메시지를 보냅니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] . **SqlDataRecord**를 사용하여 단일 행 결과 집합을 보내거나 **SqlDataReader**를 사용하여 다중 행 결과 집합을 보낼 수도 있습니다.  
  
 또한 **SqlPipe** 개체에는 **ExecuteAndSend** 메서드도 있습니다. 이 메서드를 사용하여 **SqlCommand** 개체로 전달된 명령을 실행하고 결과를 직접 호출자에게 보낼 수 있습니다. 전송된 명령에 오류가 있으면 예외를 파이프로 보내지만 호출 관리 코드에도 복사본을 보냅니다. 호출 코드에서 예외를 catch하지 않을 경우 해당 예외는 스택을 통해 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드에 전파되고 출력에 두 번 나타납니다. 호출 코드에서 예외를 catch하지 않을 경우 파이프 소비자에게 오류가 표시되지만 중복 오류는 없습니다.  
  
 이 메서드는 컨텍스트 연결과 관련된 **SqlCommand** 만 사용할 수 있으며 비컨텍스트 연결과 관련된 명령은 사용할 수 없습니다.  
  
## <a name="returning-custom-result-sets"></a>사용자 지정 결과 집합 반환  
 관리되는 저장 프로시저는 **SqlDataReader**에서 제공되지 않은 결과 집합을 보낼 수 있습니다. **SendResultsStart** 메서드와 함께 **SendResultsRow** 및 **SendResultsEnd**를 사용하면 저장 프로시저에서 사용자 지정 결과 집합을 클라이언트로 보낼 수 있습니다.  
  
 **SendResultsStart** 는 **SqlDataRecord** 를 입력으로 사용합니다. 결과 집합의 시작 부분을 표시하고 레코드 메타데이터를 사용하여 결과 집합을 설명하는 메타데이터를 만듭니다. 레코드 값은 **SendResultsStart**와 함께 전달되지 않습니다. **SendResultsRow**를 사용하여 보낸 이후의 모든 행은 이 메타데이터 정의와 일치해야 합니다.  
  
> [!NOTE]  
>  **SendResultsStart** 메서드를 호출한 후에는 **SendResultsRow** 및 **SendResultsEnd** 만 호출할 수 있습니다. 동일한 **SqlPipe** 인스턴스의 다른 메서드를 호출하면 **InvalidOperationException**이 발생합니다. **SendResultsEnd** 는 **SqlPipe** 를 다른 메서드가 호출될 수 있는 초기 상태로 다시 설정합니다.  
  
### <a name="example"></a>예제  
 **uspGetProductLine** 저장 프로시저는 지정한 제품 라인 내 모든 제품의 이름, 제품 번호, 색 및 목록 가격을 반환합니다. 이 저장 프로시저는 *prodLine*과 정확히 일치하는 항목만 받아들입니다.  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
  
public partial class StoredProcedures  
{  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void uspGetProductLine(SqlString prodLine)  
{  
    // Connect through the context connection.  
    using (SqlConnection connection = new SqlConnection("context connection=true"))  
    {  
        connection.Open();  
  
        SqlCommand command = new SqlCommand(  
            "SELECT Name, ProductNumber, Color, ListPrice " +  
            "FROM Production.Product " +   
            "WHERE ProductLine = @prodLine;", connection);  
  
        command.Parameters.AddWithValue("@prodLine", prodLine);  
  
        try  
        {  
            // Execute the command and send the results to the caller.  
            SqlContext.Pipe.ExecuteAndSend(command);  
        }  
        catch (System.Data.SqlClient.SqlException ex)  
        {  
            // An error occurred executing the SQL command.  
        }  
     }  
}  
};  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Partial Public Class StoredProcedures  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub uspGetProductLine(ByVal prodLine As SqlString)  
    Dim command As SqlCommand  
  
    ' Connect through the context connection.  
    Using connection As New SqlConnection("context connection=true")  
        connection.Open()  
  
        command = New SqlCommand( _  
        "SELECT Name, ProductNumber, Color, ListPrice " & _  
        "FROM Production.Product " & _  
        "WHERE ProductLine = @prodLine;", connection)  
        command.Parameters.AddWithValue("@prodLine", prodLine)  
  
        Try  
            ' Execute the command and send the results   
            ' directly to the caller.  
            SqlContext.Pipe.ExecuteAndSend(command)  
        Catch ex As System.Data.SqlClient.SqlException  
            ' An error occurred executing the SQL command.  
        End Try  
    End Using  
End Sub  
End Class  
```  
  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 투어링용 자전거 제품 목록을 반환하는 **uspGetProduct** 프로시저를 실행합니다.  
  
```  
EXEC uspGetProductLineVB 'T';  
```  
  
## <a name="see-also"></a>참고 항목  
 [SqlDataRecord 개체](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqldatarecord-object.md)   
 [CLR 저장 프로시저](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)   
 [ADO.NET에 대한 SQL Server In-Process 전용 확장](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
