---
title: "여러 행의 데이터를 처리하기 위한 DML 트리거 만들기 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-dml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- multiple row DML triggers
- UPDATE statement [SQL Server], DML triggers
- DELETE statement [SQL Server], DML triggers
- multirow DML triggers [SQL Server]
- INSERT statement [SQL Server], DML triggers
- DML triggers, multirow
ms.assetid: d476c124-596b-4b27-a883-812b6b50a735
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 55a772a063a33749af39f43d6a070bfdf8216796
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="create-dml-triggers-to-handle-multiple-rows-of-data"></a>여러 행의 데이터를 처리하기 위한 DML 트리거 만들기
  DML 트리거 코드를 작성할 때는 트리거를 실행시키는 단일 문이 여러 행의 데이터에 영향을 줄 수 있다는 점을 고려해야 합니다. 이 동작은 여러 행에 영향을 줄 수 있는 UPDATE 및 DELETE 트리거의 경우에 일반적입니다. 기본 INSERT 문은 한 행만 추가하기 때문에 INSERT 트리거의 경우에는 일반적이지 않습니다. 그러나 INSERT INTO (*table_name*) SELECT 문으로 INSERT 트리거를 실행할 수 있기 때문에 여러 행을 삽입하는 경우 단일 트리거를 호출할 수도 있습니다.  
  
 DML 트리거 함수가 한 테이블의 요약 값을 자동으로 다시 계산하여 계속 계산하기 위해 그 결과를 다른 테이블에 저장하는 경우 특히 다중 행을 고려해야 합니다.  
  
> [!NOTE]  
>  커서는 잠재적으로 성능을 저하시킬 수 있으므로 트리거에 사용하지 않는 것이 좋습니다. 다중 행에 영향을 주는 트리거를 디자인하려면 커서 대신 행 집합 기반 논리를 사용합니다.  
  
## <a name="examples"></a>예  
 다음 예에서 DML 트리거는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스의 다른 테이블에 열의 누계를 저장하도록 디자인되어 있습니다.  
  
### <a name="a-storing-a-running-total-for-a-single-row-insert"></a>1. 단일 행 삽입의 누계 저장  
 `PurchaseOrderDetail` 테이블에 데이터 행 하나를 로드하는 경우 첫 번째 버전의 DML 트리거는 단일 행 삽입에 대해 제대로 작동합니다. INSERT 문이 DML 트리거를 시작하면 트리거가 실행되는 동안 새 행이 **inserted** 테이블에 로드됩니다. `UPDATE` 문에서는 추가된 행의 `LineTotal` 열 값을 읽어 `SubTotal` 테이블에 있는 `PurchaseOrderHeader` 열의 기존 값에 더합니다. `WHERE` 절은 `PurchaseOrderDetail` 테이블에 있는 업데이트된 행이 `PurchaseOrderID` inserted **테이블에 있는** 행과 일치하는지 확인합니다.  
  
```  
-- Trigger is valid for single-row inserts.  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER NewPODetail  
ON Purchasing.PurchaseOrderDetail  
AFTER INSERT AS  
   UPDATE PurchaseOrderHeader  
   SET SubTotal = SubTotal + LineTotal  
   FROM inserted  
   WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID ;  
```  
  
### <a name="b-storing-a-running-total-for-a-multirow-or-single-row-insert"></a>2. 다중 행 또는 단일 행 삽입에 대한 누계 저장  
 다중 행을 삽입하는 경우에는 예 1의 DML 트리거가 제대로 실행되지 않을 수 있습니다. UPDATE 문에 있는 대입 식의 오른쪽 식(`SubTotal` + `LineTotal`)은 여러 값이 아니라 한 값만 될 수 있습니다. 따라서 트리거의 결과로 **inserted** 테이블의 단일 행에서 값을 검색하여 이 값을 특정 `SubTotal` 값에 대한 `PurchaseOrderHeader` 테이블의 기존 `PurchaseOrderID` 값에 추가합니다. 이 작업에서 `PurchaseOrderID` inserted **테이블에 단일** 값이 두 번 이상 나타난 경우 예상한 결과가 나오지 않을 수도 있습니다.  
  
 `PurchaseOrderHeader` 테이블을 올바르게 업데이트하려면 트리거가 **inserted** 테이블에 있는 다중 행을 변경할 수 있도록 허용해야 합니다. 이 작업은 각 `SUM` 에 대해 `LineTotal` inserted **테이블에 있는 행 그룹의 전체** 을 계산하는 `PurchaseOrderID`함수를 사용하여 수행할 수 있습니다. `SUM` 함수는 상호 관련된 하위 쿼리(괄호 안에 있는 `SELECT` 문)에 포함되어 있습니다. 이 하위 쿼리는 `PurchaseOrderID` 테이블의 **와 일치하거나 상호 관련된** inserted `PurchaseOrderID` 테이블의 각 `PurchaseOrderHeader` 에 대해 단일 값을 반환합니다.  
  
```  
-- Trigger is valid for multirow and single-row inserts.  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER NewPODetail2  
ON Purchasing.PurchaseOrderDetail  
AFTER INSERT AS  
   UPDATE Purchasing.PurchaseOrderHeader  
   SET SubTotal = SubTotal +   
      (SELECT SUM(LineTotal)  
      FROM inserted  
      WHERE PurchaseOrderHeader.PurchaseOrderID  
       = inserted.PurchaseOrderID)  
   WHERE PurchaseOrderHeader.PurchaseOrderID IN  
      (SELECT PurchaseOrderID FROM inserted);  
```  
  
 `LineTotal` 값 열의 합계가 단일 행의 합계와 같기 때문에 이 트리거는 단일 행만 삽입할 때도 제대로 실행됩니다. 그러나 이 트리거를 사용하면 상호 관련된 하위 쿼리 및 `IN` 절에서 사용되는 `WHERE` 연산자에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 추가 처리 작업이 필요합니다. 단일 행 삽입에는 이 작업이 필요하지 않습니다.  
  
### <a name="c-storing-a-running-total-based-on-the-type-of-insert"></a>3. 삽입 유형에 따른 누계 저장  
 트리거를 변경하여 행 수에 맞는 최적의 방법을 사용할 수 있습니다. 예를 들어 트리거 논리에서 `@@ROWCOUNT` 함수를 사용하여 단일 행 삽입과 다중 행 삽입을 구별할 수 있습니다.  
  
```  
-- Trigger valid for multirow and single row inserts  
-- and optimal for single row inserts.  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER NewPODetail3  
ON Purchasing.PurchaseOrderDetail  
FOR INSERT AS  
IF @@ROWCOUNT = 1  
BEGIN  
   UPDATE Purchasing.PurchaseOrderHeader  
   SET SubTotal = SubTotal + LineTotal  
   FROM inserted  
   WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID  
END  
ELSE  
BEGIN  
      UPDATE Purchasing.PurchaseOrderHeader  
   SET SubTotal = SubTotal +   
      (SELECT SUM(LineTotal)  
      FROM inserted  
      WHERE PurchaseOrderHeader.PurchaseOrderID  
       = inserted.PurchaseOrderID)  
   WHERE PurchaseOrderHeader.PurchaseOrderID IN  
      (SELECT PurchaseOrderID FROM inserted)  
END;  
```  
  
## <a name="see-also"></a>참고 항목  
 [DML 트리거](../../relational-databases/triggers/dml-triggers.md)  
  
  
