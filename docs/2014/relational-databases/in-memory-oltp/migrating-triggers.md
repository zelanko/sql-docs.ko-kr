---
title: 트리거 마이그레이션 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: ad5385c5-5a50-40ca-a319-97d5606b8511
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b7df393f26523991abafded74ded242390cb0e3b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63071471"
---
# <a name="migrating-triggers"></a>트리거 마이그레이션
  이 항목에서는 DDL 및 DML 트리거와 메모리 최적화 테이블에 대해 설명합니다.  
  
 LOGON 트리거는 LOGON 이벤트에 대해 발생하도록 정의된 트리거입니다. LOGON 트리거는 메모리 최적화 테이블에 영향을 주지 않습니다.  
  
## <a name="ddl-triggers"></a>DDL 트리거  
 DDL 트리거는 이 트리거가 정의된 데이터베이스 또는 서버에서 CREATE, ALTER, DROP, GRANT, DENY, REVOKE, or UPDATE STATISTICS 문을 실행할 때 발생하도록 정의된 트리거입니다.  
  
 데이터베이스 또는 서버에 CREATE_TABLE 또는 이를 포함하는 이벤트 그룹에 정의된 DDL 트리거가 하나 이상 있으면 메모리 최적화 테이블을 만들 수 없습니다. 데이터베이스 또는 서버에 DROP_TABLE 또는 이를 포함하는 이벤트 그룹에 정의된 DDL 트리거가 하나 이상 있으면 메모리 최적화 테이블을 삭제할 수 없습니다.  
  
 CREATE_PROCEDURE, DROP_PROCEDURE 또는 이러한 이벤트를 포함하는 이벤트 그룹에 DDL 트리거나 하나 이상 있는 경우에는 고유하게 컴파일된 저장 프로시저를 만들 수 없습니다.  
  
## <a name="dml-triggers"></a>DML 트리거  
 DML 트리거는 메모리 최적화 테이블에 정의할 수 없습니다. 그러나 메모리 내 OLTP를 사용하면 저장 프로시저를 명시적으로 사용하여 데이터를 삽입, 업데이트 또는 삭제하는 경우 DML 트리거를 사용할 때와 비슷한 효과를 얻을 수 있습니다. 시스템에 임시 쿼리가 있는 경우 DML 트리거의 효과를 시뮬레이션하는 대신 이러한 저장 프로시저를 사용하도록 이 임시 쿼리를 변환하십시오.  
  
 트리거 이벤트(FOR/AFTER 또는 INSTEAD OF)에 따라 해당 테이블에 대해 INSERT, UPDATE 또는 DELETE를 수행하는 트리거 내용을 적합한 저장 프로시저에 포함할 수 있습니다. 예를 들어 AFTER INSERT 트리거를 마이그레이션하는 경우 적합한 INSERT 문 다음에 트리거 내용을 포함하여 삽입 작업을 수행하는 저장 프로시저를 변경할 수 있습니다.  
  
 해석된 저장 프로시저 또는 고유하게 컴파일된 저장 프로시저를 사용할 수 있습니다. 해석된 저장 프로시저에 있는 대부분의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문을 메모리 최적화 테이블에서 실행할 수 있습니다. 그러나 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문의 하위 집합만 고유하게 컴파일된 저장 프로시저에서 지원됩니다. 메모리 최적화 테이블 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에 대 한 지원에 대 한 자세한 내용은 [해석 된 Transact-sql을 사용 하 여 메모리 액세스에 최적화 된 테이블에 액세스](accessing-memory-optimized-tables-using-interpreted-transact-sql.md)를 참조 하세요. 고유 하 게 [!INCLUDE[tsql](../../includes/tsql-md.md)] 컴파일된 저장 프로시저의 지원에 대 한 자세한 내용은 [메모리 내 OLTP에서 지원 되지 않는 transact-sql 구문](transact-sql-constructs-not-supported-by-in-memory-oltp.md)을 참조 하세요.  
  
 다음은 메모리 최적화 테이블에 대한 DML 트리거 동작을 시뮬레이션하는 간단한 예입니다.  
  
 데이터베이스에는 CREATE TABLE, CREATE TRIGGER 및 CREATE PROCEDURE 문으로 스크립팅된 다음 개체가 포함되어 있습니다.  
  
```sql  
CREATE TABLE OrderDetails  
(  
   OrderId int not null primary key,  
   ProductId int not null,  
   SalePrice money not null,  
   Quantity int not null,  
   Total money not null,  
   IsDeleted bit not null DEFAULT (0)  
)  
GO  
  
CREATE TRIGGER tr_order_details_insteadof_insert  
ON OrderDetails  
INSTEAD OF INSERT AS  
BEGIN  
   DECLARE @pid int, @qty_buy int, @qty_remain int  
   SELECT @pid = ProductId, @qty_buy = Quantity FROM inserted  
   SELECT @qty_remain = Quantity FROM Inventory WHERE ProductId = @pid  
   IF (@qty_remain <= @qty_buy)  
      THROW 51000, N'Insufficient inventory!', 1  
   ELSE  
   BEGIN  
      INSERT INTO dbo.OrderDetails (OrderId, ProductId, SalePrice, Quantity, Total)   
      SELECT OrderId, ProductId, SalePrice, Quantity, Total FROM inserted  
      UPDATE Inventory SET Quantity = Quantity - @qty_buy WHERE ProductId = @pid  
   END  
END  
GO  
  
CREATE TRIGGER tr_order_details_after_update  
ON OrderDetails  
AFTER UPDATE AS  
BEGIN  
   INSERT INTO UpdateNotifications (OrderId, UpdateTime) SELECT OrderId, GETDATE() FROM inserted     
END  
GO  
  
CREATE PROCEDURE sp_insert_order_details   
   @OrderId int, @ProductId int, @SalePrice money, @Quantity int, @total money  
AS BEGIN  
   INSERT INTO dbo.OrderDetails (OrderId, ProductId, SalePrice, Quantity, Total)  
   VALUES (@OrderId, @ProductId, @SalePrice, @Quantity, @total)  
END  
GO  
  
CREATE PROCEDURE sp_update_order_details_by_id  
   @OrderId int, @ProductId int, @SalePrice money, @Quantity int, @Total money  
AS BEGIN  
   UPDATE dbo.OrderDetails   
   SET ProductId = @ProductId, SalePrice = @SalePrice, Quantity = @Quantity, Total = @total  
   WHERE OrderId = @OrderId  
END  
GO  
```  
  
 다음 개체는 마이그레이션 전 상태와 같은 기능을 합니다.  
  
```sql  
CREATE TABLE OrderDetails  
(  
   OrderId int not null PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT = 1048576),  
   ProductId int not null,  
   SalePrice money not null,  
   Quantity int not null,  
   Total money not null,  
   IsDeleted bit not null DEFAULT (0)  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
GO  
  
CREATE TABLE Inventory  
(  
   ProductId int not null PRIMARY KEY NONCLUSTERED,  
   Quantity int not null  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
GO  
  
CREATE TABLE UpdateNotifications  
(  
   OrderId int not null,  
   UpdateTime datetime2 not null  
   CONSTRAINT pk_updateNotifications PRIMARY KEY NONCLUSTERED (OrderId, UpdateTime)  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
GO  
  
CREATE PROCEDURE sp_insert_order_details   
   @OrderId int, @ProductId int, @SalePrice money, @Quantity int, @total money  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'English')  
   DECLARE @qty_remain int  
   SELECT @qty_remain = Quantity FROM dbo.Inventory WHERE ProductId = @ProductId  
   IF (@qty_remain <= @Quantity)  
      THROW 51000, N'Insufficient inventory!', 1  
   ELSE  
   BEGIN  
      INSERT INTO dbo.OrderDetails (OrderId, ProductId, SalePrice, Quantity, Total)   
      VALUES (@OrderId, @ProductId, @SalePrice, @Quantity, @total)  
      UPDATE dbo.Inventory SET Quantity = Quantity - @Quantity WHERE ProductId = @ProductId  
   END  
END  
GO  
  
CREATE PROCEDURE sp_update_order_details_by_id  
   @OrderId int, @ProductId int, @SalePrice money, @Quantity int, @Total money  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'English')  
   UPDATE dbo.OrderDetails   
   SET ProductId = @ProductId, SalePrice = @SalePrice, Quantity = @Quantity, Total = @total  
   WHERE OrderId = @OrderId  
   INSERT INTO dbo.UpdateNotifications (OrderId, UpdateTime) VALUES (@OrderId, GETDATE())  
END  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP로 마이그레이션](migrating-to-in-memory-oltp.md)  
  
  
