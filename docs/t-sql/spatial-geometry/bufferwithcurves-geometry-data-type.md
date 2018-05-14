---
title: BufferWithCurves(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- BufferWithCurves method (geometry)
ms.assetid: 8ffaba3f-d2dd-4e57-9f41-3ced9f14b600
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e08e1f4301f1fe4ba70db867f0a3f8c73ebf9209
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="bufferwithcurves-geometry-data-type"></a>BufferWithCurves(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  호출하는 **geometry** 인스턴스와의 거리가 *distance* 매개 변수보다 작거나 같은 모든 점의 집합을 나타내는 **geometry** 인스턴스를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.BufferWithCurves ( distance )  
```  
  
## <a name="arguments"></a>인수  
 *distance*  
 버퍼를 구성하는 점과 **geometry** 인스턴스 사이에 허용되는 최대 거리를 나타내는 **float**입니다.  
  
## <a name="return-types"></a>반환 형식  
SQL Server 반환 형식: **geometry**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="exceptions"></a>예외  
 다음 조건에서 **ArgumentException**이 발생합니다.  
  
-   메서드에 매개 변수가 전달되지 않는 경우(예: `@g.BufferWithCurves()`)  
  
-   숫자가 아닌 매개 변수가 메서드에 전달되는 경우(예: `@g.BufferWithCurves('a')`)  
  
-   **NULL**이 `@g.BufferWithCurves(NULL)`과 같은 메서드로 전달됩니다  
  
## <a name="remarks"></a>Remarks  
 다음 그림에서는 이 메서드가 반환하는 geometry 인스턴스의 예를 보여 줍니다.  
  
 ![BufferedCurve](../../t-sql/spatial-geometry/media/bufferedcurve.gif)
  
 다음 표에서는 여러 거리 값에 대해 반환되는 결과를 보여 줍니다.  
  
|거리 값|유형 차원|반환되는 공간 유형|  
|--------------------|---------------------|---------------------------|  
|거리 < 0|0 또는 1|빈 **GeometryCollection** 인스턴스|  
|거리 < 0|2 이상|음수 버퍼가 있는 **CurvePolygon** 또는 **GeometryCollection** 인스턴스입니다. **참고:** 버퍼가 음수이면 빈 **GeometryCollection** 인스턴스가 생성될 수도 있습니다.|  
|거리 = 0|모든 차원|호출하는 **geometry** 인스턴스의 복사본|  
|distance > 0|모든 차원|**CurvePolygon** 또는 **GeometryCollection** 인스턴스|  
  
> [!NOTE]  
>  *거리*가 **float**이므로 매우 작은 값은 0으로 계산될 수 있습니다. 이 경우 호출 **geometry** 인스턴스의 복사본이 반환됩니다. [float 및 real&#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md)을 참조하세요.  
  
 버퍼가 음수이면 기하 도형의 경계에서 지정된 거리 내에 있는 모든 요소가 제거됩니다. 다음 그림에서는 음수 버퍼를 원의 옅은 음영이 있는 영역으로 표시합니다. 점선은 원래 다각형의 경계이며 실선은 결과 다각형의 경계입니다.  
  
 **string** 매개 변수가 메서드에 전달되면 **float**로 변환되거나 `ArgumentException`가 발생합니다.  
  
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
 다음 예에서는 *distance* 매개 변수가 -2와 같을 때 생기는 결과를 보여 줍니다.  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.BufferWithCurves(-2).ToString();
 ```  
  
 이 **SELECT** 문은 `GEOMETRYCOLLECTION EMPTY`를 반환합니다.  
  
### <a name="d-calling-bufferwithcurves-with-a-parameter-value--0"></a>4. 매개 변수 값 = 0인 BufferWithCurves() 호출  
 다음 예에서는 호출 **geometry** 인스턴스의 복사본을 반환합니다.  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(0).ToString();
 ```  
  
### <a name="e-calling-bufferwithcurves-with-a-non-zero-parameter-value-that-is-extremely-small"></a>5. 매우 작고 0이 아닌 매개 변수 값으로 BufferWithCurves() 호출  
 다음 예에서도 호출 **geometry** 인스턴스의 복사본을 반환합니다.  
  
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
  
 처음 두 **SELECT** 문은 매개 변수 *distance*가 두 요소(1 1)과(1 4) 사이 거리의 1/2보다 작거나 같기 때문에 `GeometryCollection` 인스턴스를 반환합니다. 세 번째 **SELECT** 문은 두 요소(1 1)과(1 4)의 버퍼링된 인스턴스가 겹치기 때문에 `CurvePolygon` 인스턴스를 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [geometry 인스턴스의 확장 메서드](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
 
