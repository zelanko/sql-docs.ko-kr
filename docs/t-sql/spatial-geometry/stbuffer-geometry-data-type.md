---
title: STBuffer(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STBuffer (geometry Data Type)
- STBuffer_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STBuffer (geometry Data Type)
ms.assetid: ca6bf2dc-1d38-4503-b87e-f2ea033d36ba
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 01d7b5277e0711f5297e00d7b08b12e105b7f78b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930362"
---
# <a name="stbuffer-geometry-data-type"></a>STBuffer(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**geometry** 인스턴스와의 거리가 지정된 값보다 작거나 같은 모든 요소의 합집합을 나타내는 기하학적 개체를 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STBuffer ( distance )  
```  
  
## <a name="arguments"></a>인수  
 *distance*  
 해당 버퍼를 계산할 geometry 인스턴스와의 거리를 지정하는 **float**(.NET Framework의 경우 **double**) 형식의 값입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geometry**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 `STBuffer()`는 *허용 오차* = distance\*.001 및 *relative* = **false**로 지정하여 [BufferWithTolerance](../../t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type.md)와 동일한 방식으로 버퍼를 계산합니다.  
  
 *distance* > 0이면, **Polygon** 또는 **MultiPolygon** 인스턴스가 반환됩니다.  
  
> [!NOTE]  
>  거리가 **float**이므로 매우 작은 값은 0으로 계산될 수 있습니다.  이 경우 호출 **geometry** 인스턴스의 복사본이 반환됩니다.  [float 및 real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md) 참조  
  
 *distance* = 0이면, 호출 **geometry** 인스턴스의 복사본이 반환됩니다.  
  
 *distance* < 0이면,  
  
-   인스턴스의 차원이 0 또는 1이면 빈 **GeometryCollection** 인스턴스가 반환됩니다.  
  
-   인스턴스의 차원이 2 이상이면 음수 버퍼가 반환됩니다.  
  
    > [!NOTE]  
    >  버퍼가 음수이면 빈 **GeometryCollection** 인스턴스가 생성될 수도 있습니다.  
  
 버퍼가 음수이면 geometry 경계에서 지정된 거리 내에 있는 모든 요소가 제거됩니다.  
  
 이론적 버퍼와 계산된 버퍼 간의 오차는 허용 오차 = 거리 \* .001인 max(허용 오차, 익스텐트 * 1.E-7)입니다. 익스텐트에 대한 자세한 내용은 [geometry 데이터 형식 메서드 참조](https://msdn.microsoft.com/library/d88e632b-6b2f-4466-a15f-9fbef1a347a7)를 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-calling-stbuffer-with-parametervalue--0-on-one-dimensional-geometry-instance"></a>1\. 1차원 geometry 인스턴스에서 parameter_value < 0을 사용하여 STBuffer() 호출  
 다음 예에서는 빈 `GeometryCollection` 인스턴스를 반환합니다.  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer(-1).ToString();
 ```  
  
### <a name="b-calling-stbuffer-with-parametervalue--0-on-a-polygon-instance"></a>2\. Polygon 인스턴스에서 parameter_value < 0을 사용하여 STBuffer() 호출  
 다음 예에서는 버퍼가 음수인 `Polygon` 인스턴스를 반환합니다.  
  
```
 DECLARE @g geometry = 'POLYGON((1 1, 1 5, 5 5, 5 1, 1 1))'; 
 SELECT @g.STBuffer(-1).ToString();
 ```  
  
### <a name="c-calling-stbuffer-with-parametervalue--0-on-a-curvepolygon-instance"></a>C. CurvePolygon 인스턴스에서 parameter_value < 0을 사용하여 STBuffer() 호출  
 다음 예에서는 `Polygon` 인스턴스에서 버퍼가 음수인 `CurvePolygon` 인스턴스를 반환합니다.  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.STBuffer(-1).ToString();
 ```  
  
> [!NOTE]  
>  `Polygon` 인스턴스는 `CurvePolygon` 인스턴스 대신 반환됩니다.  `CurvePolygon` 인스턴스를 반환하려면 [BufferWithCurves &#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/bufferwithcurves-geometry-data-type.md)을 참조하세요.  
  
### <a name="d-calling-stbuffer-with-a-negative-parameter-value-that-returns-an-empty-instance"></a>D. 빈 인스턴스를 반환하는 음수 매개 변수 값을 사용하여 STBuffer() 호출  
 다음 예제에서는 이전 예제에서 *distance* 매개 변수가 -2인 경우에 발생하는 결과를 보여 줍니다.  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.STBuffer(-2).ToString();
 ```  
  
 이 **SELECT** 문은 `GEOMETRYCOLLECTION EMPTY.`를 반환합니다.  
  
### <a name="e-calling-stbuffer-with-parametervalue--0"></a>E. parameter_value = 0을 사용하여 STBuffer() 호출  
 다음 예에서는 호출 `geometry` 인스턴스의 복사본을 반환합니다.  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer(0).ToString();
 ```  
  
### <a name="f-calling-stbuffer-with-a-non-zero-parameter-value-that-is-extremely-small"></a>F. 0이 아닌 매우 작은 매개 변수 값을 사용하여 STBuffer() 호출  
 다음 예에서도 호출 `geometry` 인스턴스의 복사본을 반환합니다.  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)';  
 DECLARE @distance float = 1e-20;  
 SELECT @g.STBuffer(@distance).ToString();
 ```  
  
### <a name="g-calling-stbuffer-with-parametervalue--0"></a>G. parameter_value > 0을 사용하여 STBuffer() 호출  
 다음 예에서는 `Polygon` 인스턴스를 반환합니다.  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer(2).ToString();
 ```  
  
### <a name="h-calling-stbuffer-with-a-string-parameter-value"></a>H. 문자열 매개 변수 값을 사용하여 STBuffer() 호출  
 다음 예에서는 앞에서 설명한 것과 동일하지만 문자열 매개 변수가 메서드에 전달되는 `Polygon` 인스턴스를 반환합니다.  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer('2').ToString();
 ```  
  
 다음 예에서는 오류가 발생합니다.  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer('a').ToString();
 ```  
  
> [!NOTE]  
>  위의 두 예에서 `STBuffer()`에 문자열 리터럴을 전달한 경우.  첫 번째 예는 문자열 리터럴을 숫자 값으로 변환할 수 있으므로 정상적으로 작동하지만, 두 번째 예에서는 `ArgumentException`이 발생합니다.  
  
### <a name="i-calling-stbuffer-on-a-multipoint-instance"></a>9\. MultiPoint 인스턴스에서 STBuffer() 호출  
 다음 예에서는 `MultiPolygon` 인스턴스 2개와 `Polygon` 인스턴스 1개를 반환합니다.  
  
```
 DECLARE @g geometry = 'MULTIPOINT((1 1),(1 4))'; 
 SELECT @g.STBuffer(1).ToString(); 
 SELECT @g.STBuffer(1.5).ToString(); 
 SELECT @g.STBuffer(1.6).ToString();
 ```  
  
 처음 두 **SELECT** 문은 매개 변수 *distance*가 두 요소(1 1)과(1 4) 사이 거리의 1/2보다 작거나 같기 때문에 `MultiPolygon` 인스턴스를 반환합니다. 세 번째 **SELECT** 문은 두 요소(1 1)과(1 4)의 버퍼링된 인스턴스가 겹치기 때문에 `Polygon` 인스턴스를 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [BufferWithTolerance &#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type.md)   
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

