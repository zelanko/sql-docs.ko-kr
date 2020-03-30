---
title: MSSQLSERVER_4186 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 4186 (Database Engine error)
ms.assetid: 1ae88554-f291-45bc-a186-6f41d9cd0fca
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3efa12b744d331949fc0af18f555e603f18e33ab
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68123095"
---
# <a name="mssqlserver_4186"></a>MSSQLSERVER_4186
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|4186|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름||  
|메시지 텍스트|열 '%ls.%.*ls'의 정의가 하위 쿼리를 포함하거나 사용자 또는 시스템 데이터에 액세스하는 함수를 참조하므로 OUTPUT 절에서 해당 열을 참조할 수 없습니다. 함수가 스키마 바인딩되지 않으면 기본적으로 데이터 액세스를 수행하도록 간주됩니다. 열 정의에서 하위 쿼리나 함수를 제거하거나 OUTPUT 절에서 열을 제거하십시오.|  
  
## <a name="explanation"></a>설명  
비결정적 동작을 방지하기 위해 OUTPUT 절은 뷰 또는 인라인 테이블 반환 함수의 열이 다음 중 한 가지 방법으로 정의된 경우 이러한 열을 참조할 수 없습니다.  
  
-   하위 쿼리  
  
-   사용자 또는 시스템 데이터 액세스를 수행하거나 이러한 액세스를 수행하는 것으로 간주되는 사용자 정의 함수  
  
-   해당 정의에서 사용자 또는 시스템 데이터 액세스를 수행하는 사용자 정의 함수가 포함된 계산 열  
  
### <a name="examples"></a>예  
**하위 쿼리에 의해 정의되는 뷰 열**  
  
다음 예에서는 열 `State`를 정의하기 위해 선택 목록에 있는 하위 쿼리를 사용하는 뷰를 만듭니다. 그러면 UPDATE 문이 OUTPUT 절의 `State` 열을 참조하지만 선택 목록의 하위 쿼리로 인해 실패합니다.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE VIEW dbo.V1  
AS  
    SELECT City,  
-- subquery to return the State name  
           (SELECT Name FROM Person.StateProvince AS sp   
            WHERE sp.StateProvinceID = a.StateProvinceID) AS State  
    FROM Person.Address AS a;  
GO  
--Reference the State column in the OUTPUT clause of an UPDATE statement  
UPDATE dbo.V1   
SET City = City + 'Test'   
OUTPUT deleted.City, deleted.State, inserted.City, inserted.State  
WHERE State = 'Texas';  
GO  
```  
  
**함수에 의해 정의되는 뷰 열**  
  
다음 예제에서는 열 `dbo.ufnGetStock`를 정의하기 위해 선택 목록에 있는 데이터 액세스 스칼라 함수 `CurrentInventory`을 사용하는 뷰를 만듭니다. 그러면 UPDATE 문이 OUTPUT 절의 `CurrentInventory` 열을 참조합니다.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE VIEW Production.ReorderLevels  
AS  
    SELECT ProductID, ProductModelID, ReorderPoint,  
           dbo.ufnGetStock(ProductID) AS CurrentInventory  
    FROM Production.Product;  
GO  
  
UPDATE Production.ReorderLevels  
SET ReorderPoint += CurrentInventory  
OUTPUT deleted.ReorderPoint, deleted.CurrentInventory,  
       inserted.ReorderPoint, inserted.CurrentInventory  
WHERE ProductModelID BETWEEN 75 and 80;  
```  
  
## <a name="user-action"></a>사용자 동작  
다음과 같은 방법으로 오류 4186을 해결할 수 있습니다.  
  
-   하위 쿼리 대신 조인을 사용하여 뷰 또는 함수의 열을 정의합니다. 예를 들어 다음과 같이 뷰 `dbo.V1`을 다시 작성할 수 있습니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE VIEW dbo.V1  
    AS  
        SELECT City, sp.Name AS State  
        FROM Person.Address AS a   
        JOIN Person.StateProvince AS sp   
        ON sp.StateProvinceID = a.StateProvinceID;  
    ```  
  
-   사용자 정의 함수의 정의를 검사합니다. 사용자 정의 함수가 사용자 또는 시스템 액세스를 수행하지 않으면 WITH SCHEMABINDING 절을 포함하도록 함수를 변경합니다.  
  
-   OUTPUT 절에서 열을 제거합니다.  
  
## <a name="see-also"></a>참고 항목  
[OUTPUT 절&#40;Transact-SQL&#41;](~/t-sql/queries/output-clause-transact-sql.md)  
  
