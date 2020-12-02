---
description: STCurveToLine(geography 데이터 형식)
title: STCurveToLine(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STCurveToLine_TSQL
- STCurveToLine
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveToLine method (geography)
ms.assetid: 2f863a85-6168-465a-b32f-bb5e3de58dee
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 2c8674e1e7ccafd59fa550fca690553050f68ffb
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88479311"
---
# <a name="stcurvetoline-geography-data-type"></a>STCurveToLine(geography 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  원호 세그먼트가 포함된 **geography** 인스턴스의 다각형 근사값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STCurveToLine()  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>설명  
 **CircularString** 또는 **CompoundCurve** 인스턴스에 대해 **LineString** 인스턴스를 반환합니다.  
  
 **CurvePolygon** 인스턴스에 대해 **Polygon** 인스턴스를 반환합니다.  
  
 **CircularString**, **CompoundCurve** 또는 **CurvePolygon** 인스턴스를 포함하지 않는 **geography** 인스턴스의 사본을 반환합니다.  
  
 SQL MM 사양과 달리 이 메서드는 다각형 근사값을 계산할 때 z 좌표 값을 사용하지 않습니다. **geography** 인스턴스를 호출할 때 제공되는 모든 z-좌표 값은 무시됩니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `LineString` 인스턴스의 다각형 근사값인 `CircularString` 인스턴스를 반환합니다.  
  
```
 DECLARE @g1 geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 DECLARE @g2 geography;  
 SET @g2 = @g1.STCurveToLine();  
 SELECT @g1.STNumPoints() AS G1, @g2.STNumPoints() AS G2;
 ```  
  
## <a name="see-also"></a>참고 항목  
 [STLength &#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stlength-geography-data-type.md)   
 [STNumPoints &#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stnumpoints-geography-data-type.md)   
 [공간 데이터 형식 개요](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  
