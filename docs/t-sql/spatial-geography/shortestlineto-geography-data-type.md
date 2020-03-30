---
title: ShortestLineTo(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ShortestLineTo_TSQL
- ShortestLineTo
dev_langs:
- TSQL
helpviewer_keywords:
- ShortestLineTo method (geography)
ms.assetid: 9d7c9885-5d1b-49ae-af31-5ef9fb8acaba
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 4832f28fbd07d85c9afaaf7874a51655b6922dc3
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "79090587"
---
# <a name="shortestlineto-geography-data-type"></a>ShortestLineTo(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  두 **geography** 인스턴스 사이의 최단 거리를 나타내는 두 점과 함께 **LineString** 인스턴스를 반환합니다. 반환된 **LineString** 인스턴스의 길이는 두 **geography** 인스턴스 사이의 거리입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.ShortestLineTo ( geography_other )  
```  
  
## <a name="arguments"></a>인수  
 *geography_other*  
 **geography** 인스턴스를 호출하여 최단 거리를 확인하려는 두 번째 **geography** 인스턴스를 지정합니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>설명  
 이 메서드는 비교할 두 **geography** 인스턴스가 교차하지 않을 때 해당 테두리에 있는 엔드포인트와 함계 **LineString** 인스턴스를 반환합니다. 반환된 **LineString**의 길이는 두 **geography** 인스턴스 사이의 최단 거리와 같습니다. 두 **geography** 인스턴스가 서로 교차할 경우 빈 **LineString** 인스턴스가 반환됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-calling-shortestlineto-on-non-intersecting-instances"></a>A. 교차하지 않는 인스턴스에서 ShortestLineTo() 호출  
 다음 예에서는 `CircularString` 인스턴스와 `LineString` 인스턴스 사이의 최단 거리를 찾고 두 점을 연결하는 `LineString` 인스턴스를 반환합니다.  
  
 ```
 DECLARE @g1 geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 DECLARE @g2 geography = 'LINESTRING(-119.119263 46.183634, -119.273071 47.107523, -120.640869 47.569114, -122.200928 47.454094)';  
 SELECT @g1.ShortestLineTo(@g2).ToString();
 ```  
  
### <a name="b-calling-shortestlineto-on-intersecting-instances"></a>B. 교차하는 인스턴스에서 ShortestLineTo() 호출  
 다음 예에서는 `LineString` 인스턴스가 `LineString` 인스턴스와 교차하기 때문에 빈 `CircularString` 인스턴스를 반환합니다.  
  
 ```
 DECLARE @g1 geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 DECLARE @g2 geography = 'LINESTRING(-119.119263 46.183634, -119.273071 47.107523, -120.640869 47.569114, -122.348 47.649, -122.681 47.655)';  
 SELECT @g1.ShortestLineTo(@g2).ToString();
``` 
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
 [ShortestLineTo(geometry 데이터 형식)](../../t-sql/spatial-geometry/shortestlineto-geometry-data-type.md)  
  
