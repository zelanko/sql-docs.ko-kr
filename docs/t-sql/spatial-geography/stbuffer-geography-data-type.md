---
title: STBuffer(지리 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STBuffer (geography Data Type)
- STBuffer_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STBuffer (geography Data Type)
ms.assetid: cb4deab8-642b-44d9-b3d9-85114d64021e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6a07686a0aefb9b5d41e8c6f231c57214b75f687
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51702761"
---
# <a name="stbuffer-geography-data-type"></a>STBuffer(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  **geography** 인스턴스와의 거리가 지정된 값보다 작거나 같은 모든 점의 통합을 나타내는 지리 개체를 반환합니다.  
  
 이 geography 데이터 형식 메서드는 **FullGlobe** 인스턴스 또는 반구보다 큰 공간 인스턴스를 지원합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STBuffer ( distance )  
```  
  
## <a name="arguments"></a>인수  
 *distance*  
 해당 버퍼를 계산할 **geography** 인스턴스와의 거리를 지정하는 **float**(.NET Framework의 경우 **double**) 형식의 값입니다.  
  
 버퍼의 최대 거리는 0.999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 지구 둘레의 1/2) 또는 전체 구형을 초과할 수 없습니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 STBuffer()는 *tolerance* = abs(distance) \* .001 및 *relative* = **false** 지정을 통해 [BufferWithTolerance](../../t-sql/spatial-geography/bufferwithtolerance-geography-data-type.md)와 동일한 방식으로 버퍼를 계산합니다.  
  
 버퍼가 음수이면 **geography** 인스턴스 경계에서 지정된 거리 내에 있는 모든 요소가 제거됩니다.  
  
 `STBuffer()`는 경우에 따라 **FullGlobe** 인스턴스를 반환합니다. 예를 들어 `STBuffer()`는 버퍼 거리가 적도에서 극지방까지의 거리보다 큰 경우 두 극지방에서 **FullGlobe** 인스턴스를 반환합니다. 버퍼는 전체 구형을 초과할 수 없습니다.  
  
 이 메서드는 버퍼 거리가 다음 제한을 초과하는 경우 **FullGlobe** 인스턴스에서 **ArgumentException**을 생성합니다.  
  
 0.999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 지구 둘레의 1/2)  
  
 최대 거리 제한은 버퍼가 가능한 유연하게 생성되도록 합니다.  
  
 이론적 버퍼와 계산된 버퍼 간의 오차는 허용 오차 = 거리 \* .001인 max(허용 오차, 익스텐트 * 1.E-7)입니다. 익스텐트에 대한 자세한 내용은 [geometry 데이터 형식 메서드 참조](https://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e)를 확인하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 `LineString``geography` 인스턴스를 만듭니다. 그런 다음 `STBuffer()`를 사용하여 인스턴스에서 1미터 내에 있는 영역을 반환합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STBuffer(1).ToString();  
```  
  
## <a name="see-also"></a>참고 항목  
 [BufferWithTolerance &#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/bufferwithtolerance-geography-data-type.md)   
 [지리 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
