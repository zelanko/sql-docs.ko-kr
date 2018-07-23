---
title: '방법: 단일 트랜잭션 범위 내에서 실행되는 SQL Server 단위 테스트 작성 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: cb241e94-d81c-40e9-a7ae-127762a6b855
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ab996710a0c88d004b36f7bed1e6304a494bc9eb
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39085075"
---
# <a name="how-to-write-a-sql-server-unit-test-that-runs-within-the-scope-of-a-single-transaction"></a>방법: 단일 트랜잭션 범위 내에서 실행되는 SQL Server 단위 테스트 작성
단일 트랜잭션 범위 내에서 실행할 단위 테스트를 수정할 수 있습니다. 이 방법을 사용하는 경우 테스트가 종료된 후 테스트가 실행한 변경 내용을 롤백할 수 있습니다. 다음 절차에서는 아래 작업을 수행하는 방법에 대해 설명합니다.  
  
-   **BEGIN TRANSACTION** 및 **ROLLBACK TRANSACTION**을 사용하는 Transact\-SQL 테스트 스크립트에서 트랜잭션을 만듭니다.  
  
-   테스트 클래스의 단일 테스트 메서드에 대한 트랜잭션을 만듭니다.  
  
-   지정된 테스트 클래스의 모든 테스트 메서드에 대한 트랜잭션을 만듭니다.  
  
**필수 구성 요소**  
  
이 항목의 일부 절차를 실행하기 위해서는 단위 테스트를 실행하는 컴퓨터에서 Distributed Transaction Coordinator 서비스가 실행되고 있어야 합니다. 자세한 내용은 이 항목의 끝에 나오는 절차를 참조하십시오.  
  
## <a name="to-create-a-transaction-using-transact-sql"></a>Transact\-SQL을 사용하여 트랜잭션을 만들려면  
  
#### <a name="to-create-a-transaction-using-transact-sql"></a>Transact\-SQL을 사용하여 트랜잭션을 만들려면  
  
1.  SQL Server 단위 테스트 디자이너에서 단위 테스트를 엽니다. 디자이너를 표시하려면 단위 테스트의 소스 코드 파일을 두 번 클릭합니다.  
  
2.  트랜잭션을 만들 스크립트의 유형을 지정합니다. 예를 들어 테스트 전, 테스트 또는 테스트 후를 지정할 수 있습니다.  
  
3.  Transact\-SQL 편집기에서 테스트 스크립트를 입력합니다.  
  
4.  이 간단한 예제에서와 같이 `BEGIN TRANSACTION` 및 `ROLLBACK TRANSACTION` 문을 삽입합니다. 이 예제에서는 50개의 데이터 행이 포함되어 있는 OrderDetails라는 데이터베이스 테이블을 사용합니다.  
  
    ```  
    BEGIN TRANSACTION TestTransaction  
    UPDATE "OrderDetails" set Quantity = Quantity + 10  
    IF @@ROWCOUNT!=50  
    RAISERROR('Row count does not equal 50',16,1)  
    ROLLBACK TRANSACTION TestTransaction  
    ```  
  
    > [!NOTE]  
    > COMMIT TRANSACTION 문을 실행한 후에는 트랜잭션을 롤백할 수 없습니다.  
  
    ROLLBACK TRANSACTION이 저장 프로시저 및 트리거와 함께 작동하는 방식에 대한 자세한 내용은 Microsoft 웹 사이트의 [ROLLBACK TRANSACTION(Transact-SQL)](http://go.microsoft.com/fwlink/?LinkID=115927) 페이지를 참조하세요.  
  
## <a name="to-create-a-transaction-for-a-single-test-method"></a>단일 테스트 메서드의 트랜잭션을 만들려면  
이 예제에서는 [System.Transactions.TransactionScope](https://docs.microsoft.com/dotnet/api/system.transactions.transactionscope) 형식을 사용할 때 앰비언트 트랜잭션을 사용합니다. 기본적으로 실행 연결 및 권한 있는 연결은 메서드가 실행되기 전에 만들어지므로 이 연결에서는 앰비언트 트랜잭션을 사용하지 않습니다. SqlConnection에는 활성 연결을 트랜잭션에 연결하는 [System.Data.SqlClient.SqlConnection.EnlistTransaction](https://docs.microsoft.com/en-us/dotnet/api/system.data.sqlclient.sqlconnection.enlisttransaction) 메서드가 있습니다. 앰비언트 트랜잭션이 만들어지면 현재 트랜잭션으로 등록되므로 [System.Transactions.Transaction.Current](https://docs.microsoft.com/dotnet/api/system.transactions.transaction.current) 속성을 통해 이 트랜잭션에 액세스할 수 있습니다. 이 예제에서는 앰비언트 트랜잭션이 삭제될 때 트랜잭션이 롤백됩니다. 단위 테스트를 실행할 때 변경된 내용을 커밋하려는 경우 [System.Transactions.TransactionScope.Complete](https://docs.microsoft.com/dotnet/api/system.transactions.transactionscope.complete) 메서드를 호출해야 합니다.  
  
#### <a name="to-create-a-transaction-for-a-single-test-method"></a>단일 테스트 메서드의 트랜잭션을 만들려면  
  
1.  **솔루션 탐색기**에서 테스트 프로젝트의 **참조** 노드를 마우스 오른쪽 단추로 클릭하고 **참조 추가**를 클릭합니다.  
  
    **참조 추가** 대화 상자가 나타납니다.  
  
2.  **.NET** 탭을 클릭합니다.  
  
3.  어셈블리 목록에서 **System.Transactions**를 클릭한 후 **확인**을 클릭합니다.  
  
4.  단위 테스트의 Visual Basic 또는 C# 파일을 엽니다.  
  
5.  다음 Visual Basic 코드 예제에서처럼 테스트 전, 테스트, 테스트 후 작업을 래핑합니다.  
  
    ```  
    <TestMethod()> _  
    Public Sub dbo_InsertTable1Test()  
  
        Using ts as New System.Transactions.TransactionScope( System.Transactions.TransactionScopeOption.Required)  
            ExecutionContext.Connection.EnlistTransaction(Transaction.Current)  
            PrivilegedContext.Connection.EnlistTransaction(Transaction.Current)  
  
            Dim testActions As DatabaseTestActions = Me.dbo_InsertTable1TestData  
            'Execute the pre-test script  
            '  
            System.Diagnostics.Trace.WriteLineIf((Not (testActions.PretestAction) Is Nothing), "Executing pre-test script...")  
            Dim pretestResults() As ExecutionResult = TestService.Execute(Me.PrivilegedContext, Me.PrivilegedContext, testActions.PretestAction)  
            'Execute the test script  
  
            System.Diagnostics.Trace.WriteLineIf((Not (testActions.TestAction) Is Nothing), "Executing test script...")  
            Dim testResults() As ExecutionResult = TestService.Execute(ExecutionContext, Me.PrivilegedContext, testActions.TestAction)  
  
            'Execute the post-test script  
            '  
            System.Diagnostics.Trace.WriteLineIf((Not (testActions.PosttestAction) Is Nothing), "Executing post-test script...")  
            Dim posttestResults() As ExecutionResult = TestService.Execute(Me.PrivilegedContext, Me.PrivilegedContext, testActions.PosttestAction)  
  
            'Because the transaction is not explicitly committed, it  
            'is rolled back when the ambient transaction is   
            'disposed.  
            'To commit the transaction, remove the comment delimiter  
            'from the following statement:  
            'ts.Complete()  
  
    End Sub  
    Private dbo_InsertTable1TestData As DatabaseTestActions  
    ```  
  
    > [!NOTE]  
    > Visual Basic을 사용하고 있는 경우 `Imports Microsoft.VisualStudio.TestTools.UnitTesting`, `Imports Microsoft.VisualStudio.TeamSystem.Data.UnitTesting` 및 `Imports Microsoft.VisualStudio.TeamSystem.Data.UnitTest.Conditions`와 함께 `Imports System.Transactions`를 추가해야 합니다. Visual C#을 사용하고 있는 경우에는 Microsoft.VisualStudio.TestTools, Microsoft.VisualStudio.TeamSystem.Data.UnitTesting 및 Microsoft.VisualStudio.TeamSystem.Data.UnitTesting.Conditions에 대한 `using` 문과 함께 `using System.Transactions`를 추가해야 합니다. 또한 프로젝트에 대한 참조를 해당 어셈블리에 추가해야 합니다.  
  
## <a name="to-create-a-transaction-for-all-test-methods-in-a-test-class"></a>테스트 클래스의 모든 테스트 메서드에 대한 트랜잭션을 만들려면  
  
#### <a name="to-create-a-transaction-for-all-test-methods-in-a-test-class"></a>테스트 클래스의 모든 테스트 메서드에 대한 트랜잭션을 만들려면  
  
1.  단위 테스트의 Visual Basic 또는 C# 파일을 엽니다.  
  
2.  다음 Visual C# 코드 예제에서와 같이 TestInitialize에 트랜잭션을 만들고 TestCleanup에서 트랜잭션을 삭제합니다.  
  
    ```  
    TransactionScope _trans;  
  
            [TestInitialize()]  
            public void Init()  
            {  
                _trans = new TransactionScope();  
                base.InitializeTest();  
            }  
  
            [TestCleanup()]  
            public void Cleanup()  
            {  
                base.CleanupTest();  
                _trans.Dispose();  
            }  
  
            [TestMethod()]  
            public void TransactedTest()  
            {  
                DatabaseTestActions testActions = this.DatabaseTestMethod1Data;  
                // Execute the pre-test script  
                //   
                System.Diagnostics.Trace.WriteLineIf((testActions.PretestAction != null), "Executing pre-test script...");  
                ExecutionResult[] pretestResults = TestService.Execute(this.PrivilegedContext, this.PrivilegedContext, testActions.PretestAction);  
                // Execute the test script  
                //   
                System.Diagnostics.Trace.WriteLineIf((testActions.TestAction != null), "Executing test script...");  
                ExecutionResult[] testResults = TestService.Execute(this.ExecutionContext, this.PrivilegedContext, testActions.TestAction);  
                // Execute the post-test script  
                //   
                System.Diagnostics.Trace.WriteLineIf((testActions.PosttestAction != null), "Executing post-test script...");  
                ExecutionResult[] posttestResults = TestService.Execute(this.PrivilegedContext, this.PrivilegedContext, testActions.PosttestAction);  
  
            }  
    ```  
  
## <a name="to-start-the-distributed-transaction-coordinator-service"></a>Distributed Transaction Coordinator 서비스를 시작하려면  
이 항목의 일부 절차에서는 System.Transactions 어셈블리에 있는 형식을 사용합니다. 이 절차를 수행하기 전에 단위 테스트를 실행하는 컴퓨터에서 Distributed Transaction Coordinator 서비스가 실행되고 있는지 확인해야 합니다. 그렇지 않으면 테스트가 실패하고 “테스트 메서드 *ProjectName*.*TestName*.*MethodName*에서 예외를 throw했습니다. System.Data.SqlClient.SqlException: 서버 ‘*ComputerName*’의 MSDTC를 사용할 수 없습니다.”라는 오류 메시지가 나타납니다.  
  
#### <a name="to-start-the-distributed-transaction-coordinator-service"></a>Distributed Transaction Coordinator 서비스를 시작하려면  
  
1.  **제어판**을 엽니다.  
  
2.  **제어판**에서 **관리 도구**를 엽니다.  
  
3.  **관리 도구**에서 **서비스**를 엽니다.  
  
4.  **서비스** 창에서 **Distributed Transaction Controller** 서비스를 마우스 오른쪽 단추로 클릭하고 **시작**을 클릭합니다.  
  
    서비스의 상태가 **시작됨**으로 업데이트됩니다. 이제 System.Transactions를 사용하는 단위 테스트를 실행할 수 있어야 합니다.  
  
> [!IMPORTANT]  
> Distributed Transaction Controller 서비스를 시작한 경우에도 `System.Transactions.TransactionManagerCommunicationException: Network access for Distributed Transaction Manager (MSDTC) has been disabled. Please enable DTC for network access in the security configuration for MSDTC using the Component Services Administrative tool. ---> System.Runtime.InteropServices.COMException: The transaction manager has disabled its support for remote/network transactions. (Exception from HRESULT: 0x8004D024)` 오류가 나타날 수 있습니다. 이 오류가 나타나면 네트워크 액세스에 대해 Distributed Transaction Controller를 구성해야 합니다. 자세한 내용은 [네트워크 DTC 액세스 사용](http://go.microsoft.com/fwlink/?LinkId=193916)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 단위 테스트 만들기 및 정의](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
  
