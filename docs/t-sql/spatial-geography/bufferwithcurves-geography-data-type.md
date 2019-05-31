---
title: BufferWithCurves(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BufferWithCurves
- BufferWithCurves_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- BufferWithCurves method (geography)
ms.assetid: abf0a11c-c99c-4faa-bf80-3ae8e04d7bfb
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 81222e73df527d5d51a592dd2cabe62384b5f936
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65937321"
---
# <a name="bufferwithcurves-geography-data-type"></a>BufferWithCurves(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  호출하는 **geography** 인스턴스와의 거리가 *distance* 매개 변수보다 작거나 같은 모든 점의 집합을 나타내는 **geography** 인스턴스를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.BufferWithCurves ( distance )  
```  
  
## <a name="arguments"></a>인수  
 *distance*  
 버퍼를 구성하는 점과 geography 인스턴스 사이에 허용되는 최대 거리를 나타내는 **float**입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="exceptions"></a>예외  
 다음 조건에서 **ArgumentException**이 발생합니다.  
  
-   메서드에 매개 변수가 전달되지 않는 경우(예: `@g.BufferWithCurves()`)  
  
-   숫자가 아닌 매개 변수가 메서드에 전달되는 경우(예: `@g.BufferWithCurves('a')`)  
  
-   **NULL**이 `@g.BufferWithCurves(NULL)`과 같은 메서드로 전달됩니다  
  
## <a name="remarks"></a>Remarks  
 다음 표에서는 여러 거리 값에 대해 반환되는 결과를 보여 줍니다.  
  
|거리 값|유형 차원|반환되는 공간 유형|  
|--------------------|---------------------|---------------------------|  
|거리 < 0|0 또는 1|빈 **GeometryCollection** 인스턴스|  
|거리 \< 0|2 이상|음수 버퍼가 있는 **CurvePolygon** 또는 **GeometryCollection** 인스턴스입니다.<br /><br /> 참고: 버퍼가 음수이면 빈 **GeometryCollection** 인스턴스가 생성될 수도 있습니다.|
|거리 = 0|모든 차원|호출하는 **geography** 인스턴스의 복사본|  
|distance > 0|모든 차원|**CurvePolygon** 또는 **GeometryCollection** 인스턴스|  
  
> [!NOTE]  
>  *거리*가 **float**이므로 매우 작은 값은 0으로 계산될 수 있습니다.  이 경우 호출 **geography** 인스턴스의 복사본이 반환됩니다.  
  
 **string** 매개 변수가 메서드에 전달되면 **float**로 변환되거나 `ArgumentException`가 발생합니다.  
  
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
  
### <a name="c-calling-bufferwithcurves-with-a-parameter-value--0-that-returns-an-empty-geometrycollection"></a>C. 빈 GeometryCollection을 반환하고 매개 변수 값 < 0인 BufferWithCurves() 호출  
 다음 예에서는 *distance* 매개 변수가 -2와 같을 때 생기는 결과를 보여 줍니다.  
  
 ```sql
 DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.BufferWithCurves(-2).ToString();
 ```  
  
 이 **SELECT** 문은 `GEOMETRYCOLLECTION EMPTY`를 반환합니다.  
  
### <a name="d-calling-bufferwithcurves-with-a-parameter-value--0"></a>D. 매개 변수 값 = 0인 BufferWithCurves() 호출  
 다음 예에서는 호출 **geography** 인스턴스의 복사본을 반환합니다.  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(0).ToString();
 ```  
  
### <a name="e-calling-bufferwithcurves-with-a-non-zero-parameter-value-that-is-extremely-small"></a>E. 매우 작고 0이 아닌 매개 변수 값으로 BufferWithCurves() 호출  
 다음 예에서도 호출 **geography** 인스턴스의 복사본을 반환합니다.  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 DECLARE @distance float = 1e-20;  
 SELECT @g.BufferWithCurves(@distance).ToString();
 ```  
  
### <a name="f-calling-bufferwithcurves-with-a-parameter-value--0"></a>F. 매개 변수 값 > 0인 BufferWithCurves() 호출  
 다음 예에서는 `CurvePolygon` 인스턴스를 반환합니다.  

 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(2).ToString();
 ```  
### <a name="g-passing-a-valid-string-parameter"></a>G. 올바른 문자열 매개 변수 전달  
 다음 예에서는 앞에서 설명한 것과 동일하지만 문자열 매개 변수가 메서드에 전달되는 `CurvePolygon` 인스턴스를 반환합니다.  

 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves('2').ToString();
```  
  
### <a name="h-passing-an-invalid-string-parameter"></a>H. 잘못된 문자열 매개 변수 전달  
 다음 예에서는 오류가 발생합니다.  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)'  
 SELECT @g.BufferWithCurves('a').ToString();
 ```  
  
 위의 두 예에서는 문자열 리터럴이 `BufferWithCurves()` 메서드에 전달됩니다. 첫 번째 예는 문자열 리터럴을 숫자 값으로 변환할 수 있으므로 정상적으로 작동하지만, 두 번째 예에서는 `ArgumentException`이 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [BufferWithCurves &#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/bufferwithcurves-geometry-data-type.md)  
  
  
