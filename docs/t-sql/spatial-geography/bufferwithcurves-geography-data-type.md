---
title: "BufferWithCurves (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BufferWithCurves
- BufferWithCurves_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- BufferWithCurves method (geography)
ms.assetid: abf0a11c-c99c-4faa-bf80-3ae8e04d7bfb
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 80f16777999a029e1063305a0d1b8501af7e05d7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="bufferwithcurves-geography-data-type"></a>BufferWithCurves(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  반환은 **geography** 모든 세트를 나타내는 인스턴스 호출에서 거리가 가리키는 **geography** 인스턴스 보다 작거나 같음는 *거리* 매개 변수입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.BufferWithCurves ( distance )  
```  
  
## <a name="arguments"></a>인수  
 *거리*  
 이 **float** 버퍼 점과 되는 최대 거리를 나타내는 geography 인스턴스에서 수 있습니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="exceptions"></a>예외  
 다음 조건을 발생 시킵니다는 **ArgumentException**합니다.  
  
-   메서드에 매개 변수가 전달되지 않는 경우(예: `@g.BufferWithCurves()`)  
  
-   숫자가 아닌 매개 변수가 메서드에 전달되는 경우(예: `@g.BufferWithCurves('a')`)  
  
-   **NULL** 등 메서드로 전달 됩니다`@g.BufferWithCurves(NULL)`  
  
## <a name="remarks"></a>주의  
 다음 표에서는 여러 거리 값에 대해 반환되는 결과를 보여 줍니다.  
  
|거리 값|유형 차원|반환되는 공간 유형|  
|--------------------|---------------------|---------------------------|  
|거리 < 0|0 또는 1|빈 **GeometryCollection** 인스턴스|  
|거리 \< 0|2 이상|A **CurvePolygon** 또는 **GeometryCollection** 음수 버퍼가 인스턴스.<br /><br /> 참고: 버퍼가 음수 이면 빈을 만들 수 있습니다 **GeometryCollection**|
|거리 = 0|모든 차원|호출의 복사본 **geography** 인스턴스|  
|거리 > 0|모든 차원|**CurvePolygon** 또는 **GeometryCollection** 인스턴스|  
  
> [!NOTE]  
>  이후 *거리* 는 **float**, 매우 작은 값을 0으로 계산 될 수 있습니다.  이 경우, 호출의 복사본 **geography** 인스턴스가 반환 됩니다.  
  
 경우는 **문자열** 매개 변수가 전달 메서드를 다음으로 변환 됩니다는 **float** 함수 이거나 throw 것는 `ArgumentException`합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-calling-bufferwithcurves-with-a-parameter-value--0-on-one-dimensional-geography-instance"></a>1. 1차원 geography 인스턴스에서 매개 변수 값 < 0인 BufferWithCurves() 호출  
 다음 예에서는 빈 `GeometryCollection` 인스턴스를 반환합니다.  
  
 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(-1).ToString();
``` 
  
### <a name="b-calling-bufferwithcurves-with-a-parameter-value--0-on-a-two-dimensional-geography-instance"></a>2. 2차원 geography 인스턴스에서 매개 변수 값 < 0인 BufferWithCurves() 호출  
 다음 예에서는 버퍼가 음수인 `CurvePolygon` 인스턴스를 반환합니다.  
  
 ```sql
 DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.BufferWithCurves(-1).ToString()
 ```  
  
### <a name="c-calling-bufferwithcurves-with-a-parameter-value--0-that-returns-an-empty-geometrycollection"></a>3. 빈 GeometryCollection을 반환하고 매개 변수 값 < 0인 BufferWithCurves() 호출  
 다음 예제에서는 어떤 일이 발생 하면는 *거리* 매개 변수가-2 인:  
  
 ```sql
 DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.BufferWithCurves(-2).ToString();
 ```  
  
 이 **선택** 문에서 반환`GEOMETRYCOLLECTION EMPTY`  
  
### <a name="d-calling-bufferwithcurves-with-a-parameter-value--0"></a>4. 매개 변수 값 = 0인 BufferWithCurves() 호출  
 다음 예제에서는 호출의 복사본을 반환 **geography** 인스턴스:  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(0).ToString();
 ```  
  
### <a name="e-calling-bufferwithcurves-with-a-non-zero-parameter-value-that-is-extremely-small"></a>5. 매우 작고 0이 아닌 매개 변수 값으로 BufferWithCurves() 호출  
 다음 예제에서는 또한 호출의 복사본을 반환 **geography** 인스턴스:  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 DECLARE @distance float = 1e-20;  
 SELECT @g.BufferWithCurves(@distance).ToString();
 ```  
  
### <a name="f-calling-bufferwithcurves-with-a-parameter-value--0"></a>6. 매개 변수 값 > 0인 BufferWithCurves() 호출  
 다음 예에서는 `CurvePolygon` 인스턴스를 반환합니다.  

 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(2).ToString();
 ```  
### <a name="g-passing-a-valid-string-parameter"></a>7. 올바른 문자열 매개 변수 전달  
 다음 예에서는 앞에서 설명한 것과 동일하지만 문자열 매개 변수가 메서드에 전달되는 `CurvePolygon` 인스턴스를 반환합니다.  

 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves('2').ToString();
```  
  
### <a name="h-passing-an-invalid-string-parameter"></a>8. 잘못된 문자열 매개 변수 전달  
 다음 예에서는 오류가 발생합니다.  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)'  
 SELECT @g.BufferWithCurves('a').ToString();
 ```  
  
 위의 두 예에서는 문자열 리터럴이 `BufferWithCurves()` 메서드에 전달됩니다. 첫 번째 예는 문자열 리터럴을 숫자 값으로 변환할 수 있으므로 정상적으로 작동하지만, 두 번째 예에서는 `ArgumentException`이 발생합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Geography 인스턴스의 확장된 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [BufferWithCurves &#40; geometry 데이터 형식 &#41;](../../t-sql/spatial-geometry/bufferwithcurves-geometry-data-type.md)  
  
  

