---
title: "inserted 및 deleted 테이블 사용 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: triggers
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-dml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- inserted tables
- UPDATE statement [SQL Server], DML triggers
- DELETE statement [SQL Server], DML triggers
- INSTEAD OF triggers
- deleted tables
- INSERT statement [SQL Server], DML triggers
- DML triggers, deleted or inserted tables
ms.assetid: ed84567f-7b91-4b44-b5b2-c400bda4590d
caps.latest.revision: "35"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: a285b7ece1c5f8c84c7cfc1292f4e5a4dffdc6f1
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="use-the-inserted-and-deleted-tables"></a>inserted 및 deleted 테이블 사용
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)] DML 트리거 문은 두 개의 특수 테이블(inserted 및 deleted 테이블)을 사용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 이러한 테이블을 자동으로 만들고 관리합니다. 메모리에 상주하는 이러한 임시 테이블을 사용하여 특정 데이터의 수정 결과를 테스트하고 DML 트리거 동작에 대한 조건을 설정할 수 있습니다. 이 테이블에서 데이터를 직접 수정하거나 CREATE INDEX와 같은 DDL(데이터 정의 언어) 작업을 수행할 수 없습니다.  
  
 DML 트리거에서 inserted 및 deleted 테이블은 주로 다음 작업을 수행하는 데 사용됩니다.  
  
-   테이블 간 참조 무결성을 확장합니다.  
  
-   뷰를 원본으로 사용하는 기본 테이블에 데이터를 삽입하거나 업데이트합니다.  
  
-   오류가 있는지 테스트하고 오류에 따른 적절한 동작을 수행합니다.  
  
-   데이터를 수정하기 전과 후의 테이블 상태 차이를 찾고 이 차이에 따라 동작을 수행합니다.  
  
 deleted 테이블에는 DELETE 및 UPDATE 문을 실행할 때 영향을 받는 행의 복사본이 저장됩니다. DELETE 또는 UPDATE 문을 실행하는 동안 트리거 테이블에서 행이 삭제되어 deleted 테이블로 이동됩니다. deleted 테이블과 트리거 테이블은 보통 서로 공통되는 행이 없습니다.  
  
 inserted 테이블에는 INSERT 및 UPDATE 문을 실행할 때 영향을 받는 행의 복사본이 저장됩니다. 삽입 또는 업데이트 트랜잭션 동안 새 행은 inserted 테이블과 트리거 테이블에 추가됩니다. inserted 테이블의 행은 트리거 테이블에 있는 새 행의 복사본입니다.  
  
 업데이트 트랜잭션은 삭제 작업과 삽입 작업을 차례로 수행하는 것과 비슷합니다. 즉 이전 행이 먼저 deleted 테이블로 복사된 다음 새 행이 트리거 테이블과 inserted 테이블로 복사됩니다.  
  
 트리거 조건을 설정할 때는 트리거를 실행한 동작에 적합한 inserted 및 deleted 테이블을 사용합니다. INSERT를 테스트할 때 deleted 테이블을 참조하거나 DELETE를 테스트할 때 inserted 테이블을 참조해도 오류가 발생하지는 않지만 이러한 경우 트리거 테스트 테이블에는 아무 행도 들어 있지 않습니다.  
  
> [!NOTE]  
>  트리거 동작이 데이터 수정의 영향을 받는 행의 수에 따라 달라지는 경우 여러 행 데이터 수정(SELECT 문을 기반으로 하는 INSERT, DELETE 또는 UPDATE)에 @@ROWCOUNT 검사 같은 테스트를 사용하고 적합한 작업을 수행합니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서는 inserted 및 deleted 테이블에서 AFTER 트리거에 대한 **text**, **ntext**또는 **image** 열 참조를 허용하지 않습니다. 하지만 이러한 데이터 형식은 단지 이전 버전과의 호환성을 위해 포함된 것입니다. 큰 데이터를 저장하는 경우 **varchar(max)**, **nvarchar(max)**및 **varbinary(max)** 데이터 형식을 사용하는 것이 좋습니다. AFTER 및 INSTEAD OF 트리거는 모두 inserted 및 deleted 테이블에서 **varchar(max)**, **nvarchar(max)** 및 **varbinary(max)** 데이터를 지원합니다. 자세한 내용은 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)를 참조하세요.  
  
 **비즈니스 규칙을 적용하기 위해 트리거의 inserted 테이블을 사용하는 예**  
  
 CHECK 제약 조건은 열 수준 또는 테이블 수준 제약 조건이 정의된 열만 참조할 수 있으므로 모든 상호 테이블 제약 조건(이 경우 업무 규칙)을 트리거로 정의해야 합니다.  
  
 다음 예에서는 DML 트리거를 만듭니다. 이 트리거는 `PurchaseOrderHeader` 테이블에 새 구매 주문을 삽입하려고 할 때 공급업체의 신용 등급이 양호한지 확인합니다. 방금 삽입된 구매 주문에 해당하는 공급업체의 신용 등급을 가져오려면 `Vendor` 테이블이 참조되어 inserted 테이블과 조인되어야 합니다. 신용 등급이 너무 낮으면 메시지가 표시되고 삽입이 실행되지 않습니다. 이 예에서는 다중 행 데이터 수정을 허용하지 않습니다. 자세한 내용은 [Create DML Triggers to Handle Multiple Rows of Data](../../relational-databases/triggers/create-dml-triggers-to-handle-multiple-rows-of-data.md)를 참조하세요.  
  
 [!code-sql[TriggerDDL#CreateTrigger3](../../relational-databases/triggers/codesnippet/tsql/use-the-inserted-and-del_1.sql)]  
  
## <a name="using-the-inserted-and-deleted-tables-in-instead-of-triggers"></a>INSTEAD OF 트리거에서 inserted 및 deleted 테이블 사용  
 테이블에 정의된 INSTEAD OF 트리거로 전달되는 inserted 및 deleted 테이블은 AFTER 트리거로 전달되는inserted 및 deleted 테이블과 같은 규칙을 따릅니다. inserted 및 deleted 테이블의 형식은 INSTEAD OF 트리거가 정의된 테이블의 형식과 같습니다. inserted 및 deleted 테이블의 각 열은 기본 테이블의 열로 직접 매핑됩니다.  
  
 INSTEAD OF 트리거가 있는 테이블을 참조하는 INSERT 또는 UPDATE 문이 열 값을 제공해야 하는 경우와 관련된 다음 규칙은 테이블에 INSTEAD OF 트리거가 없는 경우와 동일합니다.  
  
-   계산 열이나 **timestamp** 데이터 형식의 열에는 값을 지정할 수 없습니다.  
  
-   해당 테이블에 대해 IDENTITY_INSERT가 ON으로 설정되어 있지 않으면 IDENTITY 속성이 있는 열에 값을 지정할 수 없습니다. IDENTITY_INSERT가 ON이면 INSERT 문이 값을 제공해야 합니다.  
  
-   INSERT 문은 DEFAULT 제약 조건이 없는 모든 NOT NULL 열에 값을 제공해야 합니다.  
  
-   계산 열, ID 열 또는 **timestamp** 열을 제외한 모든 열에서 Null을 허용하는 열 또는 DEFAULT 정의가 있는 NOT NULL 열의 경우 값이 선택적입니다.  
  
 INSERT, UPDATE 또는 DELETE 문에서 INSTEAD OF 트리거가 있는 뷰를 참조할 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 테이블에 대해 직접 동작을 수행하는 대신 트리거를 호출합니다. 뷰에 대해 작성된 inserted 및 deleted 테이블의 정보 형식이 기본 테이블에 있는 데이터 형식과 다른 경우에도 트리거는 inserted 및 deleted 테이블에 있는 정보를 사용하여 기본 테이블에서 요청된 동작을 구현하는 데 필요한 문을 작성해야 합니다.  
  
 뷰에 정의된 INSTEAD OF 트리거로 전달되는 inserted 및 deleted 테이블의 형식은 뷰에 대해 정의된 SELECT 문의 선택 목록과 일치합니다. 예를 들어  
  
```  
USE AdventureWorks2012;  
GO  
CREATE VIEW dbo.EmployeeNames (BusinessEntityID, LName, FName)  
AS  
SELECT e.BusinessEntityID, p.LastName, p.FirstName  
FROM HumanResources.Employee AS e   
JOIN Person.Person AS p  
ON e.BusinessEntityID = p.BusinessEntityID;  
```  
  
 이 뷰의 결과 집합에는 **int** 열 하나와 **nvarchar** 열 두 개가 있습니다. 뷰에 정의된 INSTEAD OF 트리거로 전달되는 inserted 및 deleted 테이블에는 또한 **라는** int `BusinessEntityID`열, **이라는** nvarchar `LName`열 및 **이라는** nvarchar `FName`열이 있습니다.  
  
 뷰의 선택 목록에는 단일 기본 테이블 열에 직접 매핑되지 않는 식이 포함될 수도 있습니다. 상수 또는 함수 호출과 같은 일부 뷰 식은 열을 참조하지 않으므로 무시될 수 있습니다. 복합 식은 여러 개의 열을 참조할 수 있지만 inserted 및 deleted 테이블에는 삽입된 각 행에 대해 하나의 값만 있습니다. 뷰의 단순 식에서 복합 식이 있는 계산 열을 참조하는 경우에도 마찬가지입니다. 뷰의 INSTEAD OF 트리거는 이러한 유형의 식을 처리해야 합니다.  
  
  
