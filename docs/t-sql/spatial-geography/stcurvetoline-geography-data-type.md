---
title: "STCurveToLine (geography 데이터 형식) | Microsoft Docs"
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
f1_keywords:
- STCurveToLine_TSQL
- STCurveToLine
dev_langs: TSQL
helpviewer_keywords: STCurveToLine method (geography)
ms.assetid: 2f863a85-6168-465a-b32f-bb5e3de58dee
caps.latest.revision: "12"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 67b5f37ac6dd928f114ac1c224806387074ea97d
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="stcurvetoline-geography-data-type"></a>STCurveToLine(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  다각형 근사값을 반환 합니다.는 **geography** 원호 세그먼트가 포함 된 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STCurveToLine()  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>주의  
 반환 된 **LineString** 에 대 한 인스턴스는 **CircularString** 또는 **CompoundCurve** 인스턴스.  
  
 반환 된 **다각형** 에 대 한 인스턴스는 **CurvePolygon** 인스턴스.  
  
 복사본을 반환 **geography** 포함 하지 않는 인스턴스 **CircularString**, **CompoundCurve**, 또는 **CurvePolygon** 인스턴스.  
  
 SQL MM 사양과 달리이 메서드는 다각형 근사값 계산에 z 좌표 값을 사용 하지 않습니다. Z 좌표 값 호출할 때 제공 **geography** 인스턴스는 무시 됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `LineString` 인스턴스의 다각형 근사값인 `CircularString` 인스턴스를 반환합니다.  
  
```
 DECLARE @g1 geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 DECLARE @g2 geography;  
 SET @g2 = @g1.STCurveToLine();  
 SELECT @g1.STNumPoints() AS G1, @g2.STNumPoints() AS G2;
 ```  
  
## <a name="see-also"></a>관련 항목:  
 [Stlength&#40; geography 데이터 형식 &#41;](../../t-sql/spatial-geography/stlength-geography-data-type.md)   
 [Stnumpoints&#40; geography 데이터 형식 &#41;](../../t-sql/spatial-geography/stnumpoints-geography-data-type.md)   
 [공간 데이터 형식 개요](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  
