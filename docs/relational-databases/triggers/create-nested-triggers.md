---
title: "중첩 트리거 만들기 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-dml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- recursive DML triggers [SQL Server]
- DML triggers, nested
- triggers [SQL Server], nested
- direct recursion [SQL Server]
- triggers [SQL Server], recursive
- DML triggers, recursive
- RECURSIVE_TRIGGERS option
- indirect recursion [SQL Server]
- nested DML triggers
ms.assetid: cd522dda-b4ab-41b8-82b0-02445bdba7af
caps.latest.revision: "32"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 0e1320a9a1e3670c6d5cfc04d4b56f9d3ba51cc6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="create-nested-triggers"></a>중첩 트리거 만들기
  DML 및 DDL 트리거는 트리거가 다른 트리거를 시작하는 동작을 수행할 때 둘 다 중첩됩니다. 이러한 동작이 다른 트리거를 시작할 수도 있습니다. DML 및 DDL 트리거는 최대 32 수준까지 중첩될 수 있습니다. **nested triggers** 서버 구성 옵션을 통해 AFTER 트리거를 중첩할 수 있는지를 제어할 수 있습니다. INSTEAD OF 트리거(DML 트리거만 INSTEAD OF 트리거가 될 수 있음)는 이 설정에 관계없이 중첩될 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[tsql](../../includes/tsql-md.md)] 트리거에서 관리 코드로의 참조는 32 수준 중첩 제한에서 한 수준으로 계산됩니다. 관리 코드 내에서 호출된 메서드는 이 제한에 따라 계산되지 않습니다.  
  
 중첩 트리거가 허용되고 체인에 있는 한 트리거가 무한 루프를 시작하면 중첩 수준을 초과하기 때문에 트리거가 종료됩니다.  
  
 중첩 트리거를 사용하여 이전 트리거의 영향을 받는 행의 백업 복사본을 저장하는 등의 유용한 정리 작업 기능을 수행할 수 있습니다. 예를 들어 `PurchaseOrderDetail` 트리거가 삭제한 `PurchaseOrderDetail` 행의 백업 복사본을 저장하는 트리거를 `delcascadetrig` 에 만들 수 있습니다. `delcascadetrig` 트리거가 적용 중일 때 `PurchaseOrderID` 에서 `PurchaseOrderHeader` 1965를 삭제하면 `PurchaseOrderDetail`에서 해당 행이 삭제됩니다. 삭제된 데이터를 별도로 만든 다른 테이블 `PurchaseOrderDetail` 에 저장하는 DELETE 트리거를 `del_save`에 만들면 삭제된 데이터를 저장할 수 있습니다. 예를 들어  
  
```  
CREATE TRIGGER Purchasing.savedel  
   ON Purchasing.PurchaseOrderDetail  
FOR DELETE  
AS  
   INSERT del_save;  
   SELECT * FROM deleted;  
```  
  
 순서가 중요한 시퀀스에는 중첩 트리거를 사용하지 않는 것이 좋습니다. 관련 데이터를 모두 수정할 때는 별도의 트리거를 사용하십시오.  
  
> [!NOTE]  
>  트랜잭션 안에서 트리거가 실행되기 때문에 중첩 트리거의 특정 수준에서 작업이 실패하면 전체 트랜잭션이 취소되고 모든 데이터 수정 내용이 롤백됩니다. 트리거에 PRINT 문을 포함시키면 오류가 발생한 위치를 확인할 수 있습니다.  
  
## <a name="recursive-triggers"></a>재귀 트리거  
 RECURSIVE_TRIGGERS 데이터베이스 옵션을 설정하지 않으면 AFTER 트리거가 자신을 재귀적으로 호출하지 않습니다.  
  
 다음과 같은 두 가지 유형의 재귀가 있습니다.  
  
-   직접 재귀  
  
     이 재귀는 트리거가 같은 트리거를 다시 시작하는 동작을 시작 및 수행할 때 발생합니다. 예를 들어 응용 프로그램이 **T3**테이블을 업데이트하면 **Trig3** 트리거가 시작됩니다. **Trig3** 은 다시 **T3** 테이블을 업데이트하고 이로 인해 **Trig3** 트리거가 다시 시작됩니다.  
  
     다른 유형(AFTER 또는 INSTEAD OF)의 트리거를 호출한 후 동일한 트리거를 다시 호출할 때도 직접 재귀가 발생할 수 있습니다. 즉, 하나 이상의 AFTER 트리거를 중간에 호출해도 동일한 INSTEAD OF 트리거를 두 번째로 호출하면 INSTEAD OF 트리거의 직접 재귀가 발생할 수 있습니다. 마찬가지로 하나 이상의 INSTEAD OF 트리거를 중간에 호출해도 동일한 AFTER 트리거를 두 번째로 호출하면 AFTER 트리거의 직접 재귀가 발생할 수 있습니다. 예를 들어 응용 프로그램이 **T4**테이블을 업데이트합니다. 이 업데이트로 인해 INSTEAD OF 트리거 **Trig4** 가 발생합니다. **Trig4** 는 **T5**테이블을 업데이트합니다. 이 업데이트로 인해 AFTER 트리거 **Trig5** 가 발생합니다. **Trig5** 는 **T4**테이블을 업데이트하고 이 업데이트로 인해 INSTEAD OF 트리거 **Trig4** 가 다시 발생합니다. 이 이벤트 체인을 **Trig4**의 직접 재귀로 간주합니다.  
  
-   간접 재귀  
  
     트리거가 발생하고 같은 유형(AFTER 또는 INSTEAD OF)의 다른 트리거를 발생시키는 동작을 수행하면 이 재귀가 발생합니다. 이 두 번째 트리거는 원래 트리거를 다시 시작하는 동작을 수행합니다. 즉, 다른 INSTEAD OF 트리거를 중간에 호출한 후 INSTEAD OF 트리거를 두 번째로 호출하면 간접 재귀가 발생할 수 있습니다. 마찬가지로 다른 AFTER 트리거를 중간에 호출한 후 AFTER 트리거를 두 번째로 호출하면 간접 재귀가 발생할 수 있습니다. 예를 들어 응용 프로그램이 **T1**테이블을 업데이트합니다. 이 업데이트로 인해 AFTER 트리거 **Trig1** 이 발생합니다. **Trig1** 은 **T2**테이블을 업데이트하고 이 업데이트로 인해 AFTER 트리거 **Trig2** 가 발생합니다. **Trig2** 는 다시 **T1** 테이블을 업데이트하고 이로 인해 AFTER 트리거 **Trig1** 이 다시 발생합니다.  
  
 RECURSIVE_TRIGGERS 데이터베이스 옵션을 OFF로 설정하면 AFTER 트리거의 직접 재귀만 금지됩니다. AFTER 트리거의 간접 재귀를 해제하려면 **nested triggers** 서버 옵션도 **0**으로 설정합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 재귀 트리거를 사용하여 자체 참조 관계(전이 종료라고도 함)를 해결하는 방법을 보여 줍니다. 예를 들어 `emp_mgr` 테이블은 다음을 정의합니다.  
  
-   회사 직원(`emp`)  
  
-   각 직원의 관리자(`mgr`)  
  
-   조직 트리 내에서 각 직원에게 보고하는 총 직원 수(`NoOfReports`)  
  
 재귀 UPDATE 트리거를 사용하여 새 직원 레코드가 삽입될 때 `NoOfReports` 열을 최신 상태로 유지할 수 있습니다. INSERT 트리거가 관리자 레코드의 `NoOfReports` 열을 업데이트하면 관리 계층 위에 있는 다른 레코드의 `NoOfReports` 열이 재귀적으로 업데이트됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
-- Turn recursive triggers ON in the database.  
ALTER DATABASE AdventureWorks2012  
   SET RECURSIVE_TRIGGERS ON;  
GO  
CREATE TABLE dbo.emp_mgr (  
   emp char(30) PRIMARY KEY,  
    mgr char(30) NULL FOREIGN KEY REFERENCES emp_mgr(emp),  
    NoOfReports int DEFAULT 0  
);  
GO  
CREATE TRIGGER dbo.emp_mgrins ON dbo.emp_mgr  
FOR INSERT  
AS  
DECLARE @e char(30), @m char(30);  
DECLARE c1 CURSOR FOR  
   SELECT emp_mgr.emp  
   FROM   emp_mgr, inserted  
   WHERE emp_mgr.emp = inserted.mgr;  
  
OPEN c1;  
FETCH NEXT FROM c1 INTO @e;  
WHILE @@fetch_status = 0  
BEGIN  
   UPDATE dbo.emp_mgr  
   SET emp_mgr.NoOfReports = emp_mgr.NoOfReports + 1 -- Add 1 for newly  
   WHERE emp_mgr.emp = @e ;                           -- added employee.  
  
   FETCH NEXT FROM c1 INTO @e;  
END  
CLOSE c1;  
DEALLOCATE c1;  
GO  
-- This recursive UPDATE trigger works assuming:  
--   1. Only singleton updates on emp_mgr.  
--   2. No inserts in the middle of the org tree.  
CREATE TRIGGER dbo.emp_mgrupd ON dbo.emp_mgr FOR UPDATE  
AS  
IF UPDATE (mgr)  
BEGIN  
   UPDATE dbo.emp_mgr  
   SET emp_mgr.NoOfReports = emp_mgr.NoOfReports + 1 -- Increment mgr's  
   FROM inserted                            -- (no. of reports) by  
   WHERE emp_mgr.emp = inserted.mgr;         -- 1 for the new report.  
  
   UPDATE dbo.emp_mgr  
   SET emp_mgr.NoOfReports = emp_mgr.NoOfReports - 1 -- Decrement mgr's  
   FROM deleted                             -- (no. of reports) by 1  
   WHERE emp_mgr.emp = deleted.mgr;          -- for the new report.  
END  
GO  
-- Insert some test data rows.  
INSERT dbo.emp_mgr(emp, mgr) VALUES  
    ('Harry', NULL)  
    ,('Alice', 'Harry')  
    ,('Paul', 'Alice')  
    ,('Joe', 'Alice')  
    ,('Dave', 'Joe');  
GO  
SELECT emp,mgr,NoOfReports  
FROM dbo.emp_mgr;  
GO  
-- Change Dave's manager from Joe to Harry  
UPDATE dbo.emp_mgr SET mgr = 'Harry'  
WHERE emp = 'Dave';  
GO  
SELECT emp,mgr,NoOfReports FROM emp_mgr;  
  
GO  
```  
  
 다음은 업데이트되기 전의 결과입니다.  
  
```  
emp                            mgr                           NoOfReports  
------------------------------ ----------------------------- -----------  
Alice                          Harry                          2  
Dave                           Joe                            0  
Harry                          NULL                           1  
Joe                            Alice                          1  
Paul                           Alice                          0  
```  
  
 다음은 업데이트된 후의 결과입니다.  
  
```  
emp                            mgr                           NoOfReports  
------------------------------ ----------------------------- -----------  
Alice                          Harry                          2  
Dave                           Harry                          0  
Harry                          NULL                           2  
Joe                            Alice                          0  
Paul                           Alice                          0  
```  
  
 **중첩 트리거 옵션을 설정하려면**  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
 **RECURSIVE_TRIGGERS 데이터베이스 옵션을 설정하려면**  
  
-   [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
## <a name="see-also"></a>참고 항목  
 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [nested triggers 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md)  
  
  
