---
title: "Temporal 테이블 사용 시나리오 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4b8fa2dd-1790-4289-8362-f11e6d63bb09
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 332787256518605b6f91dab6be012889c0b0aa93
ms.openlocfilehash: 007b40b36317a67c6b9714b89aac0d3324312f30
ms.contentlocale: ko-kr
ms.lasthandoff: 07/31/2017

---
# <a name="temporal-table-usage-scenarios"></a>Temporal 테이블 사용 시나리오
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Temporal 테이블은 일반적으로 데이터 변경 기록을 추적하는 데 필요한 시나리오에서 유용합니다.    
생산성이 상당히 높아지므로 다음 사용 사례에서 Temporal 테이블 사용을 고려하는 것이 좋습니다.  
  
## <a name="data-audit"></a>데이터 감사  
 변경된 사항 및 시기를 추적하고 지정 시간에 법정 분석을 수행하는 데 필요한 중요 정보가 저장된 테이블에서는 temporal 시스템 버전 관리를 사용합니다.    
Temporal 시스템 버전 관리 테이블을 사용하면 개발 주기의 초기 단계에서 데이터 감사 시나리오에 대해 계획하고 필요할 때 기존 응용 프로그램이나 솔루션에 데이터 감사를 추가할 수 있습니다.  
  
 다음 다이어그램에서는 현재(파란색으로 표시) 및 기록 행 버전(회색으로 표시)을 포함한 데이터 샘플을 사용하여 Employee 테이블 시나리오를 보여 줍니다.   
다이어그램의 오른쪽 부분에서는 시간 축에 행 버전을 시각화하고, SYSTEM_TIME 절을 포함하거나 포함하지 않은 temporal 테이블의 여러 쿼리 형식으로 선택하는 행을 시각화합니다.  
  
 ![TemporalUsageScenario1](../../relational-databases/tables/media/temporalusagescenario1.png "TemporalUsageScenario1")  
  
### <a name="enabling-system-versioning-on-a-new-table-for-data-audit"></a>데이터 감사를 위해 새 테이블에 시스템 버전 관리를 사용하도록 설정  
 데이터 감사가 필요한 정보를 파악하고 나면 temporal 시스템 버전이 관리되는 데이터베이스 테이블을 만듭니다. 다음의 간단한 예제에서는 가상 HR 데이터베이스에서 직원 정보를 사용하는 시나리오를 보여 줍니다.  
  
```  
CREATE TABLE Employee   
(    
  [EmployeeID] int NOT NULL PRIMARY KEY CLUSTERED   
  , [Name] nvarchar(100) NOT NULL  
  , [Position] varchar(100) NOT NULL   
  , [Department] varchar(100) NOT NULL  
  , [Address] nvarchar(1024) NOT NULL  
  , [AnnualSalary] decimal (10,2) NOT NULL  
  , [ValidFrom] datetime2 (2) GENERATED ALWAYS AS ROW START  
  , [ValidTo] datetime2 (2) GENERATED ALWAYS AS ROW END  
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)  
 )    
 WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.EmployeeHistory));  
```  
  
 시스템에서 버전이 관리되는 temporal 테이블을 만드는 다양한 옵션은 [시스템 버전 temporal 테이블 만들기](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)에 설명되어 있습니다.  
  
### <a name="enabling-system-versioning-on-an-existing-table-for-data-audit"></a>데이터 감사를 위해 기존 테이블에 시스템 버전 관리를 사용하도록 설정  
 기존 데이터베이스에서 데이터 감사를 수행해야 할 경우 시스템 버전이 관리되도록 ALTER TABLE을 사용하여 비temporal 테이블을 확장합니다. [비temporal 테이블을 시스템 버전 temporal 테이블로 변경](https://msdn.microsoft.com/library/mt590957.aspx#Anchor_3)에 설명된 대로 응용 프로그램에서 새로운 변경이 발생하지 않도록 HIDDEN으로 기간 열을 추가합니다. 다음 예제에서는 가상 HR 데이터베이스에 있는 기존 직원 테이블에서 시스템 버전 관리를 사용하도록 설정하는 방법을 보여 줍니다.  
  
```  
/*   
Turn ON system versioning in Employee table in two steps   
(1) add new period columns (HIDDEN)   
(2) create default history table   
*/   
ALTER TABLE Employee   
ADD   
    ValidFrom datetime2 (2) GENERATED ALWAYS AS ROW START HIDDEN    
        constraint DF_ValidFrom DEFAULT DATEADD(second, -1, SYSUTCDATETIME())  
    , ValidTo datetime2 (2)  GENERATED ALWAYS AS ROW END HIDDEN     
        constraint DF_ValidTo DEFAULT '9999.12.31 23:59:59.99'  
    , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo);   
  
ALTER TABLE Employee    
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.Employee_History));  
```  
  
 위의 스크립트를 실행하고 나면 모든 데이터 변경 사항이 기록 테이블에 투명하게 수집됩니다.    
일반적인 데이터 감사 시나리오에서는 관심 있는 기간에 개별 행에 적용된 모든 데이터 변경에 대해 쿼리합니다. 이 사용 사례를 효율적으로 보여줄 수 있도록 기본 기록 테이블은 클러스터형 행-저장소 B-트리로 만들어집니다.  
  
### <a name="performing-data-analysis"></a>데이터 분석 수행  
 위의 방법 중 하나를 사용하여 시스템 버전 관리를 사용하도록 설정하고 나면 데이터 감사에서 한 개의 쿼리가 해결되었습니다. 다음 쿼리는 2014년 1월 1일부터 2015년 1월 1일(포함) 사이에 활성 상태로 있었던 EmployeeID가 1000인 Employee 레코드에 대한 행 버전을 검색합니다.  
  
```  
SELECT * FROM Employee   
    FOR SYSTEM_TIME    
        BETWEEN '2014-01-01 00:00:00.0000000' AND '2015-01-01 00:00:00.0000000'   
            WHERE EmployeeID = 1000 ORDER BY ValidFrom;  
```  
  
 FOR SYSTEM_TIME BETWEEN...AND를 FOR SYSTEM_TIME ALL로 바꿔 특정 직원에 대한 데이터 변경의 전체 기록을 분석합니다.  
  
```  
SELECT * FROM Employee   
    FOR SYSTEM_TIME ALL WHERE    
        EmployeeID = 1000 ORDER BY ValidFrom;  
```  
  
 범위를 벗어나지 않고 기간 내에서만 활성 상태인 행 버전을 검색하려면 CONTAINED IN을 사용합니다. 이 쿼리는 기록 테이블만 쿼리하므로 매우 효율적입니다.  
  
```  
SELECT * FROM Employee FOR SYSTEM_TIME    
    CONTAINED IN ('2014-01-01 00:00:00.0000000', '2015-01-01 00:00:00.0000000')   
        WHERE EmployeeID = 1000 ORDER BY ValidFrom;  
```  
  
 마지막으로 일부 감사 시나리오에서는 과거의 지정 시간의 전체 테이블 모습을 볼 수도 있습니다.  
  
```  
SELECT * FROM Employee FOR SYSTEM_TIME AS OF '2014-01-01 00:00:00.0000000' ;  
```  
  
 시스템 버전 관리 temporal 테이블에서는 UTC 표준 시간대의 기간 열에 대한 값이 저장됩니다. 하지만 데이터를 필터링하고 결과를 표시하기 위해서는 현지 표준 시간대를 사용하여 작업하는 것이 항상 좀 더 편리합니다. 다음 코드 예제에서는 SQL Server 2016에 도입된 AT TIME ZONE을 사용하여 원래 현지 표준 시간대에 지정되었다가 UTC로 변환된 필터링 조건을 적용하는 방법에 대해 보여 줍니다.  
  
```  
/*Add offset of the local time zone to current time*/  
DECLARE @asOf DATETIMEOFFSET = GETDATE() AT TIME ZONE 'Pacific Standard Time'  
/*Convert AS OF filter to UTC*/  
SET @asOf = DATEADD (MONTH, -9, @asOf) AT TIME ZONE 'UTC';  
  
SELECT   
    EmployeeID  
    , Name  
    , Position  
    , Department  
    , [Address]  
    , [AnnualSalary]  
    , ValidFrom AT TIME ZONE 'Pacific Standard Time' AS ValidFromPT   
    , ValidTo AT TIME ZONE 'Pacific Standard Time' AS ValidToPT  
FROM Employee   
    FOR SYSTEM_TIME AS OF @asOf where EmployeeId = 1000  
  
```  
  
 AT TIME ZONE을 사용하는 것은 시스템 버전 관리된 테이블이 사용되는 다른 모든 시나리오에 도움이 됩니다.  
  
> [!TIP]  
>  FOR SYSTEM_TIME이 포함된 temporal 절에 지정된 필터링 조건은 SARG 가능합니다. 예를 들어 SQL Server는 기본 클러스터행 인덱스를 활용하여 검색(scan) 작업 대신 찾기(seek)를 수행할 수 있습니다.   
> 기록 테이블을 직접 쿼리하는 경우 \<기간 열>  {< | > | =, …} date_condition AT TIME ZONE ‘UTC’ 형태로 필터를 지정하여 필터링 조건도 SARG 가능하도록 합니다.  
> AT TIME ZONE을 기간 열에 적용하면 SQL Server에서는 테이블/인덱스 검색을 수행하지만 이 작업은 비용이 매우 많이 들 수 있습니다. 쿼리에서  
> \<기간 열>  AT TIME ZONE ‘\<해당 표준 시간대>’  >  {< | > | =, …} date_condition과 같은 조건 형식은 사용하지 마세요.  
  
 참고 항목: [시스템 버전 temporal 테이블의 데이터 쿼리](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)  
  
## <a name="point-in-time-analysis-time-travel"></a>지정 시간 분석(시간 이동)  
 일반적으로 개별 레코드에 발생한 변경에 중점을 두는 데이터 감사와는 달리 시간 이동 시나리오에서 사용자는 시간의 흐름에 따라 전체 데이터 집합이 변경된 방식을 확인할 수 있습니다. 경우에 따라 시간 이동에는 관련 temporal 테이블이 여러 개 포함되어 있으며 각 테이블은 개별적으로 변경됩니다. 이 테이블에서 다음을 분석할 수 있습니다.  
  
-   기록 및 현재 데이터의 중요한 지표에 대한 추세  
  
-   과거의 지정 시간"을 기준으로" 전체 데이터의 정확한 스냅숏(어제, 한 달 전 등)  
  
-   관심 있는 두 지정 시간 간의 차이(예: 한 달 전 vs. 3개월 전)  
  
 실제로 시간 이동 분석이 필요한 시나리오는 많습니다. 이 사용 시나리오를 보여줄 수 있도록 자동 생성 기록을 사용하는 OLTP에 대해 살펴보겠습니다.  
  
### <a name="oltp-with-auto-generated-data-history"></a>자동 생성된 데이터 기록을 사용하는 OLTP  
 트랜잭션 처리 시스템에서는 일반적으로 시간의 흐름에 따라 중요한 메트릭이 변경되는 방식을 분석합니다. 이상적으로는 데이터의 최신 상태에 액세스할 때 대기 시간과 데이터 잠금이 최소한으로 발생되어야 하므로 OLTP 응용 프로그램에서는 기록 분석으로 인해 성능이 저하되면 안 됩니다.  시스템 버전 관리된 temporal 테이블은 사용자가 전체 변경 내역을 나중에 분석할 수 있도록 현재 데이터와는 별도로 투명하게 유지하여 주 OLTP 작업에 영향이 최소한으로 미칠 수 있도록 디자인되었습니다.  
부하가 높은 트랜잭션 처리 작업을 위해서는 [메모리 최적화 테이블을 포함한 시스템 버전 temporal 테이블](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)을 사용하는 것이 좋습니다. 이렇게 하면 현재 메모리 내 데이터와 디스크의 전체 변경 기록을 비용 효율적인 방식으로 저장할 수 있습니다.  
  
 기록 테이블의 경우 다음과 같은 이유로 클러스터형 columnstore 인덱스를 사용하는 것이 좋습니다.  
  
-   일반적인 추세 분석에서는 클러스터형 columnstore 인덱스에서 제공하는 쿼리 성능을 활용합니다.  
  
-   메모리 최적화 테이블이 있는 데이터 플러시 작업은 기록 테이블에 클러스터형 columnstore 인덱스가 있을 때 부하가 높은 OLTP 작업에서도 최고의 성능을 보여 줍니다.  
  
-   클러스터형 columnstore 인덱스는 일부 열이 동시에 변경되지 않는 시나리오에서 특히 뛰어난 압축 기능을 제공합니다.  
  
 메모리 내 OLTP에 temporal 테이블을 사용하면 메모리 내 전체 데이터 집합을 유지해야 하는 부담을 덜고 핫 데이터와 콜드 데이터를 쉽게 구분할 수 있게 됩니다.  
이 범주에 잘 맞는 실제 시나리오의 예로 인벤토리 관리 또는 환율 거래 등이 있습니다.  
  
 다음 다이어그램은 인벤토리 관리에 사용되는 간단한 데이터 모델을 보여 줍니다.  
  
 ![TemporalUsageInMemory](../../relational-databases/tables/media/temporalusageinmemory.png "TemporalUsageInMemory")  
  
 다음 코드 예제에서는 기록 테이블에서 클러스터형 columnstore 인덱스가 포함된 메모리 내 시스템 버전 관리된 temporal 테이블로 ProductInventory를 만듭니다(기본적으로 만든 행 저장소 인덱스를 실제로 바꿈).  
  
> [!NOTE]  
>  데이터베이스에서 메모리 최적화 테이블 만들기가 허용되어야 합니다. [메모리 최적화 테이블 및 고유하게 컴파일된 저장 프로시저 만들기](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)를 참조하세요.  
  
```  
USE TemporalProductInventory  
GO  
  
BEGIN  
    --If table is system-versioned, SYSTEM_VERSIONING must be set to OFF first   
    IF ((SELECT temporal_type FROM SYS.TABLES WHERE object_id = OBJECT_ID('dbo.ProductInventory', 'U')) = 2)  
    BEGIN  
        ALTER TABLE [dbo].[ProductInventory] SET (SYSTEM_VERSIONING = OFF)  
    END  
    DROP TABLE IF EXISTS [dbo].[ProductInventory]  
       DROP TABLE IF EXISTS [dbo].[ProductInventoryHistory]  
END  
GO  
  
CREATE TABLE [dbo].[ProductInventory]  
(  
    ProductId int NOT NULL,  
    LocationID INT NOT NULL,  
    Quantity int NOT NULL CHECK (Quantity >=0),  
  
    SysStartTime datetime2(0) GENERATED ALWAYS AS ROW START  NOT NULL ,  
    SysEndTime datetime2(0) GENERATED ALWAYS AS ROW END  NOT NULL ,  
    PERIOD FOR SYSTEM_TIME(SysStartTime,SysEndTime),  
  
    --Primary key definition  
    CONSTRAINT PK_ProductInventory PRIMARY KEY NONCLUSTERED (ProductId, LocationId)  
)  
WITH  
(  
    MEMORY_OPTIMIZED=ON,      
    SYSTEM_VERSIONING = ON   
    (          
        HISTORY_TABLE = [dbo].[ProductInventoryHistory],          
        DATA_CONSISTENCY_CHECK = ON  
    )  
)  
  
CREATE CLUSTERED COLUMNSTORE INDEX IX_ProductInventoryHistory ON [ProductInventoryHistory]  
WITH (DROP_EXISTING = ON);  
```  
  
 다음은 위의 모델에서 인벤토리 유지 관리에 대한 절차가 수행되는 방식을 보여 줍니다.  
  
```  
CREATE PROCEDURE [dbo].[spUpdateInventory]  
@productId int,  
@locationId int,  
@quantityIncrement int  
  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL=SNAPSHOT, LANGUAGE=N'English')  
    UPDATE dbo.ProductInventory  
        SET Quantity = Quantity + @quantityIncrement   
            WHERE ProductId = @productId AND LocationId = @locationId  
  
/*If zero rows were updated than this is insert of the new product for a given location*/  
    IF @@rowcount = 0  
        BEGIN  
            IF @quantityIncrement < 0  
                SET @quantityIncrement = 0  
            INSERT INTO [dbo].[ProductInventory]  
                (  
                    [ProductId]  
                    ,[LocationID]  
                    ,[Quantity]  
                )  
                VALUES  
                   (  
                        @productId  
                       ,@locationId  
                       ,@quantityIncrement  
        END  
END;  
```  
  
 SpUpdateInventory 저장 프로시저에서는 인벤토리에 새 제품을 삽입하거나 특정 위치에 대한 제품 수량을 업데이트합니다. 비즈니스 논리는 매우 간단하며, 테이블 업데이트를 통해 수량 필드를 증분/감소시켜 항상 최신 상태를 정확하게 유지하는 데 중점을 둡니다. 반면 시스템 버전 관리된 테이블은 아래 다이아그램에 표시된 대로 데이터에 기록 차원을 투명하게 추가합니다.  
  
 ![TemporalUsageInMemory2b](../../relational-databases/tables/media/temporalusageinmemory2b.png "TemporalUsageInMemory2b")  
  
 이제 최신 상태에 대한 쿼리를 네이티브 컴파일 모듈에서 효율적으로 수행할 수 있습니다.  
  
```  
CREATE PROCEDURE [dbo].[spQueryInventoryLatestState]  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL=SNAPSHOT, LANGUAGE=N'English')  
    SELECT ProductId, LocationID, Quantity, SysStartTime  
      FROM dbo.ProductInventory  
    ORDER BY ProductId, LocationId  
END;  
GO  
EXEC [dbo].[spQueryInventoryLatestState];  
```  
  
 시간의 흐름에 따라 데이터 변경을 분석하는 작업은 다음 예에서와 같이 FOR SYSTEM_TIME ALL 절을 사용하면 매우 간편해집니다.  
  
```  
DROP VIEW IF EXISTS vw_GetProductInventoryHistory;  
GO  
CREATE VIEW vw_GetProductInventoryHistory  
AS  
   SELECT ProductId, LocationId, Quantity, SysStartTime, SysEndTime   
   FROM [dbo].[ProductInventory]  
   FOR SYSTEM_TIME ALL;  
GO  
SELECT * FROM vw_GetProductInventoryHistory   
    WHERE ProductId = 2;  
```  
  
 아래 다이어그램은 파워 쿼리, Power BI 또는 유사한 비즈니스 인텔리전스 도구에서 위의 보기를 가져와 쉽게 렌더링할 수 있는 제품 한 개에 대한 데이터 기록을 보여 줍니다.  
  
 ![ProductHistoryOverTime](../../relational-databases/tables/media/producthistoryovertime.png "ProductHistoryOverTime")  
  
 이 시나리오에서는 temporal 테이블을 사용하여 과거의 지정 시간을 기준으로 인벤토리 상태를 다시 생성하거나 다른 시간에 속해 있는 스냅숏을 비교하는 작업과 같이 다른 형식의 시간 이동 분석을 수행합니다.  
  
 이 사용 시나리오의 경우 Product 및 Location 테이블을 확장하여 temporal 테이블로 설정할 수도 있습니다. 이렇게 하면 UnitPrice 및 NumberOfEmployee의 변경 기록을 나중에 분석할 수 있습니다.  
  
```  
ALTER TABLE Product   
ADD   
    SysStartTime datetime2 (2) GENERATED ALWAYS AS ROW START HIDDEN    
        constraint DF_ValidFrom DEFAULT DATEADD(second, -1, SYSUTCDATETIME())  
    , SysEndTime datetime2 (2)  GENERATED ALWAYS AS ROW END HIDDEN     
        constraint DF_ValidTo DEFAULT '9999.12.31 23:59:59.99'  
    , PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime);   
  
ALTER TABLE Product    
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.ProductHistory));  
  
ALTER TABLE [Location]  
ADD   
    SysStartTime datetime2 (2) GENERATED ALWAYS AS ROW START HIDDEN    
        constraint DFValidFrom DEFAULT DATEADD(second, -1, SYSUTCDATETIME())  
    , SysEndTime datetime2 (2)  GENERATED ALWAYS AS ROW END HIDDEN     
        constraint DFValidTo DEFAULT '9999.12.31 23:59:59.99'  
    , PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime);  
  
ALTER TABLE [Location]    
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.LocationHistory));  
```  
  
 데이터 모델은 이제 여러 개의 temporal 테이블에 연결되므로 시점 기준 분석을 위해서는 관련 테이블에서 필요한 데이터를 추출하는 보기를 만들고, 이 보기에 FOR SYSTEM_TIME AS OF를 적용하는 것이 가장 좋습니다. 이렇게 하면 전체 데이터 모델 상태가 매우 간편하게 다시 생성됩니다.  
  
```  
DROP VIEW IF EXISTS vw_ProductInventoryDetails;  
GO  
  
CREATE VIEW vw_ProductInventoryDetails  
AS  
    SELECT PrInv.ProductId ,PrInv.LocationId, P.ProductName, L.LocationName, PrInv.Quantity  
    , P.UnitPrice, L.NumberOfEmployees  
    , P.SysStartTime AS ProductStartTime, P.SysEndTime AS ProductEndTime  
    , L.SysStartTime AS LocationStartTime, L.SysEndTime AS LocationEndTime  
    , PrInv.SysStartTime AS InventoryStartTime, PrInv.SysEndTime AS InventoryEndTime  
FROM dbo.ProductInventory as PrInv  
JOIN dbo.Product AS P ON PrInv.ProductId = P.ProductID  
JOIN dbo.Location AS L ON PrInv.LocationId = L.LocationID;  
GO  
SELECT * FROM vw_ProductInventoryDetails  
    FOR SYSTEM_TIME AS OF '2015.01.01';   
```  
  
 다음 그림에서는 SELECT 쿼리에 대해 생성된 실행 계획을 보여 줍니다. Temporal 관계를 처리하는 모든 복잡한 작업들이 SQL Server 엔진에서 완벽하게 처리되는 것을 확인할 수 있습니다.  
  
 ![ASOFExecutionPlan](../../relational-databases/tables/media/asofexecutionplan.png "ASOFExecutionPlan")  
  
 다음 코드를 사용하여 두 지정 시간 간(하루 전 및 한 달 전) 제품 인벤토리의 상태를 비교합니다.  
  
```  
DECLARE @dayAgo datetime2 (0) = DATEADD (day, -1, SYSUTCDATETIME());  
DECLARE @monthAgo datetime2 (0) = DATEADD (month, -1, SYSUTCDATETIME());  
  
SELECT   
    inventoryDayAgo.ProductId  
    , inventoryDayAgo.ProductName  
    , inventoryDayAgo.LocationName  
    , inventoryDayAgo.Quantity AS QuantityDayAgo,inventoryMonthAgo.Quantity AS QuantityMonthAgo  
    , inventoryDayAgo.UnitPrice AS UnitPriceDayAgo, inventoryMonthAgo.UnitPrice AS UnitPriceMonthAgo  
FROM vw_ProductInventoryDetails  
FOR SYSTEM_TIME AS OF @dayAgo AS inventoryDayAgo  
JOIN vw_ProductInventoryDetails FOR SYSTEM_TIME AS OF @monthAgo AS inventoryMonthAgo  
    ON inventoryDayAgo.ProductId = inventoryMonthAgo.ProductId AND inventoryDayAgo.LocationId = inventoryMonthAgo.LocationID;  
```  
  
## <a name="anomaly-detection"></a>변칙 검색  
 변칙 검색(또는 이상 값 검색)은 예상되는 패턴을 준수하지 않는 항목 또는 데이터 집합의 다른 항목 ID입니다.   
Temporal 쿼리를 활용하면 특정 패턴을 쉽게 찾을 수 있으므로 시스템 버전 관리된 temporal 테이블을 사용하여 주기적으로 또는 불규칙적으로 발생하는 변칙을 검색할 수 있습니다.  
변칙은 수집하는 데이터 형식과 비즈니스 논리에 따라 달라집니다.  
  
 다음 예제에서는 "급증" 판매량을 검색하는 간단한 논리를 보여 줍니다. 구매한 제품의 기록을 수집하는 temporal 테이블에서 작업한다고 가정해 봅니다.  
  
```  
CREATE TABLE [dbo].[Product]  
                (  
            [ProdID] [int] NOT NULL PRIMARY KEY CLUSTERED  
        , [ProductName] [varchar](100) NOT NULL  
        , [DailySales] INT NOT NULL  
        , [ValidFrom] [datetime2](7) GENERATED ALWAYS AS ROW START NOT NULL  
        , [ValidTo] [datetime2](7) GENERATED ALWAYS AS ROW END NOT NULL  
        , PERIOD FOR SYSTEM_TIME ([ValidFrom], [ValidTo])  
    )  
    WITH( SYSTEM_VERSIONING = ON (HISTORY_TABLE = [dbo].[ProductHistory]   
        , DATA_CONSISTENCY_CHECK = ON ))  
  
```  
  
 다음 다이어그램에서는 시간의 흐름에 따라 발생한 구매를 보여 줍니다.  
  
 ![TemporalAnomalyDetection](../../relational-databases/tables/media/temporalanomalydetection.png "TemporalAnomalyDetection")  
  
 일상 기간 동안에는 구매한 제품 수의 차이가 적다고 가정하면 다음 쿼리에서는 단일 이상 값이 식별됩니다. 바로 인접해 있는 값과 비교할 때 차이가 큰 샘플(2배)이 있고 그 주변 샘플들은 상당한 차이를 보이지 않습니다(20% 미만).  
  
```  
WITH CTE (ProdId, PrevValue, CurrentValue, NextValue, ValidFrom, ValidTo)  
AS  
    (  
        SELECT   
            ProdId, LAG (DailySales, 1, 1) over (partition by ProdId order by ValidFrom) as PrevValue  
            , DailySales, LEAD (DailySales, 1, 1) over (partition by ProdId order by ValidFrom) as NextValue   
             , ValidFrom, ValidTo from Product  
        FOR SYSTEM_TIME ALL  
)  
  
SELECT   
    ProdId  
    , PrevValue  
    , CurrentValue  
    , NextValue  
    , ValidFrom  
    , ValidTo  
    , ABS (PrevValue - NextValue) / convert (float, (CASE WHEN NextValue > PrevValue THEN PrevValue ELSE NextValue END)) as PrevToNextDiff  
    , ABS (CurrentValue - PrevValue) / convert (float, (CASE WHEN CurrentValue > PrevValue THEN PrevValue ELSE CurrentValue END)) as CurrentToPrevDiff  
    , ABS (CurrentValue - NextValue) / convert (float, (CASE WHEN CurrentValue > NextValue THEN NextValue ELSE CurrentValue END)) as CurrentToNextDiff  
FROM CTE   
    WHERE   
        ABS (PrevValue - NextValue) / (CASE WHEN NextValue > PrevValue THEN PrevValue ELSE NextValue END) < 0.2  
            AND ABS (CurrentValue - PrevValue) / (CASE WHEN CurrentValue > PrevValue THEN PrevValue ELSE CurrentValue END) > 2  
            AND ABS (CurrentValue - NextValue) / (CASE WHEN CurrentValue > NextValue THEN NextValue ELSE CurrentValue END) > 2;  
```  
  
> [!NOTE]  
>  이 예는 의도적으로 단순화되었습니다. 프로덕션 시나리오에서는 고급 통계 방법을 사용하여 공통 패턴을 따르지 않는 샘플을 식별할 수 있습니다.  
  
## <a name="slowly-changing-dimensions"></a>느린 변경 차원  
 데이터 웨어하우징에서 차원은 일반적으로 지리 위치, 고객 또는 제품과 같은 엔터티에 대한 비교적 정적 데이터를 포함합니다. 그러나 일부 시나리오의 경우 차원 테이블에서도 데이터 변경 사항을 추적해야 합니다. 예측 가능하지 않은 방법을 사용하고, 팩트 테이블에 적용되는 정기 업데이트 일정에서 벗어난 경우 차원의 수정 발생 빈도가 매우 낮아지는 것을 고려할 때 이러한 차원 테이블 형식을 SCD(느린 변경 차원)라고 합니다.  
  
 변경 기록이 유지되는 방법에 따라 느린 변경 차원 범주가 몇 가지 있습니다.  
  
-   유형 0: 기록이 유지되지 않습니다. 차원 특성은 원래 값을 반영합니다.  
  
-   유형 1: 차원 특성이 최신 값을 반영합니다(이전 값은 덮어 씀).  
  
-   유형 2: 모든 버전의 차원 멤버가 유효 기간을 나타내는 열이 포함된 테이블에서 별도의 행으로 나타납니다.  
  
-   유형 3: 동일한 행에서 추가 열을 사용하여 선택한 특성에 대해 제한된 기록을 유지합니다.  
  
-   유형 4: 원래 차원 테이블에서 최신(현재) 차원 멤버 버전을 유지하는 동안 별도의 테이블에서 기록을 유지합니다.  
  
 SCD 전략을 선택할 때 주로 많은 코드와 복잡한 유지 관리가 필요한 차원 테이블을 정확하게 유지하는 책임은 ETL(추출-변환-로드) 계층에 있습니다.  
  
 SQL Server 2016에서 시스템 버전 관리된 temporal 테이블을 사용하면 데이터 기록이 자동으로 유지되므로 코드의 복잡성을 획기적으로 줄일 수 있습니다. 두 테이블을 사용하는 구현 방법을 고려해볼 때 SQL Server 2016에서 temporal 테이블은 SCD 유형 4에 가장 가깝습니다. 그러나 temporal 쿼리를 사용하면 현재 테이블만 참조할 수 있으므로 SCD 유형 2 사용을 계획하는 환경에서 temporal 테이블을 고려해볼 수도 있습니다.  
  
 일반 차원을 SCD로 변환하려면 새 테이블을 만들거나 기존 테이블을 시스템 버전 관리된 temporal 테이블로 변경하기만 하면 됩니다. 기존 차원 테이블에 기록 데이터가 있는 경우 별도 테이블을 만들고 기록 데이터를 이동하여 현재(실제) 차원 버전을 원래 차원 테이블에서 유지합니다. 그런 다음 ALTER TABLE 구문을 사용하여 미리 정의된 기록 테이블이 있는 시스템 버전 관리된 temporal 테이블에 차원 테이블을 변환합니다.  
  
 다음 예제에서는 해당 프로세스에 대해 설명하고, DimLocation 차원 테이블에 ETL에서 채워지는 datetime2의 null이 아닌 열로 ValidFrom과 ValidTo가 있다고 가정합니다.  
  
```  
/*Move “closed” row versions into newly created history table*/  
SELECT * INTO  DimLocationHistory  
    FROM DimLocation  
        WHERE ValidTo < '9999-12-31 23:59:59.99';  
GO  
/*Create clustered columnstore index which is a very good choice in DW scenarios*/  
CREATE CLUSTERED COLUMNSTORE INDEX IX_DimLocationHistory ON DimLocationHistory  
/*Delete previous versions from DimLocation which will become current table in temporal-system-versioning configuration*/  
DELETE FROM DimLocation  
    WHERE ValidTo < '9999-12-31 23:59:59.99';  
/*Add period definition*/  
ALTER TABLE DimLocation ADD PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo);  
/*Enable system-versioning and bind histiory table to the DimLocation*/  
ALTER TABLE DimLocation SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.DimLocationHistory));  
```  
  
 Nno 추가 코드는 SCD를 만들고 난 후 데이터 웨어하우스 로드 프로세스 중 SCD를 유지할 때 필요합니다.  
  
 다음 그림에서는 SCD 2개(DimLocation과 DimProduct)와 팩트 테이블 1개가 포함된 간단한 시나리오에서 temporal 테이블을 사용하는 방법에 대해 보여 줍니다.  
  
 ![TemporalSCD](../../relational-databases/tables/media/temporalscd.png "TemporalSCD")  
  
 위의 SCD를 보고서에서 사용하려면 쿼리를 효과적으로 조정해야 합니다. 예를 들어 지난 6개월 동안 1인당 판매된 제품 수의 평균과 총 판매액을 계산할 수 있습니다.  분석에 중요한 특성을 변경했을 수도 있는 팩트 테이블과 차원에서의 데이터의 상관 관계가 두 메트릭에 모두 필요합니다(DimLocation.NumOfCustomers, DimProduct.UnitPrice).  다음 쿼리에서는 필요한 메트릭을 올바르게 계산합니다.  
  
```  
DECLARE @now datetime2 = SYSUTCDATETIME()  
DECLARE @sixMonthsAgo datetime2 SET   
    @sixMonthsAgo = DATEADD (month, -12, SYSUTCDATETIME())   
  
SELECT DimProduct_History.ProductId  
   , DimLocation_History.LocationId  
    , SUM(F.Quantity * DimProduct_History.UnitPrice) AS TotalAmount  
    , AVG (F.Quantity/DimLocation_History.NumOfCustomers) AS AverageProductsPerCapita   
FROM FactProductSales F   
/* find corresponding record in SCD history in last 6 months, based on matching fact */  
JOIN DimLocation FOR SYSTEM_TIME BETWEEN @sixMonthsAgo AND @now AS DimLocation_History   
    ON DimLocation_History.LocationId = F.LocationId   
        AND F.FactDate BETWEEN DimLocation_History.ValidFrom AND DimLocation_History.ValidTo   
/* find corresponding record in SCD history in last 6 months, based on matching fact */  
JOIN DimProduct FOR SYSTEM_TIME BETWEEN @sixMonthsAgo AND @now AS DimProduct_History   
    ON DimProduct_History.ProductId = F.ProductId  
        AND F.FactDate BETWEEN DimProduct_History.ValidFrom AND DimProduct_History.ValidTo   
    WHERE F.FactDate BETWEEN @sixMonthsAgo AND @now   
GROUP BY DimProduct_History.ProductId, DimLocation_History.LocationId ;  
```  
  
 **고려 사항:**  
  
-   데이터베이스 트랜잭션 시간을 기반으로 계산된 유효성 검사 기간이 비즈니스 논리에 적합한 경우 SCD에 대한 시스템 버전 관리된 temporal 테이블을 사용할 수 있습니다. 데이터를 로드할 때 지연 시간이 상당한 경우 트랜잭션 시간이 허용되지 않을 수 있습니다.  
  
-   기본적으로 시스템 버전 관리된 temporal 테이블에서는 로딩 후에는 기록 데이터를 변경할 수 없습니다(SYSTEM_VERSIONING을 OFF로 설정한 후 기록 수정 가능). 기록 데이터를 정기적으로 변경하는 경우 제한이 있을 수 있습니다.  
  
-   시스템 버전 관리된 temporal 테이블에서 열 변경 시 행 버전이 생성됩니다. 특정 열 변경 시 새 버전을 표시하지 않으려면 ETL 논리에서 해당 제한 사항을 통합해야 합니다.  
  
-   SCD 테이블에 기록 행 수가 상당할 것으로 예상되는 경우 기록 테이블의 주 저장소 옵션으로 클러스터형 columnstore 인덱스를 사용하는 것이 좋습니다. 이렇게 하면 기록 테이블의 공간이 줄어들어 분석 쿼리 속도가 빨라집니다.  
  
## <a name="repairing-row-level-data-corruption"></a>행 수준 데이터 손상 복구  
 시스템 버전 관리된 temporal 테이블에서 기록 데이터를 사용하여 개별 행을 이전에 캡처된 상태로 빠르게 복구할 수 있습니다. Temporal 테이블의 이 속성은 영향을 받는 행을 찾거나 원하지 않는 데이터 변경 시간을 알고 있을 때 백업을 처리하지 않고 효율적으로 복구를 수행할 수 있으므로 매우 유용합니다.  
  
 이 접근 방법에는 여러 가지 이점이 있습니다.  
  
-   복구 범위를 매우 정확하게 제어할 수 있습니다. 영향을 받지 않는 레코드는 최신 상태로 유지되어야 하며, 종종 중요하게 요구됩니다.  
  
-   작업이 매우 효율적이며 데이터를 사용하는 모든 작업에 대해 데이터베이스가 온라인 상태로 유지됩니다.  
  
-   복구 작업 자체가 버전 관리입니다. 복구 작업 자체에 대한 감사 추적이 가능하므로 필요할 경우 나중에 발생한 내용을 분석할 수 있습니다.  
  
 복구 작업은 비교적 쉽게 자동화할 수 있습니다. 데이터 감사 시나리오에 사용되는 Employee 테이블에 대해 데이터 복구를 수행하는 저장 프로시저의 코드 예제는 다음과 같습니다.  
  
```  
DROP PROCEDURE IF EXISTS sp_RepairEmployeeRecord;  
GO  
  
CREATE PROCEDURE sp_RepairEmployeeRecord   
    @EmployeeID INT,  
    @versionNumber INT = 1  
AS  
  
;WITH History  
AS  
(  
        /* Order historical rows by tehir age in DESC order*/  
        SELECT ROW_NUMBER () OVER (PARTITION BY EmployeeID ORDER BY [ValidTo] DESC) AS RN, *  
        FROM Employee FOR SYSTEM_TIME ALL WHERE YEAR (ValidTo) < 9999 AND Employee.EmployeeID = @EmployeeID  
)  
  
/*Update current row by using N-th row version from history (default is 1 - i.e. last version)*/  
UPDATE Employee   
    SET [Position] = H.[Position], [Department] = H.Department, [Address] = H.[Address], AnnualSalary = H.AnnualSalary  
    FROM Employee E JOIN History H ON E.EmployeeID = H.EmployeeID AND RN = @versionNumber  
    WHERE E.EmployeeID = @EmployeeID  
  
```  
  
 이 저장 프로시저는 @EmployeeID 및 @versionNumber를 입력 매개 변수로 사용합니다. 기본적으로 이 프로시저에서는 행 상태를 기록에서 마지막 버전으로 복원합니다(@versionNumber = 1).  
  
 다음 그림은 프로시저 호출 이전 및 이후 행의 상태를 보여 줍니다. 빨간색 직사각형은 잘못된 현재 행 버전을 표시하고, 녹색 직사각형은 기록에서 올바른 버전을 표시합니다.  
  
 ![TemporalUsageRepair1](../../relational-databases/tables/media/temporalusagerepair1.png "TemporalUsageRepair1")  
  
```  
EXEC sp_RepairEmployeeRecord @EmployeeID = 1, @versionNumber = 1  
```  
  
 ![TemporalUsageRepair2](../../relational-databases/tables/media/temporalusagerepair2.png "TemporalUsageRepair2")  
  
 이 복구 저장 프로시저는 행 버전 대신 정확한 타임스탬프를 허용하도록 정의할 수 있습니다. 이렇게 하면 행이 제공된 지정 시간에 활성 상태였던 버전으로 복원됩니다(예: 지정 시간 기준).  
  
```  
DROP PROCEDURE IF EXISTS sp_RepairEmployeeRecordAsOf;  
GO  
  
CREATE PROCEDURE sp_RepairEmployeeRecordAsOf   
    @EmployeeID INT,  
    @asOf datetime2  
AS  
  
/*Update current row to the state that was actual AS OF provided date*/  
UPDATE Employee   
    SET [Position] = History.[Position], [Department] = History.Department, [Address] = History.[Address], AnnualSalary = History.AnnualSalary  
    FROM Employee AS E JOIN Employee FOR SYSTEM_TIME AS OF @asOf AS History  ON E.EmployeeID = History.EmployeeID  
    WHERE E.EmployeeID = @EmployeeID  
  
```  
  
 동일한 데이터 샘플에 대해 다음 그림은 시간 조건이 포함된 복구 시나리오를 보여 줍니다. @asOf 매개 변수, 제공된 지정 시간에 실제로 있었던 기록에서 선택한 행, 그리고 복구 작업 후 현재 테이블의 새 행 버전이 강조 표시되어 있습니다.  
  
 ![TemporalUsageRepair3](../../relational-databases/tables/media/temporalusagerepair3.png "TemporalUsageRepair3")  
  
 데이터 수정은 데이터 웨어하우징 및 보고 시스템에서 자동화된 데이터 로드 작업에 포함될 수 있습니다.  
새로 업데이트된 값이 올바르지 않으면 여러 시나리오에서 기록에서 이전 버전을 복원하는 것이 문제를 완화시킬 수 있는 충분한 방법입니다. 다음 다이어그램은 이 프로세스를 자동화하는 방법을 보여 줍니다.  
  
 ![TemporalUsageRepair4](../../relational-databases/tables/media/temporalusagerepair4.png "TemporalUsageRepair4")  
  
## <a name="see-also"></a>참고 항목  
 [Temporal 테이블](../../relational-databases/tables/temporal-tables.md)   
 [시스템 버전 관리 temporal 테이블 시작](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Temporal 테이블 시스템 일관성 검사](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Temporal 테이블을 사용하여 분할](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [Temporal 테이블 고려 사항 및 제한 사항](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [Temporal 테이블 보안](../../relational-databases/tables/temporal-table-security.md)   
 [메모리 최적화 테이블을 포함한 시스템 버전 temporal 테이블](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Temporal 테이블 메타데이터 뷰 및 함수](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  

