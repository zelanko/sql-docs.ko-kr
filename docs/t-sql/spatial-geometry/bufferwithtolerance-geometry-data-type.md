---
title: BufferWithTolerance(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 941eb7f9cdf39475631b8ab45789cd2082ad3084
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="bufferwithtolerance-geometry-data-type"></a>BufferWithTolerance(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

지정된 허용 오차를 고려하여 **geometry** 인스턴스와의 거리가 지정된 값보다 작거나 같은 모든 점 값의 합집합을 나타내는 기하학적 개체를 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
## <a name="arguments"></a>인수  
 *distance*  
 해당 버퍼를 계산할 **geometry** 인스턴스와의 거리를 지정하는 **float** 식입니다.  
  
 *tolerance*  
 버퍼 거리에 대한 허용 오차를 지정하는 **float** 식입니다.  
  
 *Tolerance*는 반환된 선형 근사값에 대한 이상적인 버퍼 거리의 최대 편차를 나타냅니다.  
  
 예를 들어 요소의 이상적인 버퍼 거리는 원이지만 이는 다각형으로 대략 나타내야 합니다. 허용 오차가 작을수록 다각형의 점 개수가 늘어나 결과가 더 복잡해지지만 오류는 줄어듭니다.  
  
 *relative*  
 *tolerance* 값이 상대적인지, 아니면 절대적인지를 지정하는 **비트**입니다. 'TRUE' 또는 1인 경우 *tolerance*는 상대적이며 허용 오차 매개 변수와 인스턴스 경계 상자 지름의 곱으로 계산됩니다. 'FALSE' 또는 0인 경우 허용 오차는 절대적이며 *tolerance* 값은 반환된 선형 근사값에 대한 이상적인 버퍼 거리의 최대 절대 편차입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geometry**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="exceptions"></a>예외  
 *tolerance* 매개 변수는 0보다 커야 합니다. *tolerance* <= 0일 경우 `System.ArgumentOutOfRangeException`이 throw됩니다.  
  
> [!NOTE]  
>  *tolerance*가 **float** 형식이므로 부동 소수점 형식의 반올림 문제로 인해 허용 오차로 지정된 값이 매우 작을 경우 `System.Runtime.InteropServices.COMException`이 발생할 수 있습니다.  
  
## <a name="remarks"></a>Remarks  
 *distance* > 0이면, **Polygon** 또는 **MultiPolygon** 인스턴스가 반환됩니다.  
  
> [!NOTE]  
>  거리가 **float**이므로 계산에서 매우 작은 값은 0과 같습니다. 이 경우 호출 **geometry** 인스턴스의 복사본이 반환됩니다. [float 및 real&#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md)을 참조하세요.  
  
 *distance* = 0이면, 호출 **geometry** 인스턴스의 복사본이 반환됩니다.  
  
 *distance* < 0이면  
  
-   인스턴스의 차원이 0 또는 1이면 빈 **GeometryCollection** 인스턴스가 반환됩니다.  
  
-   인스턴스의 차원이 2 이상이면 음수 버퍼가 반환됩니다.  
  
    > [!NOTE]  
    >  버퍼가 음수이면 빈 **GeometryCollection** 인스턴스가 생성될 수도 있습니다.  
  
 버퍼가 음수이면 **geometry** 인스턴스 경계에서 지정된 거리 내에 있는 모든 요소가 제거됩니다.  
  
 이론 버퍼와 계산된 버퍼 간의 오류는 최대입니다(허용 오차, 익스텐트 \* 1.E-7). 여기서 허용 오차는 *tolerance* 매개 변수의 값입니다. 익스텐트에 대한 자세한 내용은 [geometry 데이터 형식 메서드 참조](http://msdn.microsoft.com/library/d88e632b-6b2f-4466-a15f-9fbef1a347a7)를 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Point` 인스턴스를 만들고 `BufferWithTolerance()`를 사용하여 인스턴스 주위의 대략적인 버퍼를 구합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(3 3)', 0);  
SELECT @g.BufferWithTolerance(1, .5, 0).ToString();  
```  
  
## <a name="see-also"></a>참고 항목  
 [STBuffer&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stbuffer-geometry-data-type.md)   
 [geometry 인스턴스의 확장 메서드](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

