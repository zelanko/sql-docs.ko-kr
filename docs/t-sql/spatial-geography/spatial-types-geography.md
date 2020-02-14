---
title: geography(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- geography
dev_langs:
- TSQL
helpviewer_keywords:
- geography data type [SQL Server], Transact-SQL
- spatial data types [SQL Server]
ms.assetid: d9e4952a-1841-4465-a64b-11e9288dba1d
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 5b98f2283cfb9d89277ad97ffc7a883e43a42b4f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68042523"
---
# <a name="spatial-types---geography"></a>공간 형식 - geography
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  geography 공간 데이터 형식인 **geography**는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 .NET CLR(공용 언어 런타임) 데이터 형식으로 구현됩니다. 이 데이터 형식은 둥근 표면 좌표 시스템의 데이터를 나타냅니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **geography** 데이터 형식은 GPS 위도 및 경도 좌표 등의 타원(둥근 표면) 데이터를 저장합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 **gegraphy** 공간 데이터 형식에 대해 메서드 집합을 지원합니다. 이러한 메서드에는 OGC(Open Geospatial Consortium) 표준과 해당 표준에 대한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 확장의 집합으로 정의된 **geography**의 메서드가 포함됩니다.  
 
 **geography** 메서드의 허용 오차는 1.0e-7 * 익스텐트와 같을 수 있습니다. 익스텐트는 **geography** 개체의 점 사이의 최대 근사 거리를 나타냅니다.
  

## <a name="registering-the-geography-type"></a>geography 형식 등록  
 **geography** 형식은 각 데이터베이스에서 미리 정의되고 사용할 수 있습니다. 다른 시스템 제공 형식을 사용할 때와 동일한 방식으로 **geography** 형식의 테이블 열을 만들고 **geography** 데이터에 대한 작업을 수행할 수 있습니다. 이 형식은 지속형 및 비지속형 계산 열에 사용할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-showing-how-to-add-and-query-geography-data"></a>A. geography 데이터를 추가하고 쿼리하는 방법 보기  
 다음 예에서는 geography 데이터를 추가하고 쿼리하는 방법을 보여 줍니다. 첫 번째 예에서는 ID 열과 `geography` 열 `GeogCol1`이 있는 테이블을 만듭니다. 세 번째 열에서는 `geography` 열을 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현으로 렌더링하고 `STAsText()` 메서드를 사용합니다. 그러고 나면 두 개의 행이 삽입됩니다. 이 중 한 행에는 `LineString` 의 `geography`인스턴스가 들어 있고, 다른 행에는 `Polygon` 인스턴스가 들어 있습니다.  
  
```  
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
    DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable   
    ( id int IDENTITY (1,1),  
    GeogCol1 geography,   
    GeogCol2 AS GeogCol1.STAsText() );  
GO  
  
INSERT INTO SpatialTable (GeogCol1)  
VALUES (geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656 )', 4326));  
  
INSERT INTO SpatialTable (GeogCol1)  
VALUES (geography::STGeomFromText('POLYGON((-122.358 47.653 , -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326));  
GO  
```  
  
### <a name="b-returning-the-intersection-of-two-geography-instances"></a>B. 두 geography 인스턴스의 교차점 반환  
 다음 예에서는 `STIntersection()` 메서드를 사용하여 앞에서 삽입한 두 개의 `geography` 인스턴스가 교차하는 지점을 반환합니다.  
  
```  
DECLARE @geog1 geography;  
DECLARE @geog2 geography;  
DECLARE @result geography;  
  
SELECT @geog1 = GeogCol1 FROM SpatialTable WHERE id = 1;  
SELECT @geog2 = GeogCol1 FROM SpatialTable WHERE id = 2;  
SELECT @result = @geog1.STIntersection(@geog2);  
SELECT @result.STAsText();  
```  
  
### <a name="c-using-geography-in-a-computed-column"></a>C. 계산 열에 geography 사용  
 다음 예제에서는 **geography** 형식을 사용하여 지속형 계산 열이 있는 테이블을 만듭니다.  
  
```  
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
    DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable  
(  
    locationId int IDENTITY(1,1),  
    location geography,  
    deliveryArea as location.STBuffer(10) persisted  
)  
```  
  
## <a name="see-also"></a>참고 항목  
 [공간 데이터&#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)   

  
  
