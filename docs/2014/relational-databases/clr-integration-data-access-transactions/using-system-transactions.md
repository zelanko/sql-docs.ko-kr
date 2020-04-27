---
title: 시스템 트랜잭션 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TransactionScope class
- Dispose method
- System.Transactions namespace
ms.assetid: 79656ce5-ce46-4c5e-9540-cf9869bd774b
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e39106ea1c4077d1aee90cedc17c5af07503a136
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62919535"
---
# <a name="using-systemtransactions"></a>System.Transactions 사용
  `System.Transactions` 네임스페이스는 이미 통합된 ADO.NET 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CLR(공용 언어 런타임)과 완전히 통합되는 트랜잭션 프레임워크를 제공합니다. `System.Transactions.TransactionScope` 클래스는 연결을 암시적으로 분산 트랜잭션에 등록함으로써 코드 블록에 트랜잭션을 적용합니다. `Complete`로 표시된 코드 블록의 끝에서 `TransactionScope` 메서드를 호출해야 합니다. `Dispose` 메서드는 프로그램 실행이 코드 블록을 종료할 때 호출되며 `Complete` 메서드가 호출되지 않으면 트랜잭션이 중단되도록 합니다. 예외가 발생하여 코드가 범위를 벗어나게 되면 트랜잭션이 중단된 것으로 볼 수 있습니다.  
  
 `using` 블록이 종료될 때 `Dispose` 개체에 대해 `TransactionScope` 메서드가 호출되도록 `using` 블록을 사용하는 것이 좋습니다. `TransactionScope`의 기본 제한 시간은 1분이므로 보류 중인 트랜잭션을 커밋 또는 롤백하지 못하면 성능이 매우 저하됩니다. `using` 문을 사용하지 않는 경우 `Try` 블록에서 모든 작업을 수행하고 `Dispose` 블록에서 명시적으로 `Finally` 메서드를 호출해야 합니다.  
  
 `TransactionScope` 내에서 예외가 발생하면 트랜잭션이 일관성이 없는 것으로 표시되고 중단된 후 `TransactionScope`가 삭제될 때 롤백됩니다. 예외가 발생하지 않으면 참여하는 트랜잭션이 커밋됩니다.  
  
 `TransactionScope`는 로컬 및 원격 데이터 원본 또는 외부 리소스 관리자가 액세스하는 경우에만 사용되어야 합니다. `TransactionScope`는 컨텍스트 연결 내에서만 사용되는 경우에도 항상 트랜잭션을 승격시키기 때문입니다.  
  
> [!NOTE]  
>  `TransactionScope` 클래스는 기본적으로 `System.Transactions.Transaction.IsolationLevel`의 `Serializable`을 사용하여 트랜잭션을 만듭니다. 애플리케이션에 따라서는 애플리케이션에 경합이 많이 발생하지 않도록 격리 수준을 낮추는 방법을 고려할 수 있습니다.  
  
> [!NOTE]  
>  원격 서버에 대한 분산 트랜잭션은 상당히 많은 데이터베이스 리소스를 소비하므로 여기에서는 업데이트, 삽입 및 삭제만 수행해야 합니다. 로컬 서버에서 수행되는 작업에는 분산 트랜잭션이 필요하지 않으며 로컬 트랜잭션으로 충분합니다. SELECT 문은 데이터베이스 리소스를 불필요하게 잠글 수 있으며 일부 시나리오에서는 선택 작업에 트랜잭션을 사용해야 할 수 있습니다. 데이터베이스와 관련이 없는 작업은 트랜잭션된 다른 리소스 관리자와 연관된 경우가 아니면 트랜잭션 범위 밖에서 수행해야 합니다. 트랜잭션의 범위 내에서 예외가 발생하면 트랜잭션이 커밋되지 않지만 `TransactionScope` 클래스는 코드가 트랜잭션 자체의 범위 밖에서 수행한 변경 내용을 롤백하는 기능은 제공하지 않습니다. 트랜잭션이 롤백될 때 몇 가지 동작을 수행해야 하는 경우 직접 `System.Transactions.IEnlistmentNotification` 인터페이스 구현을 작성하고 트랜잭션에 명시적으로 등록해야 합니다.  
  
## <a name="example"></a>예제  
 `System.Transactions`를 사용하려면 System.Transactions.dll 파일에 대한 참조가 있어야 합니다.  
  
 다음 코드에서는 두 가지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대해 승격 가능한 트랜잭션을 만드는 방법을 보여 줍니다. 이러한 인스턴스는 `System.Data.SqlClient.SqlConnection` 블록에 래핑된 두 가지 `TransactionScope` 개체로 표현됩니다. 코드는 `TransactionScope` 문을 사용하여 `using` 블록을 만들고 첫 번째 연결을 엽니다. 이 연결은 자동으로 `TransactionScope`에 등록됩니다. 트랜잭션은 처음에 전체 분산 트랜잭션이 아닌 경량 트랜잭션으로 등록됩니다. 코드는 조건부 논리가 있는 것으로 가정합니다(여기에서는 간단하게 나타내기 위해 생략됨). 코드는 필요한 경우에만 두 번째 연결을 열어 `TransactionScope`에 등록합니다. 연결이 열리면 트랜잭션은 완전 분산 트랜잭션으로 자동 승격됩니다. 그런 다음 `TransactionScope.Complete`를 호출하여 트랜잭션을 커밋합니다. 코드는 연결에 대한 `using` 문을 종료할 때 두 연결을 삭제합니다. `TransactionScope.Dispose`의 `TransactionScope` 메서드는 `using`의 `TransactionScope` 블록이 종료될 때 자동으로 호출됩니다. `TransactionScope` 블록 내의 어떤 부분에서든 예외가 발생하는 경우 `Complete`는 호출되지 않으며 `TransactionScope`가 삭제될 때 분산 트랜잭션이 롤백됩니다.  
  
 Visual Basic  
  
```  
Using transScope As New TransactionScope()  
    Using connection1 As New SqlConnection(connectString1)  
        ' Opening connection1 automatically enlists it in the   
        ' TransactionScope as a lightweight transaction.  
        connection1.Open()  
  
        ' Do work in the first connection.  
  
        ' Assumes conditional logic in place where the second  
        ' connection will only be opened as needed.  
        Using connection2 As New SqlConnection(connectString2)  
            ' Open the second connection, which enlists the   
            ' second connection and promotes the transaction to  
            ' a full distributed transaction.  
            connection2.Open()  
  
            ' Do work in the second connection.  
  
        End Using  
    End Using  
  
    ' Commit the transaction.  
    transScope.Complete()  
End Using  
```  
  
 C#  
  
```  
using (TransactionScope transScope = new TransactionScope())  
{  
    using (SqlConnection connection1 = new   
       SqlConnection(connectString1))  
    {  
        // Opening connection1 automatically enlists it in the   
        // TransactionScope as a lightweight transaction.  
        connection1.Open();  
  
        // Do work in the first connection.  
  
        // Assumes conditional logic in place where the second  
        // connection will only be opened as needed.  
        using (SqlConnection connection2 = new   
            SqlConnection(connectString2))  
        {  
            // Open the second connection, which enlists the   
            // second connection and promotes the transaction to  
            // a full distributed transaction.   
            connection2.Open();  
  
            // Do work in the second connection.  
        }  
    }  
    //  The Complete method commits the transaction.  
    transScope.Complete();  
}  
```  
  
## <a name="see-also"></a>참고 항목  
 [CLR 통합 및 트랜잭션](../native-client-ole-db-transactions/transactions.md)  
  
  
