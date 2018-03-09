---
title: "STBuffer (geometry 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STBuffer (geometry Data Type)
- STBuffer_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STBuffer (geometry Data Type)
ms.assetid: ca6bf2dc-1d38-4503-b87e-f2ea033d36ba
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ff65df2a1216a29b15a0458e9e4537c748140714
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="stbuffer-geometry-data-type"></a>STBuffer(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

모든의 합집합을 나타내는 기하학적 개체를 가리키는 인스턴스와의 거리가 반환은 **geometry** 인스턴스는 지정된 된 값 보다 작습니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STBuffer ( distance )  
```  
  
## <a name="arguments"></a>인수  
 *distance*  
 형식의 값은 **float** (**double** .NET framework에서)를 버퍼를 계산할 geometry 인스턴스와의 거리를 지정 하 합니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>주의  
 `STBuffer()`버퍼를 계산 [BufferWithTolerance](../../t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type.md)로 지정 하 여 *허용 오차* = 거리 \* .001 및 *상대*  =   **false**합니다.  
  
 때 *거리* > 0 이면 한 **다각형** 또는 **MultiPolygon** 인스턴스가 반환 됩니다.  
  
> [!NOTE]  
>  거리 이므로 **float**, 매우 작은 값을 0으로 계산 될 수 있습니다.  이 경우 호출의 복사본이 **geometry** 인스턴스가 반환 됩니다.  참조 [float 및 real &#40; Transact SQL &#41;](../../t-sql/data-types/float-and-real-transact-sql.md)  
  
 때 *거리* = 0 이면 호출의 복사본 **geometry** 인스턴스가 반환 됩니다.  
  
 때 *거리* < 0 인  
  
-   빈 **GeometryCollection** 인스턴스의 차원이 0 또는 1은 인스턴스가 반환 됩니다.  
  
-   인스턴스의 차원이 2 이상이면 음수 버퍼가 반환됩니다.  
  
    > [!NOTE]  
    >  버퍼가 음수 이면 빈 만들 수도 **GeometryCollection** 인스턴스.  
  
 버퍼가 음수이면 geometry 경계에서 지정된 거리 내에 있는 모든 요소가 제거됩니다.  
  
 이론적 버퍼와 계산 된 버퍼 간의 오차는 max (허용 오차, 익스텐트 * 1.E-7) 여기서 허용 오차 = 거리 \* .001 합니다. 익스텐트에 대 한 자세한 내용은 참조 하십시오. [geometry 데이터 형식 메서드 참조](http://msdn.microsoft.com/library/d88e632b-6b2f-4466-a15f-9fbef1a347a7)합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-calling-stbuffer-with-parametervalue--0-on-one-dimensional-geometry-instance"></a>1. 1차원 geometry 인스턴스에서 parameter_value < 0을 사용하여 STBuffer() 호출  
 다음 예에서는 빈 `GeometryCollection` 인스턴스를 반환합니다.  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer(-1).ToString();
 ```  
  
### <a name="b-calling-stbuffer-with-parametervalue--0-on-a-polygon-instance"></a>2. Polygon 인스턴스에서 parameter_value < 0을 사용하여 STBuffer() 호출  
 다음 예에서는 버퍼가 음수인 `Polygon` 인스턴스를 반환합니다.  
  
```
 DECLARE @g geometry = 'POLYGON((1 1, 1 5, 5 5, 5 1, 1 1))'; 
 SELECT @g.STBuffer(-1).ToString();
 ```  
  
### <a name="c-calling-stbuffer-with-parametervalue--0-on-a-curvepolygon-instance"></a>3. CurvePolygon 인스턴스에서 parameter_value < 0을 사용하여 STBuffer() 호출  
 다음 예에서는 `Polygon` 인스턴스에서 버퍼가 음수인 `CurvePolygon` 인스턴스를 반환합니다.  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.STBuffer(-1).ToString();
 ```  
  
> [!NOTE]  
>  `Polygon` 인스턴스는 `CurvePolygon` 인스턴스 대신 반환됩니다.  반환 하는 `CurvePolygon` 인스턴스를 참조 [BufferWithCurves &#40; geometry 데이터 형식 &#41;](../../t-sql/spatial-geometry/bufferwithcurves-geometry-data-type.md)  
  
### <a name="d-calling-stbuffer-with-a-negative-parameter-value-that-returns-an-empty-instance"></a>4. 빈 인스턴스를 반환하는 음수 매개 변수 값을 사용하여 STBuffer() 호출  
 다음 예제에서는 발생 하는 상황 때는 *거리* 매개 변수가-2 인 앞의 예제입니다.  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.STBuffer(-2).ToString();
 ```  
  
 이 **선택** 문에서 반환 된`GEOMETRYCOLLECTION EMPTY.`  
  
### <a name="e-calling-stbuffer-with-parametervalue--0"></a>5. parameter_value = 0을 사용하여 STBuffer() 호출  
 다음 예에서는 호출 `geometry` 인스턴스의 복사본을 반환합니다.  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer(0).ToString();
 ```  
  
### <a name="f-calling-stbuffer-with-a-non-zero-parameter-value-that-is-extremely-small"></a>6. 0이 아닌 매우 작은 매개 변수 값을 사용하여 STBuffer() 호출  
 다음 예에서도 호출 `geometry` 인스턴스의 복사본을 반환합니다.  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)';  
 DECLARE @distance float = 1e-20;  
 SELECT @g.STBuffer(@distance).ToString();
 ```  
  
### <a name="g-calling-stbuffer-with-parametervalue--0"></a>7. parameter_value > 0을 사용하여 STBuffer() 호출  
 다음 예에서는 `Polygon` 인스턴스를 반환합니다.  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer(2).ToString();
 ```  
  
### <a name="h-calling-stbuffer-with-a-string-parameter-value"></a>8. 문자열 매개 변수 값을 사용하여 STBuffer() 호출  
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
  
### <a name="i-calling-stbuffer-on-a-multipoint-instance"></a>9. MultiPoint 인스턴스에서 STBuffer() 호출  
 다음 예에서는 `MultiPolygon` 인스턴스 2개와 `Polygon` 인스턴스 1개를 반환합니다.  
  
```
 DECLARE @g geometry = 'MULTIPOINT((1 1),(1 4))'; 
 SELECT @g.STBuffer(1).ToString(); 
 SELECT @g.STBuffer(1.5).ToString(); 
 SELECT @g.STBuffer(1.6).ToString();
 ```  
  
 처음 두 **선택** 문은 반환는 `MultiPolygon` 않았기 때문에 인스턴스에 매개 변수 *거리* 보다 작거나 1/2 둘 사이의 거리 요소 (1 1) 및 (1 4). 세 번째 **선택** 문에서 반환은 `Polygon` 두의 버퍼링 된 인스턴스가 요소 (1 1) 때문에 인스턴스 (1 4) 및 중첩 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Bufferwithtolerance&#40; geometry 데이터 형식 &#41;](../../t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type.md)   
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

