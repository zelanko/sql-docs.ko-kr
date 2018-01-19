---
title: "STBuffer (geography 데이터 형식) | Microsoft Docs"
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
- STBuffer (geography Data Type)
- STBuffer_TSQL
dev_langs: TSQL
helpviewer_keywords: STBuffer (geography Data Type)
ms.assetid: cb4deab8-642b-44d9-b3d9-85114d64021e
caps.latest.revision: "19"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b6d744ac8a275d48c1acb65ab7ea7c870692a1a1
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="stbuffer-geography-data-type"></a>STBuffer(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  모든의 합집합을 나타내는 지리 개체를 가리키는 인스턴스와의 거리가 반환은 **geography** 인스턴스는 지정된 된 값 보다 작습니다.  
  
 이 geography 데이터 형식 메서드 지원 **FullGlobe** 인스턴스 또는 반구 보다 큰 공간 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STBuffer ( distance )  
```  
  
## <a name="arguments"></a>인수  
 *distance*  
 형식의 값은 **float** (**double** .NET framework에서)에서 거리를 지정 하는 **geography** 버퍼를 계산할 인스턴스와의 합니다.  
  
 버퍼의 최대 거리는 0.999를 초과할 수 없습니다 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 지구 둘레의 1/2) 또는 전체 구형입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>주의  
 Stbuffer ()와 같은 방식으로 버퍼를 계산 [BufferWithTolerance](../../t-sql/spatial-geography/bufferwithtolerance-geography-data-type.md)로 지정 하 여 *허용 오차* = abs (distance) \* .001 및 *상대*  =  **false**합니다.  
  
 버퍼가 음수 이면의 경계에서 지정 된 거리 내 모든 요소가 제거 된 **geography** 인스턴스.  
  
 `STBuffer()`반환는 **FullGlobe** ; 특정 한 경우에는 인스턴스 예를 들어 `STBuffer()` 반환는 **FullGlobe** 인스턴스는 버퍼 거리가 적도 극 지방 까지의 거리 보다 큰 경우. 버퍼는 전체 구형을 초과할 수 없습니다.  
  
 이 메서드는 throw 된 **ArgumentException** 에 **FullGlobe** 버퍼 거리는 다음과 같은 제한 사항이 초과 하는 인스턴스:  
  
 0.999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 지구 둘레의 1/2)  
  
 최대 거리 제한은 버퍼가 가능한 유연하게 생성되도록 합니다.  
  
 이론적 버퍼와 계산 된 버퍼 간의 오차는 max (허용 오차, 익스텐트 * 1.E-7) 여기서 허용 오차 = 거리 \* .001 합니다. 익스텐트에 대 한 자세한 내용은 참조 하십시오. [geography 데이터 형식 메서드 참조](http://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e)합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 한 `LineString``geography` 인스턴스. 그런 다음 `STBuffer()`를 사용하여 인스턴스에서 1미터 내에 있는 영역을 반환합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STBuffer(1).ToString();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Bufferwithtolerance&#40; geography 데이터 형식 &#41;](../../t-sql/spatial-geography/bufferwithtolerance-geography-data-type.md)   
 [지리 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
