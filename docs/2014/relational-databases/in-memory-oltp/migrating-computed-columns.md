---
title: 계산 열 마이그레이션 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 64a9eade-22c3-4a9d-ab50-956219e08df1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 65d6680d7e03960c0c59e83413be58cb74e5f028
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48158113"
---
# <a name="migrating-computed-columns"></a>계산 열 마이그레이션
  계산 열은 메모리 최적화 테이블에서 지원되지 않습니다. 그러나 계산 열을 시뮬레이션할 수 있습니다.  
  
 디스크 기반 테이블을 메모리 최적화 테이블로 마이그레이션하는 경우 계산 열을 유지할 필요성을 고려해야 합니다. 메모리 최적화 테이블과 고유하게 컴파일된 저장 프로시저의 다양한 성능 특성 때문에 계산 열을 유지할 필요성이 무시될 수 있습니다.  
  
## <a name="non-persisted-computed-columns"></a>비지속형 계산 열  
 비지속형 계산 열의 효과를 시뮬레이션하려면 메모리 최적화 테이블에 대한 뷰를 만듭니다. 뷰를 정의하는 SELECT 문에서 계산 열 정의를 뷰에 추가합니다. 고유하게 컴파일된 저장 프로시저의 경우를 제외하고 계산 열에서 값을 사용하는 쿼리는 뷰에서 읽어야 합니다. 고유하게 컴파일된 저장 프로시저 내에서는 계산 열 정의에 따라 모든 SELECT, UPDATE 또는 DELETE 문을 업데이트해야 합니다.  
  
```tsql  
-- Schema for the table dbo.OrderDetails:  
-- OrderId int not null primary key,  
-- ProductId int not null,  
-- SalePrice money not null,  
-- Quantity int not null,  
-- Total money not null  
--  
-- Total is computed as SalePrice * Quantity and is not persisted.  
CREATE VIEW dbo.v_order_details AS  
   SELECT  
      OrderId,  
      ProductId,  
      SalePrice,  
      Quantity,  
      Quantity * SalePrice AS Total  
   FROM dbo.order_details  
```  
  
## <a name="persisted-computed-columns"></a>지속형 계산 열  
 지속형 계산 열의 효과를 시뮬레이션하려면 테이블에 삽입하기 위한 저장 프로시저와 테이블을 업데이트하기 위한 또 다른 저장 프로시저를 만듭니다. 테이블을 삽입하거나 업데이트하는 경우 이러한 저장 프로시저를 호출하여 해당 작업을 수행합니다. 저장 프로시저 내에서는 계산 열이 원래 디스크 기반 테이블에 정의되는 방식과 매우 유사하게 입력에 따라 계산 필드의 값을 계산합니다. 그런 다음 저장 프로시저 내에서 필요에 따라 테이블을 삽입하거나 업데이트합니다.  
  
```tsql  
-- Schema for the table dbo.OrderDetails:  
-- OrderId int not null primary key,  
-- ProductId int not null,  
-- SalePrice money not null,  
-- Quantity int not null,  
-- Total money not null  
--  
-- Total is computed as SalePrice * Quantity and is persisted.  
-- we need to create insert and update procedures to calculate Total.  
CREATE PROCEDURE sp_insert_order_details   
@OrderId int, @ProductId int, @SalePrice money, @Quantity int  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (LANGUAGE = N'english', TRANSACTION ISOLATION LEVEL = SNAPSHOT)  
-- compute the value here.   
-- this stored procedure works with single rows only.  
-- for bulk inserts, accept a table-valued parameter into the stored procedure  
-- and use an INSERT INTO SELECT statement.  
DECLARE @total money = @SalePrice * @Quantity  
INSERT INTO dbo.OrderDetails (OrderId, ProductId, SalePrice, Quantity, Total)  
VALUES (@OrderId, @ProductId, @SalePrice, @Quantity, @total)  
END  
GO  
  
CREATE PROCEDURE sp_update_order_details_by_id  
@OrderId int, @ProductId int, @SalePrice money, @Quantity int  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (LANGUAGE = N'english', TRANSACTION ISOLATION LEVEL = SNAPSHOT)  
-- compute the value here.   
-- this stored procedure works with single rows only.  
DECLARE @total money = @SalePrice * @Quantity  
UPDATE dbo.OrderDetails   
SET ProductId = @ProductId, SalePrice = @SalePrice, Quantity = @Quantity, Total = @total  
WHERE OrderId = @OrderId  
END  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [메모리 내 OLTP로 마이그레이션](migrating-to-in-memory-oltp.md)  
  
  
