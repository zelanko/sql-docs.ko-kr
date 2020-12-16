---
title: 현재 트랜잭션 액세스 | Microsoft Docs
description: CLR 통합 SQL Server에서 current 속성을 사용 하면 현재 트랜잭션에 액세스할 수 있습니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- current transaction access
- Current property
- Transaction class
ms.assetid: 1a4e2ce5-f627-4c81-8960-6a9968cefda2
author: rothja
ms.author: jroth
ms.openlocfilehash: b9220519a926ca75a00843dba54dfad797064aee
ms.sourcegitcommit: 52252e8b4c9b50d3915aecd3135e8901d345e7e2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97599850"
---
# <a name="accessing-the-current-transaction"></a>현재 트랜잭션 액세스
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 실행되는 CLR(공용 언어 런타임) 코드를 입력하는 시점에 트랜잭션이 활성 상태인 경우 트랜잭션은 **System.Transactions.Transaction** 클래스를 통해 표시됩니다. **Transaction.Current** 속성은 현재 트랜잭션에 액세스하는 데 사용됩니다. 대부분의 경우 트랜잭션에 명시적으로 액세스할 필요가 없습니다. 데이터베이스 연결의 경우 ADO.NET에서는 **Transaction.Current** 메서드를 호출할 때 **Connection.Open** 를 자동으로 검사하고 연결 문자열에서 **Enlist** 키워드가 false로 설정되지 않은 경우 연결을 트랜잭션에 투명하게 참여시킵니다.  
  
 다음 시나리오에서는 **Transaction** 개체를 직접 사용할 수 있습니다.  
  
-   자동 참여를 수행하지 않거나 초기화 동안 몇 가지 이유로 참여하지 못한 리소스를 참여시키려는 경우  
  
-   리소스를 트랜잭션에 명시적으로 참여시키려는 경우  
  
-   저장 프로시저 또는 함수 내에서 외부 트랜잭션을 종료하려는 경우. 이 경우에는 <xref:System.Transactions.TransactionScope>를 사용합니다. 예를 들어 다음 코드에서는 현재 트랜잭션을 롤백합니다.  
  
    ```  
    using(TransactionScope transactionScope = new TransactionScope(TransactionScopeOptions.Required)) { }  
    ```  
  
 이 항목의 나머지 부분에서는 외부 트랜잭션을 취소하는 다른 방법에 대해 설명합니다.  
  
## <a name="canceling-an-external-transaction"></a>외부 트랜잭션 취소  
 관리되는 프로시저나 함수에서 다음과 같은 방법으로 외부 트랜잭션을 취소할 수 있습니다.  
  
-   관리되는 프로시저나 함수에서 출력 매개 변수를 사용하여 값을 반환할 수 있습니다. 호출 하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로시저는 반환 된 값을 확인 하 고, 해당 하는 경우 **ROLLBACK TRANSACTION** 을 실행할 수 있습니다.  
  
-   관리되는 프로시저나 함수에서 사용자 지정 예외를 throw할 수 있습니다. 호출 하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로시저는 try/catch 블록의 관리 되는 프로시저 또는 함수에서 throw 된 예외를 catch 하 고 **ROLLBACK TRANSACTION** 을 실행할 수 있습니다.  
  
-   관리되는 프로시저나 함수에서 특정 조건에 맞는 경우 **Transaction.Rollback** 메서드를 호출하여 현재 트랜잭션을 취소할 수 있습니다.  
  
 관리되는 프로시저나 함수 내에서 호출할 경우 **Transaction.Rollback** 메서드는 모호한 오류 메시지와 함께 예외를 throw하고 try/catch 블록에 래핑될 수 있습니다. 오류 메시지는 다음과 유사 합니다.  
  
```  
Msg 3994, Level 16, State 1, Procedure uspRollbackFromProc, Line 0  
Transaction is not allowed to roll back inside a user defined routine, trigger or aggregate because the transaction is not started in that CLR level. Change application logic to enforce strict transaction nesting.  
```  
  
 이 예외는 예상된 것이며, 코드 실행을 계속하려면 try/catch 블록이 필요합니다. try/catch 블록이 없으면 즉시 예외가 호출 [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로시저로 throw되고 관리되는 코드 실행이 완료됩니다. 관리되는 코드 실행이 완료되면 다른 예외가 발생합니다.  
  
```  
Msg 3991, Level 16, State 1, Procedure uspRollbackFromProc, Line 1   
The context transaction which was active before entering user defined routine, trigger or aggregate " uspRollbackFromProc " has been ended inside of it, which is not allowed. Change application logic to enforce strict transaction nesting. The statement has been terminated.  
```  
  
 이 예외도 예상된 것이며 실행을 계속하려면 트리거를 발생시키는 동작을 수행하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 try/catch 블록으로 둘러싸야 합니다. 두 가지 예외가 throw되지만 트랜잭션이 롤백되고 변경 내용이 커밋되지 않습니다.  
  
### <a name="example"></a>예제  
 다음은 **Transaction.Rollback** 메서드를 사용하여 관리되는 프로시저에서 트랜잭션을 롤백하는 예입니다. 관리되는 코드에서 **Transaction.Rollback** 메서드는 try/catch 블록으로 둘러싸여 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트는 어셈블리 및 관리되는 저장 프로시저를 만듭니다. 관리되는 프로시저 실행이 완료될 때 throw되는 예외가 catch되도록 **EXEC uspRollbackFromProc** 문이 try/catch 블록에 래핑됩니다.  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
using System.Transactions;  
  
public partial class StoredProcedures  
{  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void uspRollbackFromProc()  
{  
   using (SqlConnection connection = new SqlConnection(@"context connection=true"))  
   {  
      // Open the connection.  
      connection.Open();  
  
      bool successCondition = true;  
  
      // Success condition is met.  
      if (successCondition)  
      {  
         SqlContext.Pipe.Send("Success condition met in procedure.");   
         // Perform other actions here.  
      }  
  
      //  Success condition is not met, the transaction will be rolled back.  
      else  
      {  
         SqlContext.Pipe.Send("Success condition not met in managed procedure. Transaction rolling back...");  
         try  
         {  
               // Get the current transaction and roll it back.  
               Transaction trans = Transaction.Current;  
               trans.Rollback();  
         }  
         catch (SqlException ex)  
         {  
            // Catch the expected exception.   
            // This allows the connection to close correctly.                      
         }    
      }  
  
      // Close the connection.  
      connection.Close();  
   }  
}  
};  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Transactions  
  
Partial Public Class StoredProcedures  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub  uspRollbackFromProc ()  
   Using connection As New SqlConnection("context connection=true")  
  
   ' Open the connection.  
   connection.Open()  
  
   Dim successCondition As Boolean  
   successCondition = False  
  
   ' Success condition is met.  
   If successCondition Then  
  
      SqlContext.Pipe.Send("Success condition met in procedure.")  
  
      ' Success condition is not met, the transaction will be rolled back.  
  
   Else  
      SqlContext.Pipe.Send("Success condition not met in managed procedure. Transaction rolling back...")  
      Try  
         ' Get the current transaction and roll it back.  
         Dim trans As Transaction  
         trans = Transaction.Current  
         trans.Rollback()  
  
      Catch ex As SqlException  
         ' Catch the exception instead of throwing it.    
         ' This allows the connection to close correctly.                      
      End Try  
  
   End If  
  
   ' Close the connection.  
   connection.Close()  
  
End Using  
End Sub  
End Class  
```  
  
 **Transact-SQL**  
  
```  
--Register assembly.  
CREATE ASSEMBLY TestProcs FROM 'C:\Programming\TestProcs.dll'   
Go  
CREATE PROCEDURE uspRollbackFromProc AS EXTERNAL NAME TestProcs.StoredProcedures.uspRollbackFromProc  
Go  
  
-- Execute procedure.  
BEGIN TRY  
BEGIN TRANSACTION   
-- Perform other actions.  
Exec uspRollbackFromProc  
-- Perform other actions.  
PRINT N'Commiting transaction...'  
COMMIT TRANSACTION  
END TRY  
  
BEGIN CATCH  
SELECT ERROR_NUMBER() AS ErrorNum, ERROR_MESSAGE() AS ErrorMessage  
PRINT N'Exception thrown, rolling back transaction.'  
ROLLBACK TRANSACTION  
PRINT N'Transaction rolled back.'   
END CATCH  
Go  
  
-- Clean up.  
DROP Procedure uspRollbackFromProc;  
Go  
DROP ASSEMBLY TestProcs;  
Go  
```  
  
## <a name="see-also"></a>참고 항목  
 [CLR 통합 및 트랜잭션](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
