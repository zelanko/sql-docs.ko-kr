---
title: OR 구현 고유 하 게 컴파일된 저장된 프로시저에서 연산자 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f2528e74-2b1c-48cb-861b-c4e57b51ac35
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ce9b8660fa52d2a09302b51b0f95e368071caa4d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37228183"
---
# <a name="implementing-the-or-operator-in-natively-compiled-stored-procedures"></a>고유하게 컴파일된 저장 프로시저에서 OR 연산자 구현
  OR 연산자는 고유하게 컴파일된 저장 프로시저의 쿼리 조건자에서 지원되지 않습니다. NOT 연산자도 고유하게 컴파일된 저장 프로시저의 쿼리 조건자에서 지원되지 않으므로 동등한 논리 연산자만 사용하여 OR 연산자를 시뮬레이션할 수 없습니다. 그러나 메모리 최적화 테이블 변수를 통해 OR 연산자의 효과를 시뮬레이션할 수 있습니다.  
  
## <a name="or-operator-in-where-clause"></a>WHERE 절의 OR 연산자  
 WHERE 절에 OR 연산자가 있는 경우 다음 방법을 사용하여 해당 동작을 시뮬레이션할 수 있습니다.  
  
1.  적합한 스키마를 사용하여 메모리 최적화 테이블 변수를 만듭니다. 이렇게 하려면 미리 정의된 메모리 최적화 테이블 형식이 필요합니다.  
  
2.  최상위 OR 연산자로 시작하여 OR 연산자로 조인된 조건자에 따라 WHERE 절을 두 부분으로 나눕니다. WHERE 절에 둘 이상의 OR 연산자가 있는 경우 두 번 이상 이 동작을 수행해야 할 수 있습니다. OR 연산자가 남아 있지 않을 때까지 이 단계를 반복합니다. 예를 들어 다음 조건자가 있는 경우  
  
    ```  
    pred1 OR (pred2 AND (pred3 OR pred4)) OR (pred5 AND pred6)  
    ```  
  
     이 단계 후에 다음 조건자가 있어야 합니다.  
  
    ```  
    pred1  
    pred5 AND pred6  
    pred2 AND pred3  
    pred2 AND pred4  
    ```  
  
3.  2단계에 있는 두 부분의 각각을 조건자로 사용하여 쿼리를 실행합니다. 각 쿼리의 결과를 1단계에서 만든 메모리 최적화 테이블 변수에 넣습니다.  
  
4.  필요한 경우 메모리 최적화 테이블 변수에서 중복 항목을 제거합니다.  
  
5.  메모리 최적화 테이블 변수를 쿼리의 결과로 사용합니다.  
  
 다음 샘플에서는 [!INCLUDE[hek_2](../includes/hek-2-md.md)]에 대해 업데이트된 AdventureWorks2012 데이터베이스에서 테이블을 사용합니다. 이 샘플에 대한 파일을 다운로드하려면 [AdventureWorks 데이터베이스 – 2012, 2008R2 및 2008](http://msftdbprodsamples.codeplex.com/releases/view/93587)로 이동하십시오. AdventureWorks2012에 [!INCLUDE[hek_2](../includes/hek-2-md.md)] 코드 샘플을 적용하려면 [SQL Server 2014 메모리 내 OLTP 샘플](https://msftdbprodsamples.codeplex.com/releases/view/114491)로 이동하십시오.  
  
 다음 저장 프로시저를 데이터베이스에 추가합니다. 네이티브 컴파일을 사용하도록 이 저장 프로시저를 변환합니다.  
  
```  
CREATE PROCEDURE Sales.usp_fuzzySearchSalesOrderDetail_ondisk  
  @SalesOrderId int = 0, @SalesOrderDetailId int = 0,   
  @CarrierTrackingNumber nvarchar(25) = N'', @ProductId int = 0,   
  @minUnitPrice money = 0, @maxUnitPrice money = 0  
AS BEGIN  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_ondisk s  
  WHERE  s.SalesOrderId = @SalesOrderId  
      OR s.SalesOrderDetailId = @SalesOrderDetailId  
      OR s.CarrierTrackingNumber = @CarrierTrackingNumber  
      OR s.ProductID = @ProductId  
      OR (s.UnitPrice > @minUnitPrice AND s.UnitPrice < @maxUnitPrice)  
END  
GO  
```  
  
 변환 후 테이블 및 저장 프로시저 스키마는 다음과 같습니다.  
  
```  
CREATE TYPE Sales.fuzzySearchSalesOrderDetailType AS TABLE  
(  
  SalesOrderId int not null,  
  SalesOrderDetailId int not null,  
  ModifiedDate datetime2(7) not null  
  INDEX ix_fuzzySearchSalesOrderDetailType NONCLUSTERED (SalesOrderId, SalesOrderDetailId)  
) WITH (MEMORY_OPTIMIZED = ON)  
GO  
  
CREATE TYPE Sales.fuzzySearchSalesOrderDetailTempType AS TABLE  
(  
  SalesOrderId int not null,  
  SalesOrderDetailId int not null,  
  recordcount int not null  
  INDEX ix_fuzzySearchSalesOrderDetailTempType NONCLUSTERED (SalesOrderId, SalesOrderDetailId)  
) WITH (MEMORY_OPTIMIZED = ON)  
GO  
  
CREATE PROCEDURE Sales.usp_fuzzySearchSalesOrderDetail_inmem  
  @SalesOrderId int = 0, @SalesOrderDetailId int = 0,   
  @CarrierTrackingNumber nvarchar(25) = N'', @ProductId int = 0,   
  @minUnitPrice money = 0, @maxUnitPrice money = 0  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'ENGLISH')  
  
  DECLARE @retValue Sales.fuzzySearchSalesOrderDetailType  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE s.SalesOrderId = @SalesOrderId  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE s.SalesOrderDetailId = @SalesOrderDetailId  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE s.CarrierTrackingNumber COLLATE Latin1_General_BIN2 = @CarrierTrackingNumber COLLATE Latin1_General_BIN2   
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE s.ProductID = @ProductId  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE (s.UnitPrice > @minUnitPrice AND s.UnitPrice < @maxUnitPrice)  
  
  -- After the above statements, there will be duplicates inside @retValue  
  -- Delete the duplicates from @retValue  
  DECLARE @duplicates Sales.fuzzySearchSalesOrderDetailTempType  
  
  INSERT INTO @duplicates (SalesOrderId, SalesOrderDetailId, recordcount)   
  SELECT SalesOrderId, SalesOrderDetailId, COUNT(*) AS recordCount  
  FROM @retValue  
  GROUP BY SalesOrderId, SalesOrderDetailId  
  
  -- Now we have one row per pair  
  -- clear and rebuild the result set  
  DELETE FROM @retValue  
  
  INSERT INTO @retValue  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  JOIN @duplicates d ON s.SalesOrderId = d.SalesOrderId AND s.SalesOrderDetailId = d.SalesOrderDetailId  
  
  -- After this every pair of (SalesOrderId, SalesOrderDetailId) in @retValue should be unique.  
  SELECT SalesorderId, SalesOrderDetailId, ModifiedDate FROM @retValue  
END  
GO  
```  
  
## <a name="or-operator-in-join-condition"></a>JOIN 조건의 OR 연산자  
 SELECT 문의 JOIN 조건에 OR 연산자가 있는 경우 다음 방법을 사용하여 해당 동작을 시뮬레이션할 수 있습니다. JOIN 조건에 둘 이상의 OR 연산자가 있거나 OR 연산자가 포함된 여러 JOIN 조건이 있는 경우 이 동작을 두 번 이상 수행해야 할 수 있습니다.  
  
 OUTER JOIN 조건이 있는 경우 OUTER JOIN 조건 해결 방법과 이 해결 방법을 결합할 수 있습니다.  
  
1.  적합한 스키마를 사용하여 메모리 최적화 테이블 변수를 만듭니다. 이렇게 하려면 미리 정의된 메모리 최적화 테이블 형식이 필요합니다.  
  
2.  OR 연산자로 조인된 조건자에 따라 JOIN 조건의 조건자를 두 부분으로 나눕니다. JOIN 조건이 여러 개 있는 경우 각 JOIN 조건에 대해 이를 수행한 후 결과 조각 조합 집합을 만들어야 할 수 있습니다. 예를 들어 각 JOIN 조건에 OR 연산자가 하나 있는 JOIN 조건이 세 개인 경우 2x2x2=8 조건자를 가질 수 있습니다.  
  
3.  2단계에서 생성된 각 조건자의 경우 해당 결과를 1단계에서 만든 메모리 최적화 테이블 변수에 삽입하는 쿼리를 만듭니다.  
  
4.  필요한 경우 메모리 최적화 테이블 변수에서 중복 항목을 제거합니다.  
  
5.  메모리 최적화 테이블 변수를 쿼리의 결과로 사용합니다.  
  
 다음 샘플에서는 [!INCLUDE[hek_2](../includes/hek-2-md.md)]에 대해 업데이트된 AdventureWorks2012 데이터베이스에서 테이블을 사용합니다. 이 샘플에 대한 파일을 다운로드하려면 [AdventureWorks 데이터베이스 – 2012, 2008R2 및 2008](http://msftdbprodsamples.codeplex.com/releases/view/93587)로 이동하십시오. AdventureWorks2012에 [!INCLUDE[hek_2](../includes/hek-2-md.md)] 코드 샘플을 적용하려면 [SQL Server 2014 메모리 내 OLTP 샘플](https://msftdbprodsamples.codeplex.com/releases/view/114491)로 이동하십시오.  
  
 다음 저장 프로시저를 데이터베이스에 추가합니다. 네이티브 컴파일을 사용하도록 이 저장 프로시저를 변환합니다. 이 샘플에서는 INNER JOIN 조건을 사용합니다.  
  
```  
CREATE PROCEDURE Sales.usp_fuzzySearchSalesSpecialOffers_ondisk  
  @SpecialOfferId int  
AS BEGIN  
  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.SpecialOfferID, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_ondisk s  
  JOIN Sales.SpecialOffer_onDisk offer   
    ON s.SpecialOfferID = offer.SpecialOfferID   
    OR s.ProductID IN (SELECT ProductId FROM Sales.SpecialOfferProduct sop WHERE sop.SpecialOfferID = @SpecialOfferId)  
END  
```  
  
 변환 후 테이블 및 저장 프로시저 스키마는 다음과 같습니다.  
  
```  
CREATE TYPE Sales.fuzzySearchSalesSpecialOffers_Type AS TABLE  
(  
  SalesOrderId int not null,  
  SalesOrderDetailId int not null,  
  SpecialOfferId int not null,  
  ModifiedDate datetime2(7) not null  
  INDEX ix_fuzzySearchSalesSpecialOffers_Type NONCLUSTERED (SalesOrderId, SalesOrderDetailId)  
) WITH (MEMORY_OPTIMIZED = ON)  
GO  
  
CREATE TYPE Sales.fuzzySearchSalesSpecialOffers_TempType AS TABLE  
(  
  SalesOrderId int not null,  
  SalesOrderDetailId int not null,  
  SpecialOfferId int not null,  
  recordcount int null  
  INDEX ix_fuzzySearchSalesSpecialOffers_TempType NONCLUSTERED (SalesOrderId, SalesOrderDetailId)  
) WITH (MEMORY_OPTIMIZED = ON)  
GO  
  
CREATE PROCEDURE Sales.usp_fuzzySearchSalesSpecialOffers_inmem  
  @SpecialOfferId int  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'ENGLISH')  
  
  DECLARE @retValue Sales.FuzzySearchSalesSpecialOffers_Type  
  
  -- Find all special offers matching the conditions  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, SpecialOfferid, ModifiedDate)  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.SpecialOfferID, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  JOIN Sales.SpecialOffer_inmem offer   
    ON s.SpecialOfferID = offer.SpecialOfferID  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, SpecialOfferid, ModifiedDate)  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.SpecialOfferID, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  JOIN Sales.SpecialOfferProduct_inmem sop   
    ON sop.SpecialOfferId = @SpecialOfferId AND s.ProductID = sop.ProductId  
  
  -- Now we need to remove the duplicates from @matchingSpecialOffers  
  DECLARE @duplicates Sales.fuzzySearchSalesSpecialOffers_TempType  
  
  INSERT INTO @duplicates (SalesOrderId, SalesOrderDetailId, SpecialOfferid, recordcount)  
  SELECT SalesOrderId, SalesOrderDetailId, SpecialOfferId, COUNT(*)   
  FROM @retValue  
  GROUP BY SalesOrderId, SalesOrderDetailId, SpecialOfferId  
  
  -- now there should be no duplicates within @duplicate  
  -- use @duplicate for join.  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.SpecialOfferID, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  JOIN @duplicates offer   
    ON    s.SalesOrderId = offer.SalesOrderId   
      AND s.SalesOrderDetailId = offer.SalesOrderDetailID   
      AND s.SpecialOfferId = offer.SpecialOfferId  
END  
GO  
```  
  
## <a name="side-effects"></a>부작용  
 WHERE 절 또는 JOIN 조건에 OR 연산자가 둘 이상 있는 경우 동작을 시뮬레이션하는 데 실행해야 하는 쿼리 수가 기하급수적으로 증가할 수 있습니다. 이로 인해 쿼리 성능이 저하되고, 메모리 최적화 테이블 변수를 사용해야 하므로 메모리 사용량이 증가할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [고유하게 컴파일된 저장 프로시저의 마이그레이션 문제](../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)  
  
  
