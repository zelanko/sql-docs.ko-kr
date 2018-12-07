---
title: SQL Server 단위 테스트에서 테스트 조건 사용 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.unittesting.testconditions
ms.assetid: e3d1c86c-1e58-4d2c-b625-d1b591b221aa
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 852651601ba7264c079a42c82a4bbb626d902328
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52529885"
---
# <a name="using-test-conditions-in-sql-server-unit-tests"></a>SQL Server 단위 테스트에서 테스트 조건 사용
SQL Server 단위 테스트에서 하나 이상의 Transact\-SQL 테스트 스크립트가 실행됩니다. 결과는 Transact\-SQL 스크립트와 오류를 반환하고 테스트를 실패 처리하는 데 사용되는 THROW 또는 RAISERROR 내에서 평가할 수 있으며, 결과를 평가하기 위한 테스트 조건을 테스트에 정의할 수 있습니다. 테스트는 [SqlExecutionResult](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.sqlexecutionresult.aspx) 클래스의 인스턴스를 반환합니다. 이 클래스의 인스턴스에는 하나 이상의 데이터 집합, 실행 시간 및 스크립트의 영향을 받는 행이 포함됩니다. 이러한 모든 정보는 스크립트를 실행하는 동안 수집됩니다. 이러한 결과는 테스트 조건을 사용하여 평가될 수 있습니다. SQL Server Data Tools에서는 미리 정의된 테스트 조건의 집합을 제공합니다. 사용자 지정 조건을 작성하고 사용할 수도 있습니다. [SQL Server 단위 테스트의 사용자 지정 테스트 조건](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)을 참조하세요.  
  
## <a name="predefined-test-conditions"></a>미리 정의된 테스트 조건  
다음 표에서는 SQL Server 단위 테스트 디자이너에서 테스트 조건 창을 사용하여 추가할 수 있는 미리 정의된 테스트 조건을 보여 줍니다.  
  
|**테스트 조건**|**테스트 조건 설명**|  
|----------------------|----------------------------------|  
|데이터 체크섬|Transact\-SQL 스크립트에서 반환되는 결과 집합의 체크섬이 필요한 체크섬과 일치하지 않으면 실패합니다. 자세한 내용은 [데이터 체크섬 지정](#SpecifyDataChecksum)을 참조하십시오.<br /><br />**참고:** 테스트 실행 간에 다른 데이터를 반환하는 경우에는 이 테스트 조건을 사용하지 않는 것이 좋습니다. 예를 들어 결과 집합에 생성된 날짜나 시간이 포함되어 있거나 ID 열이 포함되어 있으면 각 실행 시 체크섬이 다르므로 테스트가 실패합니다.|  
|빈 ResultSet|Transact\-SQL 스크립트에서 반환되는 결과 집합이 비어 있지 않으면 실패합니다.|  
|실행 시간|Transact\-SQL 테스트 스크립트를 실행하는 데 예상보다 오래 걸리면 실패합니다. 기본 실행 시간은 30초입니다.<br /><br />실행 시간은 테스트 전 스크립트나 테스트 후 스크립트가 아닌 테스트 스크립트 테스트에만 적용됩니다.|  
|필요한 스키마|결과 집합의 열 및 데이터 형식이 테스트 조건에 대해 지정된 열 및 데이터 형식과 일치하지 않으면 실패합니다. 테스트 조건의 속성을 통해 스키마를 지정해야 합니다. 자세한 내용은 [필요한 스키마 지정](#SpecifyExpectedSchema)을 참조하십시오.|  
|결과 불충분|항상 결과 불충분이라는 결과의 테스트를 생성합니다. 결과 불충분은 모든 테스트에 추가된 기본 조건입니다. 이 테스트 조건은 테스트 확인이 구현되지 않았음을 나타내기 위해 포함됩니다. 이 테스트 조건은 다른 테스트 조건을 추가한 후 테스트에서 삭제합니다.|  
|비어 있지 않은 ResultSet|결과 집합이 비어 있으면 실패합니다. 이 테스트 조건을 사용하거나 테스트 스크립트에 Transact\-SQL @@RAISERROR 함수와 함께 EmptyResultSet을 사용하여 업데이트가 제대로 작동했는지 여부를 테스트할 수 있습니다. 예를 들어 업데이트 전 값을 저장하고 업데이트를 실행하고 업데이트 후 값을 비교한 다음 예상 결과를 얻지 못하면 오류를 발생시킬 수 있습니다.|  
|행 개수|결과 집합에 예상 행 수가 포함되어 있지 않으면 실패합니다.|  
|스칼라 값|결과 집합의 특정 값이 지정된 값과 같지 않으면 실패합니다. 기본 **예상 값** 은 null입니다.|  
  
> [!NOTE]  
> 실행 시간 테스트 조건은 Transact\-SQL 테스트 스크립트를 실행해야 하는 시간 제한을 지정합니다. 이 제한 시간을 초과하는 경우 테스트가 실패합니다. 테스트 결과에는 실행 시간 테스트 조건과는 다른 지속 시간 통계도 포함됩니다. 지속 시간 통계에는 실행 시간뿐 아니라 데이터베이스에 두 번 연결하는 데 걸리는 시간이 포함됩니다. 한 번은 테스트 전 스크립트 및 테스트 후 스크립트와 같은 다른 테스트 스크립트를 실행하는 데 걸리는 시간이고 또 한 번은 테스트 조건을 실행하는 데 걸리는 시간입니다. 따라서 지속 시간이 실행 시간보다 긴 경우에도 테스트가 통과될 수 있습니다.  
>   
> 데이터 생성 및 스키마 배포는 테스트가 실행되기 전에 발생하므로 데이터 생성 및 스키마 배포에 사용된 시간은 보고되는 지속 시간에 포함되지 않습니다. 테스트 지속 시간을 보려면 **테스트 결과** 창에서 테스트 실행을 선택하고 마우스 오른쪽 단추를 선택한 후 **테스트 결과 정보 보기**를 선택합니다.  
  
SQL Server 단위 테스트 디자이너의 테스트 조건 창을 사용하여 SQL Server 단위 테스트에 테스트 조건을 추가할 수 있습니다. 자세한 내용은 [방법: SQL Server 단위 테스트에 테스트 조건 추가](../ssdt/how-to-add-test-conditions-to-sql-server-unit-tests.md)를 참조하세요.  
  
직접 테스트 메서드 코드를 편집하여 기능을 추가할 수도 있습니다. 자세한 내용은 [방법: 편집할 SQL Server 단위 테스트 열기](../ssdt/how-to-open-a-sql-server-unit-test-to-edit.md) 및 [방법: 단일 트랜잭션 범위 내에서 실행되는 SQL Server 단위 테스트 작성](../ssdt/how-to-write-sql-server-unit-test-that-runs-in-single-transaction-scope.md)을 참조하세요. 예를 들어 Assert 문을 추가하여 테스트 메서드에 기능을 추가할 수 있습니다. 자세한 내용은 [SQL Server 단위 테스트에서 Transact-SQL 어설션 사용](../ssdt/using-transact-sql-assertions-in-sql-server-unit-tests.md)을 참조하세요.  
  
## <a name="expected-failures"></a>예상 실패  
성공해서는 안 되는 테스트 동작을 테스트하는 SQL Server 단위 테스트를 만들 수 있습니다. 이러한 예상 실패를 부정적 테스트라고도 합니다. 다음과 같은 몇 가지 예가 있습니다.  
  
-   잘못된 고객 ID를 지정하는 경우 고객의 데이터를 삭제하는 저장 프로시저가 실패하는지 확인합니다.  
  
-   주문이 접수되지 않았거나 주문이 이미 찬 경우 주문을 채우는 저장 프로시저가 실패하는지 확인합니다.  
  
-   주문을 취소하는 저장 프로시저가 완료된 주문 또는 이미 취소된 주문을 취소할 수 없는지 확인합니다.  
  
저장 프로시저에 대해 예상된 SQL 예외를 발생시키는 SQL Server 단위 테스트를 정의할 수 있습니다. 단위 테스트 메서드에 특성을 추가하여 예상된 예외를 나타낼 수 있습니다. 이를 통해 예외가 발생할 때 테스트가 실패하지 않도록 방지할 수 있습니다.  
  
SQL Server 단위 테스트 메서드를 예상된 예외로 표시하려면 다음 특성을 추가합니다.  
  
```  
[ExpectedSqlException(MessageNumber = nnnnn, Severity = x, MatchFirstError = false, State = y)]  
```  
  
각 항목이 나타내는 의미는 다음과 같습니다.  
  
-   *nnnnn* 은 예상 메시지 수(예: 14025)입니다.  
  
-   *x* 는 예상된 예외의 심각도입니다.  
  
-   *y* 는 예상된 예외의 상태입니다.  
  
지정되지 않은 매개 변수는 무시됩니다. 이러한 매개 변수를 데이터베이스 코드의 **THROW** 문에 전달합니다. MatchFirstError = false로 지정하는 경우 특성은 예외의 SqlError 중 하나와 일치합니다. 기본 동작(MatchFirstError = true)은 발생한 첫 번째 오류만 일치시키는 것입니다.  
  
예상된 예외와 부정 SQL Server 단위 테스트를 사용하는 방법에 대한 예를 보려면 [연습: SQL Server 단위 테스트 만들기 및 실행](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md)을 참조하세요.  
  
## <a name="SpecifyDataChecksum"></a>데이터 체크섬 지정  
SQL Server 단위 테스트 디자이너를 표시하려면 **솔루션 탐색기**에서 SQL Server 단위 테스트 소스 코드 파일을 두 번 클릭합니다.  
  
데이터베이스 단위 테스트에 데이터 체크섬 테스트 조건을 추가한 후에는 다음 절차를 사용하여 필요한 체크섬을 구성해야 합니다.  
  
#### <a name="to-specify-an-expected-checksum"></a>필요한 체크섬을 지정하려면  
  
1.  테스트 조건 목록에서 체크섬을 지정할 데이터 체크섬 테스트 조건을 클릭합니다.  
  
2.  F4 키를 눌러 **속성** 창을 엽니다. **보기** 메뉴를 열고 **속성** 창을 클릭할 수도 있습니다.  
  
3.  (옵션) 테스트 조건의 **(이름)** 속성을 설명이 포함된 이름으로 변경할 수도 있습니다.  
  
4.  **구성** 속성에서 찾아보기 단추(**…**)를 클릭합니다.  
  
    **TestConditionName에 대한 구성** 대화 상자가 나타납니다.  
  
5.  테스트할 데이터베이스에 대한 연결을 지정합니다. 자세한 내용은 [방법: 데이터베이스 연결 만들기](https://msdn.microsoft.com/library/aa833420(VS.100).aspx)를 참조하세요.  
  
6.  기본적으로 편집 창에는 테스트의 Transact\-SQL 본문이 나타납니다. 필요한 경우 예상 결과를 만들도록 코드를 수정할 수 있습니다. 예를 들어 테스트에 테스트 전 코드가 있는 경우 해당 코드를 추가해야 할 수 있습니다.  
  
    > [!IMPORTANT]  
    > 이전에 체크섬을 지정한 체크섬 조건을 수정하면 편집 창에서 변경한 내용이 모두 저장되지 않습니다. **검색**을 클릭하기 전에 해당 변경 작업을 다시 수행해야 합니다.  
  
7.  **검색**을 클릭합니다.  
  
    지정된 데이터베이스 연결에 대해 Transact\-SQL이 실행되고 대화 상자에 결과가 나타납니다.  
  
8.  결과가 테스트의 예상 결과와 일치하면 **확인**을 클릭합니다. 그렇지 않으면 예상 결과를 얻을 때까지 Transact\-SQL 본문을 수정하고 6, 7, 8단계를 반복합니다.  
  
    테스트 조건의 **값** 열에 필요한 체크섬 값이 표시됩니다.  
  
## <a name="SpecifyExpectedSchema"></a>필요한 스키마 지정  
SQL Server 단위 테스트에 필요한 스키마 테스트 조건을 추가한 후에는 다음 절차를 따라 필요한 스키마를 구성해야 합니다.  
  
#### <a name="to-specify-an-expected-schema"></a>필요한 스키마를 지정하려면  
  
1.  테스트 조건 목록에서 스키마를 지정할 필요한 스키마 테스트 조건을 클릭합니다.  
  
2.  F4 키를 눌러 **속성** 창을 엽니다. **보기** 메뉴를 열고 **속성** 창을 클릭할 수도 있습니다.  
  
3.  (옵션) 테스트 조건의 **(이름)** 속성을 설명이 포함된 이름으로 변경할 수도 있습니다.  
  
4.  **구성** 속성에서 찾아보기 단추(**…**)를 클릭합니다.  
  
    **TestConditionName에 대한 구성** 대화 상자가 나타납니다.  
  
5.  테스트할 데이터베이스에 대한 연결을 지정합니다. 자세한 내용은 [방법: 데이터베이스 연결 만들기](https://msdn.microsoft.com/library/aa833420(VS.100).aspx)를 참조하세요.  
  
6.  기본적으로 편집 창에는 테스트의 Transact\-SQL 본문이 나타납니다. 필요한 경우 예상 결과를 만들도록 코드를 수정할 수 있습니다. 예를 들어 테스트에 테스트 전 코드가 있는 경우 해당 코드를 추가해야 할 수 있습니다.  
  
    > [!IMPORTANT]  
    > 이전에 스키마를 지정한 필요한 스키마 조건을 수정하면 편집 창에서 변경한 내용이 모두 저장되지 않습니다. **검색**을 클릭하기 전에 해당 변경 작업을 다시 수행해야 합니다.  
  
7.  **검색**을 클릭합니다.  
  
    지정된 데이터베이스 연결에 대해 Transact\-SQL이 실행되고 대화 상자에 결과가 나타납니다. 결과 값을 확인하는 것이 아니라 결과 집합의 스키마 또는 모양을 확인하므로 열이 예상대로 나타나면 반환된 결과 데이터를 확인할 필요가 없습니다.  
  
8.  결과가 테스트의 예상 결과와 일치하면 **확인**을 클릭합니다. 그렇지 않으면 예상 결과를 얻을 때까지 Transact\-SQL 본문을 수정하고 6, 7, 8단계를 반복합니다.  
  
    테스트 조건의 **값** 열에 필요한 스키마에 대한 정보가 표시됩니다. 예를 들어 "예상: 테이블 2개"라고 표시될 수 있습니다.  
  
## <a name="extensible-test-conditions"></a>확장 가능한 테스트 조건  
미리 정의된 6개의 테스트 조건 이외에 새 테스트 조건을 직접 작성할 수 있습니다. 이러한 테스트 조건은 SQL Server 단위 테스트 디자이너의 [테스트 조건] 창에 표시됩니다. 자세한 내용은 [SQL Server 단위 테스트의 사용자 지정 테스트 조건](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 단위 테스트 만들기 및 정의](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[SQL Server 단위 테스트에서 Transact-SQL 어설션 사용](../ssdt/using-transact-sql-assertions-in-sql-server-unit-tests.md)  
[SQL Server 단위 테스트의 스크립트](../ssdt/scripts-in-sql-server-unit-tests.md)  
  
