---
title: SQL Server 단위 테스트에서 Transact-SQL 어설션 사용 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 55d8be9c-9282-47d3-be7f-e2c26f00c95e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8da09c20837b060606b087c0edebb7bf9713675e
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51671250"
---
# <a name="using-transact-sql-assertions-in-sql-server-unit-tests"></a>SQL Server 단위 테스트에서 Transact-SQL 어설션 사용
SQL Server 단위 테스트에서는 Transact\-SQL 테스트 스크립트가 실행되어 결과를 반환합니다. 결과가 결과 집합으로 반환되는 경우도 있습니다. 테스트 조건을 사용하면 결과의 유효성을 검사할 수 있습니다. 예를 들어 테스트 조건을 사용하여 특정 결과 집합에서 반환되는 행 수를 확인하거나 특정 테스트가 실행되는 데 걸린 시간을 확인할 수 있습니다. 테스트 조건에 대한 자세한 내용은 [SQL Server 단위 테스트에서 테스트 조건 사용](../ssdt/using-test-conditions-in-sql-server-unit-tests.md)을 참조하세요.  
  
테스트 조건을 사용하는 대신 Transact\-SQL 스크립트에서 Transact\-SQL 어설션, 즉 THROW 또는 RAISERROR 문을 사용할 수도 있습니다. 특정 환경에서는 테스트 조건 대신 Transact\-SQL 어설션을 사용해야 할 수 있습니다.  
  
## <a name="using-transact-sql-assertions"></a>Transact-SQL 어설션 사용  
Transact\-SQL 어설션을 사용하거나 테스트 조건을 사용하여 데이터의 유효성을 검사할지 결정하려면 먼저 다음 사항을 고려해야 합니다.  
  
-   **성능**. 먼저 데이터를 클라이언트 컴퓨터로 이동하고 이를 로컬로 조작하는 것보다는 서버에서 Transact\-SQL 어설션을 실행하는 것이 더 빠릅니다.  
  
-   **언어에 대한 친밀성**. 사용자의 현재 전문 기술 기반의 특정 언어 선호도에 따라 Transact\-SQL 어설션이나 Visual C\# 또는 Visual Basic 테스트 조건 중에서 선택할 수 있습니다.  
  
-   **복잡한 유효성 검사**. 일부 경우에는 Visual C\# 또는 Visual Basic에서 보다 복잡한 테스트를 빌드하고 클라이언트에서 테스트의 유효성을 검사할 수 있습니다.  
  
-   **단순성**. 일부 경우에는 미리 정의된 테스트 조건을 사용하는 편이 Transact\-SQL에서 동일한 스크립트를 작성하는 것보다 더 간단할 수 있습니다.  
  
-   **레거시 유효성 검사 라이브러리**. 유효성 검사를 수행하는 코드가 이미 있는 경우 SQL Server 단위 테스트에서 테스트 조건을 사용하는 대신 이 코드를 사용할 수 있습니다.  
  
## <a name="mark-unit-test-methods-with-the-expected-exception"></a>단위 테스트 메서드에 예상된 예외 표시  
SQL Server 단위 테스트 메서드를 예상된 예외로 표시하려면 다음 특성을 추가합니다.  
  
```vb  
<ExpectedSqlException(MessageNumber=nnnnn, Severity=x, MatchFirstError=false, State=y)> _  
```  
  
```csharp  
[ExpectedSqlException(MessageNumber=nnnnn, Severity=x, MatchFirstError=false, State=y)]  
```  
  
각 항목이 나타내는 의미는 다음과 같습니다.  
  
-   *nnnnn* 은 예상 메시지 수(예: 14025)입니다.  
  
-   *x* 는 예상된 예외의 심각도입니다.  
  
-   *y* 는 예상된 예외의 상태입니다.  
  
지정되지 않은 매개 변수는 무시됩니다. 이러한 매개 변수는 데이터베이스 코드의 RAISERROR 문에 전달합니다. MatchFirstError = true를 지정한 경우 특성이 예외의 모든 SqlErrors와 일치합니다. 기본 동작(MatchFirstError = true)은 발생한 첫 번째 오류만 일치시키는 것입니다.  
  
예상된 예외와 부정 SQL Server 단위 테스트를 사용하는 방법에 대한 예를 보려면 [연습: SQL Server 단위 테스트 만들기 및 실행](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md)을 참조하세요.  
  
## <a name="the-raiserror-statement"></a>RAISERROR 문  
  
> [!NOTE]  
> RAISERROR 대신 THROW를 사용하십시오. 이제 RAISERROR는 더 이상 사용되지 않습니다.  
  
Transact\-SQL 스크립트에서 RAISERROR 문을 사용하여 서버에서 Transact\-SQL 어설션을 직접 사용할 수 있습니다. 구문은 다음과 같습니다.  
  
**RAISERROR (@ErrorMessage, @ErrorSeverity, @ErrorState)**  
  
각 항목이 나타내는 의미는 다음과 같습니다.  
  
@ErrorMessage는 사용자 정의 오류 메시지입니다. 이 메시지 문자열은 printf_s 함수와 비슷하게 형식을 지정할 수 있습니다.  
  
@ErrorSeverity는 0~18의 사용자 정의 심각도 수준입니다.  
  
> [!NOTE]  
> 심각도 수준 값 ‘0’과 ‘10’에서는 SQL Server 단위 테스트가 실패하지 않습니다. 테스트를 실패하도록 하려면 0~18 사이의 다른 모든 값을 사용할 수 있습니다.  
  
@ErrorState는 1~127 사이의 임의 정수입니다. 이 정수를 사용하여 코드의 서로 다른 위치에서 발생한 단일 오류를 구분할 수 있습니다.  
  
자세한 내용은 [RAISERROR(Transact-SQL)](https://msdn.microsoft.com/library/ms178592.aspx)를 참조하세요. SQL Server 단위 테스트에서 RAISERROR를 사용하는 예는 [방법: 단일 트랜잭션 범위 내에서 실행되는 SQL Server 단위 테스트 작성](../ssdt/how-to-write-sql-server-unit-test-that-runs-in-single-transaction-scope.md) 항목에서 제공됩니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 단위 테스트 만들기 및 정의](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[SQL Server 단위 테스트에서 테스트 조건 사용](../ssdt/using-test-conditions-in-sql-server-unit-tests.md)  
[SQL Server 단위 테스트를 사용하여 데이터베이스 코드 확인](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
[방법: 편집할 SQL Server 단위 테스트 열기](../ssdt/how-to-open-a-sql-server-unit-test-to-edit.md)  
  
