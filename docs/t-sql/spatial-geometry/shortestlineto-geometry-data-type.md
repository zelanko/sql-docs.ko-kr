---
description: ShortestLineTo(geometry 데이터 형식)
title: ShortestLineTo(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- ShortestLineTo method (geometry)
ms.assetid: 39a2d0e4-4f93-4e94-a27e-6ad9537cfe74
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: bd22be1b41ec9213d8e42c66f4de187581d7381d
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88422297"
---
# <a name="shortestlineto-geometry-data-type"></a>ShortestLineTo(geometry 데이터 형식)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

두 **geometry** 인스턴스 사이의 최단 거리를 나타내는 두 점과 함께 **LineString** 인스턴스를 반환합니다. 반환된 **LineString** 인스턴스의 길이는 두 **geometry** 인스턴스 사이의 거리입니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.ShortestLineTo ( geometry_other )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *geometry_other*  
 **geometry** 인스턴스를 호출하여 최단 거리를 확인하려는 두 번째 **geometry** 인스턴스입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geometry**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>설명  
 이 메서드는 비교할 교차하지 않는 두 **geometry** 인스턴스의 테두리에 있는 엔드포인트와 함께 **LineString** 인스턴스를 반환합니다. 반환된 **LineString** 의 길이는 두 **geometry** 인스턴스 사이의 최단 거리와 같습니다. 두 **geometry** 인스턴스가 서로 교차할 경우 빈 **LineString** 인스턴스가 반환됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-calling-shortestlineto-on-non-intersecting-instances"></a>A. 교차하지 않는 인스턴스에서 ShortestLineTo() 호출  
 다음 예에서는 `CircularString` 인스턴스와 `LineString` 인스턴스 사이의 최단 거리를 찾고 두 점을 연결하는 `LineString` 인스턴스를 반환합니다.  
  
```
 DECLARE @g1 geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
 DECLARE @g2 geometry = 'LINESTRING(-4 7, 7 10, 3 7)';  
 SELECT @g1.ShortestLineTo(@g2).ToString();
 ```  
  
### <a name="b-calling-shortestlineto-on-intersecting-instances"></a>B. 교차하는 인스턴스에서 ShortestLineTo() 호출  
 다음 예에서는 `LineString` 인스턴스가 `LineString` 인스턴스와 교차하기 때문에 빈 `CircularString` 인스턴스를 반환합니다.  
  
```
 DECLARE @g1 geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
 DECLARE @g2 geometry = 'LINESTRING(0 5, 7 10, 3 7)';  
 SELECT @g1.ShortestLineTo(@g2).ToString();
 ```  
  
## <a name="see-also"></a>참고 항목  
 [ShortestLineTo&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/shortestlineto-geography-data-type.md)  
  
  

