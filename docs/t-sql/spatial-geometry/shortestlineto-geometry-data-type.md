---
title: "ShortestLineTo (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- ShortestLineTo method (geometry)
ms.assetid: 39a2d0e4-4f93-4e94-a27e-6ad9537cfe74
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bc8843ceefe8819d2f314d76b019720863866ed1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="shortestlineto-geometry-data-type"></a>ShortestLineTo(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

반환 된 **LineString** 두 사이의 최단 거리를 나타내는 두 점과 사용 하 여 인스턴스 **geometry** 인스턴스. 길이 **LineString** 반환 된 인스턴스는 둘 사이의 거리 **geometry** 인스턴스.
  
## <a name="syntax"></a>구문  
  
```  
  
.ShortestLineTo ( geometry_other )  
```  
  
## <a name="arguments"></a>인수  
 *geometry_other*  
 두 번째 **geometry** 인스턴스를 호출 하는 **geometry** 인스턴스 최단 거리를 확인 하려고 합니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>주의  
 메서드는 **LineString** 인스턴스는 두 개의 교차 하지 않는의 테두리에 있는 끝점과 함께 **기 하 도형** 비교 되는 인스턴스. 길이 **LineString** 반환된 equals 둘 사이의 최단 거리 **geometry** 인스턴스. 빈 **LineString** 인스턴스가 반환 됩니다 두 **geometry** 인스턴스가 서로 교차 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-calling-shortestlineto-on-non-intersecting-instances"></a>1. 교차하지 않는 인스턴스에서 ShortestLineTo() 호출  
 다음 예에서는 `CircularString` 인스턴스와 `LineString` 인스턴스 사이의 최단 거리를 찾고 두 점을 연결하는 `LineString` 인스턴스를 반환합니다.  
  
```
 DECLARE @g1 geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
 DECLARE @g2 geometry = 'LINESTRING(-4 7, 7 10, 3 7)';  
 SELECT @g1.ShortestLineTo(@g2).ToString();
 ```  
  
### <a name="b-calling-shortestlineto-on-intersecting-instances"></a>2. 교차하는 인스턴스에서 ShortestLineTo() 호출  
 다음 예에서는 `LineString` 인스턴스가 `LineString` 인스턴스와 교차하기 때문에 빈 `CircularString` 인스턴스를 반환합니다.  
  
```
 DECLARE @g1 geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
 DECLARE @g2 geometry = 'LINESTRING(0 5, 7 10, 3 7)';  
 SELECT @g1.ShortestLineTo(@g2).ToString();
 ```  
  
## <a name="see-also"></a>관련 항목:  
 [ShortestLineTo &#40; geography 데이터 형식 &#41;](../../t-sql/spatial-geography/shortestlineto-geography-data-type.md)  
  
  


