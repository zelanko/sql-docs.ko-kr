---
title: "기 하 도형 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: geometry
dev_langs: TSQL
helpviewer_keywords:
- spatial data types [SQL Server]
- geometry data type [SQL Server], Transact-SQL
ms.assetid: 3fefdf7b-f931-404c-821c-82c0375eaf51
caps.latest.revision: "20"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 988bfaaa5e1b28fa871836641b12517626aa7ed3
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="spatial-types---geometry-transact-sql"></a>공간 형식-geometry (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  평면 공간 데이터 형식인 **geometry**에서 공용 언어 런타임 (CLR) 데이터 형식으로 구현 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 이 데이터 형식은 유클리드(평면) 좌표 시스템의 데이터를 나타냅니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대 한 메서드 집합이 지원는 **geometry** 공간 데이터 형식입니다. 이러한 메서드에 대 한 메서드가 있습니다 **geometry** Open Geospatial Consortium (OGC) 표준과의 집합으로 정의한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 표준에 대 한 확장입니다.  
 
 기 하 도형 메서드에 대 한 허용 오차 수 만큼 클 1.0 e-7 * 익스텐트 합니다. 지점 사이의 최대 근사 거리를 참조 하는 익스텐트가 **geometry**개체입니다.
  
## <a name="registering-the-geometry-type"></a>geometry 형식 등록  
 **geometry** 형식은 각 데이터베이스에서 미리 정의되고 사용할 수 있습니다. 다른 CLR 형식을 사용할 때와 동일한 방식으로 **geometry** 형식의 테이블 열을 만들고 **geometry** 데이터에 대한 작업을 수행할 수 있습니다. 이 형식은 지속형 및 비지속형 계산 열에 사용할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-showing-how-to-add-and-query-geometry-data"></a>1. geometry 데이터를 추가하고 쿼리하는 방법 보기  
 다음 두 예에서는 geometry 데이터를 추가하고 쿼리하는 방법을 보여 줍니다. 첫 번째 예에서는 ID 열과 `geometry` 열 `GeomCol1`이 있는 테이블을 만듭니다. 세 번째 열에서는 `geometry` 열을 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현으로 렌더링하고 `STAsText()` 메서드를 사용합니다. 그러고 나면 두 개의 행이 삽입됩니다. 이 중 한 행에는 `LineString` 의 `geometry`인스턴스가 들어 있고, 다른 행에는 `Polygon` 인스턴스가 들어 있습니다.  
  
```sql 
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
    DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable   
    ( id int IDENTITY (1,1),  
    GeomCol1 geometry,   
    GeomCol2 AS GeomCol1.STAsText() );  
GO  
  
INSERT INTO SpatialTable (GeomCol1)  
VALUES (geometry::STGeomFromText('LINESTRING (100 100, 20 180, 180 180)', 0));  
  
INSERT INTO SpatialTable (GeomCol1)  
VALUES (geometry::STGeomFromText('POLYGON ((0 0, 150 0, 150 150, 0 150, 0 0))', 0));  
GO  
```  
  
### <a name="b-returning-the-intersection-of-two-geometry-instances"></a>2. 두 geometry 인스턴스의 교차점 반환  
 두 번째 예에서는 `STIntersection()` 메서드를 사용하여 앞서 삽입한 두 `geometry` 인스턴스가 교차하는 지점을 반환합니다.  
  
```sql  
DECLARE @geom1 geometry;  
DECLARE @geom2 geometry;  
DECLARE @result geometry;  
  
SELECT @geom1 = GeomCol1 FROM SpatialTable WHERE id = 1;  
SELECT @geom2 = GeomCol1 FROM SpatialTable WHERE id = 2;  
SELECT @result = @geom1.STIntersection(@geom2);  
SELECT @result.STAsText();  
```  
  
### <a name="c-using-geometry-in-a-computed-column"></a>3. 계산 열에서 geometry 사용  
 다음 예제에서는 사용 하 여 지속형된 계산된 열 테이블을 만듭니다는 **geometry** 유형입니다.  
  
```sql  
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
    DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable  
(  
    locationId int IDENTITY(1,1),  
    location geometry,  
    deliveryArea as location.STBuffer(10) persisted  
)  
```  
  
## <a name="see-also"></a>관련 항목:  
  [공간 데이터&#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
