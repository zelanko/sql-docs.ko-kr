---
title: "BufferWithTolerance (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BufferWithTolerance_TSQL
- BufferWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- BufferWithTolerance (geometry Data Type)
ms.assetid: 7049d37a-3e72-4e93-87a1-c96a6f0e2b99
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ffa8a350cb4531f9d4a6d1439a4dad0682189266
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="bufferwithtolerance-geometry-data-type"></a>BufferWithTolerance(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

반환 값 인스턴스와의 거리가 모든 점의 합집합을 나타내는 기하학적 개체는 **기 하 도형** 인스턴스는 지정된 된 허용 오차 범위 지정된 된 값 보다 작습니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
## <a name="arguments"></a>인수  
 *거리*  
 한 **float** 거리를 지정 하는 식의 **기 하 도형** 인스턴스와의 버퍼를 계산할 합니다.  
  
 *허용 오차*  
 이 **float** 버퍼 거리의 허용 오차를 지정 하는 식입니다.  
  
 *허용 오차* 은 반환된 된 선형 근사값에 대 한 이상적인 버퍼 거리의 최대 편차를 나타냅니다.  
  
 예를 들어 요소의 이상적인 버퍼 거리는 원이지만 이는 다각형으로 대략 나타내야 합니다. 허용 오차가 작을수록 다각형의 점 개수가 늘어나 결과가 더 복잡해지지만 오류는 줄어듭니다.  
  
 *상대*  
 **비트** 지정 여부는 *허용 오차* 상대 또는 절대 값이 합니다. 경우 '값은 TRUE' 또는 1 인 다음 허용 오차는 상대적 이며의 곱으로 계산 되는 *허용 오차* 매개 변수와 인스턴스 경계 상자 지름의 합니다. 'FALSE' 또는 0 허용 오차는 절대적 하는 경우 및 *허용 오차* 값은 반환된 된 선형 근사값에 대 한 이상적인 버퍼 거리의 최대 절대 편차입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="exceptions"></a>예외  
 *허용 오차* 매개 변수는 0 보다 커야 합니다. 경우 *허용 오차* < = 0는 `System.ArgumentOutOfRangeException` throw 됩니다.  
  
> [!NOTE]  
>  이후 *허용 오차* 은 **float** 종류는 `System.Runtime.InteropServices.COMException` 부동 소수점 형식으로 반올림 문제로 인해 허용 오차로 지정 값은 매우 작은 경우에 throw 될 수 있습니다.  
  
## <a name="remarks"></a>주의  
 때 *거리* > 0 이면 한 **다각형** 또는 **MultiPolygon** 인스턴스가 반환 됩니다.  
  
> [!NOTE]  
>  거리 이므로 **float**, 매우 작은 값 0으로 계산 될 수 있습니다. 이 경우 호출의 복사본이 **geometry** 인스턴스가 반환 됩니다. 참조 [float 및 real &#40; Transact SQL &#41; ](../../t-sql/data-types/float-and-real-transact-sql.md).  
  
 때 *거리* = 0 호출의 복사본 **geometry** 인스턴스가 반환 됩니다.  
  
 때 *거리* < 0 다음  
  
-   빈 **GeometryCollection** 인스턴스의 차원이 0 또는 1은 인스턴스가 반환 됩니다.  
  
-   인스턴스의 차원이 2 이상이면 음수 버퍼가 반환됩니다.  
  
    > [!NOTE]  
    >  버퍼가 음수 이면 빈 만들 수도 **GeometryCollection** 인스턴스.  
  
 버퍼가 음수 이면의 경계에서 지정 된 거리 내 모든 요소가 제거 된 **geometry** 인스턴스.  
  
 이론적 버퍼와 계산 된 버퍼 간의 오차는 최대 (허용 오차, 익스텐트 \* 1.E-7) 허용 오차는의 값은 *허용 오차* 매개 변수입니다. 익스텐트에 대 한 자세한 내용은 참조 하십시오. [geometry 데이터 형식 메서드 참조](http://msdn.microsoft.com/library/d88e632b-6b2f-4466-a15f-9fbef1a347a7)합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Point` 인스턴스를 만들고 `BufferWithTolerance()`를 사용하여 인스턴스 주위의 대략적인 버퍼를 구합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(3 3)', 0);  
SELECT @g.BufferWithTolerance(1, .5, 0).ToString();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Stbuffer&#40; geometry 데이터 형식 &#41;](../../t-sql/spatial-geometry/stbuffer-geometry-data-type.md)   
 [Geometry 인스턴스의 확장된 메서드](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  


