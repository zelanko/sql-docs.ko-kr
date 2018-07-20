---
title: '방법: 쿼리를 사용하여 기존 테이블 편집 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 58f4de8e-97b4-4bcb-953f-f3d428432491
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b8a5814bf073891006b6f2a1917459f9b711482f
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37094720"
---
# <a name="how-to-edit-an-existing-table-using-queries"></a>방법: 쿼리를 사용하여 기존 테이블 편집
Transact\-SQL 쿼리를 작성하여 테이블 또는 테이블 데이터의 정의를 편집할 수 있습니다. 테이블의 데이터를 보거나 비주얼 환경에서 입력하려면 [연결된 데이터베이스 개발](../ssdt/connected-database-development.md)에 설명된 대로 데이터 편집기를 사용합니다.  
  
> [!WARNING]  
> 다음 절차에서는 이전의 [연결된 데이터베이스 개발](../ssdt/connected-database-development.md) 섹션에 나오는 절차에서 만든 엔터티를 사용합니다.  
  
### <a name="to-edit-the-definition-of-an-existing-table"></a>기존 테이블의 정의를 편집하려면  
  
1.  **SQL Server 개체 탐색기**에서 **Trade** 데이터베이스의 **테이블** 노드를 확장하고 **dbo.Suppliers**를 마우스 오른쪽 단추로 클릭합니다.  
  
2.  **디자이너 보기**를 선택하여 테이블 디자이너에서 테이블 스키마를 봅니다.  
  
3.  **Address** 열에 대한 **Null 허용** 상자를 선택합니다. 스크립트 창의 해당 코드가 즉시 `NULL`로 변경됩니다.  
  
4.  [방법: 파워 버퍼를 사용하여 연결된 데이터베이스 업데이트](../ssdt/how-to-update-a-connected-database-with-power-buffer.md) 항목의 단계에 따라 데이터베이스를 업데이트합니다.  
  
### <a name="to-populate-data-in-new-tables-using-a-transact-sql-query"></a>Transact\-SQL 쿼리를 사용하여 새 테이블에 데이터를 채우려면  
  
1.  **Trade** 데이터베이스 노드를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다.  
  
2.  스크립트 창에서 다음 코드를 붙여 넣습니다.  
  
    ```  
    insert into dbo.Suppliers values  
    (1, 'NorthWind Traders', 'Seattle, WA'),  
    (2, 'Contoso', 'Tacoma, WA')  
    GO  
  
    insert dbo.Customer values  
    (1, 'Fourth Coffee')  
    GO  
  
    insert dbo.Products values  
    (1, 'Apples', 0, 1, 1),  
    (2, 'Instant Coffee', 1, 2, 1)  
    GO  
    ```  
  
3.  **쿼리 실행** 단추를 클릭하여 이 쿼리를 실행합니다. **메시지** 창의 다음 메시지는 행이 테이블에 올바르게 추가되었음을 나타냅니다.  
  
**(2개 행이 영향을 받음)(1개 행이 영향을 받음)(2개 행이 영향을 받음)**  
  
4.  스크립트 창의 코드를 다음 코드로 바꾸고 쿼리를 실행합니다. 이 코드는 `Products` 테이블에 `ShelfLife`가 6인 새 행을 추가하려고 시도합니다.  
  
    ```  
    insert dbo.Products values  
    (3, 'Potato Chips', 6, 1, 1)  
    GO  
    ```  
  
5.  **메시지** 창에 `INSERT` 문이 `ShelfLife` 값을 5 미만으로 제한하는 기존 CHECK 제약 조건과 충돌한다는 메시지가 표시됩니다. 기존 제약 조건에 맞지 않는 문으로 인해 Products 테이블이 업데이트되지 않습니다.  
  
6.  코드를 다음과 같이 변경하고 쿼리를 다시 실행합니다. 이번에는 행이 올바르게 업데이트됩니다.  
  
    ```  
    insert dbo.Products values  
    (3, 'Potato Chips', 2, 1, 1)  
    GO  
    ```  
  
## <a name="see-also"></a>참고 항목  
[테이블 및 관계 관리, 오류 해결](../ssdt/manage-tables-relationships-and-fix-errors.md)  
[Transact-SQL 편집기를 사용하여 스크립트 편집 및 실행](../ssdt/use-transact-sql-editor-to-edit-and-execute-scripts.md)  
  
