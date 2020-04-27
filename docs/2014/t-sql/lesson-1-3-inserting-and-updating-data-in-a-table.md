---
title: 테이블에서 데이터 삽입 및 업데이트(자습서) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- inserting and updating data
ms.assetid: 514dc87a-b829-43b5-8fc8-1a400a260284
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 19e6683baeb0a82c77a858b04f18695ba7120b15
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63250132"
---
# <a name="inserting-and-updating-data-in-a-table-tutorial"></a>테이블에서 데이터 삽입 및 업데이트(자습서)
  이제 **Products** 테이블을 만들었으므로 INSERT 문을 사용하여 테이블에 데이터를 삽입할 준비가 되었습니다. 데이터가 삽입된 후 UPDATE 문을 사용하여 행 내용을 변경합니다. UPDATE 문의 WHERE 절을 사용하여 업데이트를 단일 행으로 제한합니다. 4개의 문이 다음 데이터를 입력합니다.  
  
|ProductID|ProductName|Price|ProductDescription|  
|---------------|-----------------|-----------|------------------------|  
|1|Clamp|12.48|Workbench clamp|  
|50|Screwdriver|3.17|Flat head|  
|75|Tire Bar||Tool for changing tires.|  
|3000|3mm Bracket|.52||  
  
 기본 구문은 INSERT, 테이블 이름, 열 목록, VALUES, 삽입할 값 목록을 차례로 포함합니다. 줄의 맨 앞에 있는 두 개의 하이픈은 해당 줄이 주석이며 컴파일러에서 텍스트를 무시한다는 것을 나타냅니다. 이 경우에는 허용되는 구문 변형을 주석에서 설명합니다.  
  
### <a name="to-insert-data-into-a-table"></a>데이터를 테이블에 삽입하려면  
  
1.  다음 문을 실행하여 이전 태스크에서 만든 `Products` 테이블에 행을 삽입합니다. 기본 구문은 다음과 같습니다.  
  
    ```  
    -- Standard syntax  
    INSERT dbo.Products (ProductID, ProductName, Price, ProductDescription)  
        VALUES (1, 'Clamp', 12.48, 'Workbench clamp')  
    GO  
  
    ```  
  
2.  다음 문은 필드 목록(괄호로 묶인 부분) 및 값 목록에서 `ProductID` 및 `ProductName` 의 위치를 전환하여 매개 변수가 제공되는 순서를 변경하는 방법을 보여 줍니다.  
  
    ```  
    -- Changing the order of the columns  
    INSERT dbo.Products (ProductName, ProductID, Price, ProductDescription)  
        VALUES ('Screwdriver', 50, 3.17, 'Flat head')  
    GO  
  
    ```  
  
3.  다음 문은 값이 올바른 순서로 나열되는 경우 열 이름이 선택 사항임을 보여 줍니다. 이 구문이 일반적이기는 하지만 다른 사람이 코드를 이해하기 어려울 수 있으므로 이 구문을 사용하지 않는 것이 좋습니다. `NULL` 이 `Price` 열에 대해 지정되는데, 이 제품의 가격을 아직 알 수 없기 때문입니다.  
  
    ```  
    -- Skipping the column list, but keeping the values in order  
    INSERT dbo.Products  
        VALUES (75, 'Tire Bar', NULL, 'Tool for changing tires.')  
    GO  
  
    ```  
  
4.  기본 스키마에서 테이블을 액세스 및 변경하는 경우 스키마 이름은 선택 사항입니다. `ProductDescription` 열에서 Null 값을 허용하고 제공되는 값이 없으므로 `ProductDescription` 열 이름과 값을 문에서 완전히 삭제할 수 있습니다.  
  
    ```  
    -- Dropping the optional dbo and dropping the ProductDescription column  
    INSERT Products (ProductID, ProductName, Price)  
        VALUES (3000, '3mm Bracket', .52)  
    GO  
    ```  
  
### <a name="to-update-the-products-table"></a>Products 테이블을 업데이트하려면  
  
1.  다음 `UPDATE` 문을 입력하고 실행하여 두 번째 제품의 `ProductName` 을 `Screwdriver`에서 `Flat Head Screwdriver`로 변경합니다.  
  
    ```  
    UPDATE dbo.Products  
        SET ProductName = 'Flat Head Screwdriver'  
        WHERE ProductID = 50  
    GO  
    ```  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [테이블의 데이터 읽기&#40;자습서&#41;](lesson-1-4-reading-the-data-in-a-table.md)  
  
## <a name="see-also"></a>참고 항목  
 [INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)   
 [UPDATE&#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql)  
  
  
