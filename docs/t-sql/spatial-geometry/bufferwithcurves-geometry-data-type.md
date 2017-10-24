---
title: "BufferWithCurves (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- BufferWithCurves method (geometry)
ms.assetid: 8ffaba3f-d2dd-4e57-9f41-3ced9f14b600
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a88ea4010ec1cfd48661b34e990634fe371141f3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="bufferwithcurves-geometry-data-type"></a>BufferWithCurves(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  반환은 **기 하 도형** 모든 세트를 나타내는 인스턴스 호출에서 거리가 가리키는 **기 하 도형** 인스턴스 보다 작거나 같음는 *거리* 매개 변수입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.BufferWithCurves ( distance )  
```  
  
## <a name="arguments"></a>인수  
 *거리*  
 이 **float** 에서 수를 버퍼로 점과 되는 최대 거리를 나타내는 **기 하 도형** 인스턴스.  
  
## <a name="return-types"></a>반환 형식  
SQL Server 반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="exceptions"></a>예외  
 다음 조건을 발생 시킵니다는 **ArgumentException**합니다.  
  
-   메서드에 매개 변수가 전달되지 않는 경우(예: `@g.BufferWithCurves()`)  
  
-   숫자가 아닌 매개 변수가 메서드에 전달되는 경우(예: `@g.BufferWithCurves('a')`)  
  
-   **NULL** 등 메서드로 전달 됩니다`@g.BufferWithCurves(NULL)`  
  
## <a name="remarks"></a>주의  
 다음 그림에서는 이 메서드가 반환하는 geometry 인스턴스의 예를 보여 줍니다.  
  
 ![BufferedCurve](../../t-sql/spatial-geometry/media/bufferedcurve.gif)
  
 다음 표에서는 여러 거리 값에 대해 반환되는 결과를 보여 줍니다.  
  
|거리 값|유형 차원|반환되는 공간 유형|  
|--------------------|---------------------|---------------------------|  
|거리 < 0|0 또는 1|빈 **GeometryCollection** 인스턴스|  
|거리 < 0|2 이상|A **CurvePolygon** 또는 **GeometryCollection** 음수 버퍼가 인스턴스. **참고:** 버퍼가 음수 이면 빈을 만들 수 있습니다 **GeometryCollection**|  
|거리 = 0|모든 차원|호출의 복사본 **geometry** 인스턴스|  
|거리 > 0|모든 차원|**CurvePolygon** 또는 **GeometryCollection** 인스턴스|  
  
> [!NOTE]  
>  이후 *거리* 는 **float**, 매우 작은 값을 0으로 계산 될 수 있습니다. 이 경우 호출의 복사본 **geometry** 인스턴스가 반환 됩니다. 참조 [float 및 real &#40; Transact SQL &#41; ](../../t-sql/data-types/float-and-real-transact-sql.md).  
  
 버퍼가 음수이면 기하 도형의 경계에서 지정된 거리 내에 있는 모든 요소가 제거됩니다. 다음 그림에서는 음수 버퍼를 원의 옅은 음영이 있는 영역으로 표시합니다. 점선은 원래 다각형의 경계이며 실선은 결과 다각형의 경계입니다.  
  
 경우는 **문자열** 매개 변수가 전달 메서드를 다음으로 변환 됩니다는 **float** 함수 이거나 throw 것는 `ArgumentException`합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-calling-bufferwithcurves-with-a-parameter-value--0-on-one-dimensional-geometry-instance"></a>1. 1차원 geometry 인스턴스에서 매개 변수 값 < 0인 BufferWithCurves() 호출  
 다음 예에서는 빈 `GeometryCollection` 인스턴스를 반환합니다.  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(-1).ToString(); 
 ```
  
### <a name="b-calling-bufferwithcurves-with-a-parameter-value--0-on-a-two-dimensional-geometry-instance"></a>2. 2차원 geometry 인스턴스에서 매개 변수 값 < 0인 BufferWithCurves() 호출  
 다음 예에서는 버퍼가 음수인 `CurvePolygon` 인스턴스를 반환합니다.  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.BufferWithCurves(-1).ToString()
 ```  
  
### <a name="c-calling-bufferwithcurves-with-a-parameter-value--0-that-returns-an-empty-geometrycollection"></a>3. 빈 GeometryCollection을 반환하고 매개 변수 값 < 0인 BufferWithCurves() 호출  
 다음 예제에서는 어떤 일이 발생 하면는 *거리* 매개 변수가-2 인:  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.BufferWithCurves(-2).ToString();
 ```  
  
 이 **선택** 문에서 반환`GEOMETRYCOLLECTION EMPTY`  
  
### <a name="d-calling-bufferwithcurves-with-a-parameter-value--0"></a>4. 매개 변수 값 = 0인 BufferWithCurves() 호출  
 다음 예제에서는 호출의 복사본을 반환 **geometry** 인스턴스:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(0).ToString();
 ```  
  
### <a name="e-calling-bufferwithcurves-with-a-non-zero-parameter-value-that-is-extremely-small"></a>5. 매우 작고 0이 아닌 매개 변수 값으로 BufferWithCurves() 호출  
 다음 예제에서는 또한 호출의 복사본을 반환 **geometry** 인스턴스:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 DECLARE @distance float = 1e-20; 
 SELECT @g.BufferWithCurves(@distance).ToString();
 ```  
  
### <a name="f-calling-bufferwithcurves-with-a-parameter-value--0"></a>6. 매개 변수 값 > 0인 BufferWithCurves() 호출  
 다음 예에서는 `CurvePolygon` 인스턴스를 반환합니다.  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(2).ToString();
 ```  
  
### <a name="g-passing-a-valid-string-parameter"></a>7. 올바른 문자열 매개 변수 전달  
 다음 예에서는 앞에서 설명한 것과 동일하지만 문자열 매개 변수가 메서드에 전달되는 `CurvePolygon` 인스턴스를 반환합니다.  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves('2').ToString();
 ```  
  
### <a name="h-passing-an-invalid-string-parameter"></a>8. 잘못된 문자열 매개 변수 전달  
 다음 예에서는 오류가 발생합니다.  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)' 
 SELECT @g.BufferWithCurves('a').ToString();
 ```  
  
 위의 두 예에서는 문자열 리터럴이 `BufferWithCurves()` 메서드에 전달됩니다. 첫 번째 예는 문자열 리터럴을 숫자 값으로 변환할 수 있으므로 정상적으로 작동하지만, 두 번째 예에서는 `ArgumentException`이 발생합니다.  
  
### <a name="i-calling-bufferwithcurves-on-multipoint-instance"></a>9. MultiPoint 인스턴스에서 BufferWithCurves() 호출  
 다음 예에서는 `GeometryCollection` 인스턴스 2개와 `CurvePolygon` 인스턴스 1개를 반환합니다.  
  
```
 DECLARE @g geometry = 'MULTIPOINT((1 1),(1 4))'; 
 SELECT @g.BufferWithCurves(1).ToString(); 
 SELECT @g.BufferWithCurves(1.5).ToString(); 
 SELECT @g.BufferWithCurves(1.6).ToString();
 ```  
  
 처음 두 **선택** 문은 반환는 `GeometryCollection` 않았기 때문에 인스턴스에 매개 변수 *거리* 보다 작거나 1/2 둘 사이의 거리 요소 (1 1) 및 (1 4). 세 번째 **선택** 문에서 반환은 `CurvePolygon` 두의 버퍼링 된 인스턴스가 요소 (1 1) 때문에 인스턴스 (1 4) 및 중첩 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Geometry 인스턴스의 확장된 메서드](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
 

