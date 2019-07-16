---
title: 뷰 및 저장 프로시저 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- creating views and stored procedures
ms.assetid: 53a0426d-07d8-4b7c-aa21-22632753bad8
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 20f16e9deeb9e07d2c63090c92100871331e0443
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211188"
---
# <a name="creating-views-and-stored-procedures"></a>뷰 및 저장 프로시저 만들기
  이제 Mary는 **TestData** 데이터베이스에 액세스할 수 있으므로 뷰 및 저장 프로시저와 같은 일부 데이터베이스 개체를 만든 다음 이러한 개체에 대한 액세스 권한을 Mary에게 부여할 수 있습니다. 뷰는 저장된 SELECT 문이며 저장 프로시저는 일괄 처리로 실행되는 하나 이상의 [!INCLUDE[tsql](../includes/tsql-md.md)] 문입니다.  
  
 뷰는 테이블처럼 쿼리되며 매개 변수를 허용하지 않습니다. 저장 프로시저는 뷰보다 복잡합니다. 저장 프로시저는 입력 및 출력 매개 변수를 가질 수 있으며 코드 흐름을 제어하기 위해 IF 및 WHILE 문과 같은 문을 포함할 수 있습니다. 데이터베이스의 모든 반복되는 동작에 저장 프로시저를 사용하는 것이 바람직한 프로그래밍 방식입니다.  
  
 예를 들어 CREATE VIEW를 사용하여 **Products** 테이블에 있는 두 개의 열만 선택하는 뷰를 만듭니다. 그런 다음 CREATE PROCEDURE를 사용하여 가격 매개 변수를 허용하고 지정된 매개 변수 값보다 가격이 낮은 제품만 반환하는 저장 프로시저를 만듭니다.  
  
### <a name="to-create-a-view"></a>뷰를 만들려면  
  
1.  다음 문을 실행하여 select 문을 실행하고 제품의 이름과 가격을 사용자에게 반환하는 매우 간단한 뷰를 만듭니다.  
  
    ```  
    CREATE VIEW vw_Names  
       AS  
       SELECT ProductName, Price FROM Products;  
    GO  
  
    ```  
  
### <a name="test-the-view"></a>뷰 테스트  
  
1.  뷰는 테이블처럼 처리됩니다. `SELECT` 문을 사용하여 뷰에 액세스할 수 있습니다.  
  
    ```  
    SELECT * FROM vw_Names;  
    GO  
  
    ```  
  
### <a name="to-create-a-stored-procedure"></a>저장 프로시저를 만들려면  
  
1.  다음 문은 저장 프로시저 이름인 `pr_Names`를 만들고 `@VarPrice` 데이터 형식의 `money`라는 입력 매개 변수를 허용합니다. 이 저장 프로시저는 `Products less than` 데이터 형식에서 `money` 문자 데이터 형식으로 변경되는 입력 매개 변수와 연결된 `varchar(10)` 문을 인쇄합니다. 그런 다음 이 저장 프로시저는 입력 매개 변수를 `SELECT` 절의 일부로 전달하며 뷰에서 `WHERE` 문을 실행합니다. 이렇게 하면 입력 매개 변수 값보다 가격이 낮은 모든 제품이 반환됩니다.  
  
    ```  
    CREATE PROCEDURE pr_Names @VarPrice money  
       AS  
       BEGIN  
          -- The print statement returns text to the user  
          PRINT 'Products less than ' + CAST(@VarPrice AS varchar(10));  
          -- A second statement starts here  
          SELECT ProductName, Price FROM vw_Names  
                WHERE Price < @varPrice;  
       END  
    GO  
  
    ```  
  
### <a name="test-the-stored-procedure"></a>저장 프로시저 테스트  
  
1.  저장 프로시저를 테스트하려면 다음 문을 입력하고 실행합니다. 이 프로시저는 1단원에서 가격이 `Products` 보다 낮은 `10.00`테이블에 입력한 제품 두 개의 이름을 반환해야 합니다.  
  
    ```  
    EXECUTE pr_Names 10.00;  
    GO  
  
    ```  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [데이터베이스 개체에 대한 액세스 권한 부여](lesson-2-4-granting-access-to-a-database-object.md)  
  
## <a name="see-also"></a>관련 항목  
 [CREATE VIEW&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql)   
 [CREATE PROCEDURE&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)  
  
  
