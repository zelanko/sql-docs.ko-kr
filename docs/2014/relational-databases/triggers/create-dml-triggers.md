---
title: DML 트리거 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- encryption [SQL Server], DML triggers
- deferred name resolution, DML triggers
- WITH ENCRYPTION clause
- IF UPDATE
- SET statement, DML triggers
- DML triggers, programming
- testing column changes
- results [SQL Server], DML triggers
ms.assetid: b2b52258-642b-462e-8e0f-18c09d2eccf4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 10399a26335912a9370aa21a386f58d04d04321e
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72796392"
---
# <a name="create-dml-triggers"></a>DML 트리거 만들기
  이 항목에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 및 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] CREATE TRIGGER 문을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] DML 트리거를 만드는 방법에 대해 설명합니다.  
  
##  <a name="Top"></a> 시작하기 전에  
  
### <a name="limitations-and-restrictions"></a>제한 사항  
 DML 트리거 생성과 관련한 제한 사항 목록은 [CREATE TRIGGER&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)를 참조하세요.  
  
###  <a name="Permissions"></a> Permissions  
 트리거를 생성할 테이블 또는 뷰에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="Procedures"></a> DML 트리거를 만드는 방법  
 다음 중 하나를 사용할 수 있습니다.  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**, [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스, **테이블** 및 **Purchasing.PurchaseOrderHeader**테이블을 차례로 확장합니다.  
  
3.  **트리거**를 마우스 오른쪽 단추로 클릭한 다음 **새 트리거**를 선택합니다.  
  
4.  **쿼리** 메뉴에서 **템플릿 매개 변수 값 지정**을 클릭합니다. 또는 (Ctrl-Shift-M)을 눌러 **템플릿 매개 변수 값 지정** 대화 상자를 열 수 있습니다.  
  
5.  **템플릿 매개 변수 값 지정** 대화 상자에 표시된 매개 변수에 대해 다음 값을 입력합니다.  
  
    |Execute|ReplTest1|  
    |---------------|-----------|  
    |작성자|*Your name*|  
    |만든 날짜|*Today's date*|  
    |Description|공급업체의 새 PO를 삽입하기 전에 공급업체의 신용 등급을 확인합니다.|  
    |Schema_Name|Purchasing|  
    |Trigger_Name|NewPODetail2|  
    |Table_Name|PurchaseOrderDetail|  
    |Data_Modification_Statement|목록에서 UPDATE 및 DELETE를 제거합니다.|  
  
6.  **확인**을 클릭합니다.  
  
7.  **쿼리 편집기**에서 `-- Insert statements for trigger here` 주석을 다음 문으로 바꿉니다.  
  
    ```sql  
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
  
8.  구문이 올바른지 확인하려면 **쿼리** 메뉴에서 **구문 분석**을 클릭합니다. 오류 메시지가 반환되면 필요에 따라 위의 정보와 문을 비교하여 수정하고 이 단계를 반복합니다.  
  
9. DML 트리거를 만들려면 **쿼리** 메뉴에서 **실행**을 클릭합니다. DML 트리거가 데이터베이스 개체로 만들어집니다.  
  
10. 개체 탐색기에 나열된 DML 트리거를 보려면 **트리거** 를 마우스 오른쪽 단추로 클릭하고 **새로 고침**을 선택합니다.  
  
 [시작하기 전에](#Top)  
  
###  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  메뉴에서 **파일** 메뉴에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 위와 동일한 저장된 DML 트리거를 만듭니다.  
  
    ```sql
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
