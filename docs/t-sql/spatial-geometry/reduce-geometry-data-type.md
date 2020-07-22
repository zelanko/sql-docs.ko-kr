---
title: Reduce(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Reduce_TSQL
- Reduce
dev_langs:
- TSQL
helpviewer_keywords:
- Reduce method
ms.assetid: 132184bf-c4d2-4a27-900d-8373445dce2a
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 16ac1ced9d2bfbfa8de4b2c8cc577aeb83d15be0
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554705"
---
# <a name="reduce-geometry-data-type"></a>Reduce(geometry 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

지정된 **기하 도형** 인스턴스의 근사값을 반환합니다. 근사값은 지정된 허용 오차를 가진 인스턴스에서 Douglas-Peucker 알고리즘 확장을 실행하여 생성됩니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.Reduce ( tolerance )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *tolerance*  
 **float** 형식의 값입니다. *tolerance*는 근사값 알고리즘에 입력할 허용 오차입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geometry**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>설명  
 컬렉션 형식의 경우 이 알고리즘은 인스턴스에 포함된 각 **geometry**에 대해 독립적으로 작동합니다.  
  
 이 알고리즘은 **Point** 인스턴스를 수정하지 않습니다.  
  
 **LineString**, **CircularString** 및 **CompoundCurve** 인스턴스에서 근사값 알고리즘은 인스턴스의 원래 시작점과 엔드포인트를 유지합니다. 알고리즘은 다음에 반복적으로 결과에서 가장 벗어나는 원래 인스턴스의 포인트를 추가합니다. 이 프로세스는 지정된 허용 오차를 벗어나는 포인트가 없을 때까지 계속됩니다.  
  
 `Reduce()`은 **CircularString** 인스턴스에 대해 **LineString**, **CircularString** 또는 **CompoundCurve** 인스턴스를 반환합니다.  `Reduce()`은 **CompoundCurve** 인스턴스에 대해 **CompoundCurve** 또는 **LineString** 인스턴스를 반환합니다.  
  
 **Polygon** 인스턴스에서 근사값 알고리즘은 각 링에 독립적으로 적용됩니다. 이 메서드는 반환된 **Polygon** 인스턴스가 잘못된 경우 `FormatException`을 생성합니다. 예를 들어 `Reduce()`를 적용하여 인스턴스의 각 링을 단순화한 결과로 생성된 링이 겹치는 경우 잘못된 **MultiPolygon** 인스턴스가 생성됩니다.  내부 링이 없고 외부 링이 있는 **CurvePolygon** 인스턴스에서 `Reduce()`는 **CurvePolygon**, **LineString** 또는 **Point** 인스턴스를 반환합니다.  **CurvePolygon**에 내부 링이 있으면, **CurvePolygon** 또는 **MultiPoint** 인스턴스가 반환됩니다.  
  
 원호 세그먼트가 발견되면 근사값 알고리즘이 지정된 허용 오차 절반 이내에서 해당 현으로 어림할 수 있는지 여부를 확인합니다. 이 조건을 충족하는 현은 계산에서 원호가 현으로 바뀝니다. 현이 이 조건을 충족하지 못하면 원호가 유지되고 근사값 알고리즘이 나머지 세그먼트에 적용됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-reduce-to-simplify-a-linestring"></a>A. Reduce()를 사용하여 LineString 단순화  
 다음 예에서는 `LineString` 인스턴스를 만들고 `Reduce()`를 사용하여 인스턴스를 단순화합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 0 1, 1 0, 2 1, 3 0, 4 1)', 0);  
SELECT @g.Reduce(.75).ToString();  
```  
  
### <a name="b-using-reduce-with-varying-tolerance-levels-on-a-circularstring"></a>B. CircularString에서 다양한 허용 오차 수준과 함께 Reduce() 사용  
 다음 예제에서는 **CircularString** 인스턴스에서 세 가지 허용 오차 수준과 함께 `Reduce()`를 사용합니다.  
  
```
 DECLARE @g geometry = 'CIRCULARSTRING(0 0, 8 8, 16 0, 20 -4, 24 0)'; 
 SELECT @g.Reduce(5).ToString(); 
 SELECT @g.Reduce(15).ToString(); 
 SELECT @g.Reduce(16).ToString();
 ```  
  
 이 예에서 생성되는 출력은 다음과 같습니다.  
  
 ```
 CIRCULARSTRING (0 0, 8 8, 16 0, 20 -4, 24 0) 
 COMPOUNDCURVE (CIRCULARSTRING (0 0, 8 8, 16 0), (16 0, 24 0)) 
 LINESTRING (0 0, 24 0)
 ```  
  
 반환된 각 인스턴스는 엔드포인트 (0 0) 및 (24 0)을 포함합니다.  
  
### <a name="c-using-reduce-with-varying-tolerance-levels-on-a-compoundcurve"></a>C. CompoundCurve에서 다양한 허용 오차 수준과 함께 Reduce() 사용  
 다음 예제에서는 **CompoundCurve** 인스턴스에서 두 가지 허용 오차 수준과 함께 `Reduce()`를 사용합니다.  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE(CIRCULARSTRING(0 0, 8 8, 16 0, 20 -4, 24 0),(24 0, 20 4, 16 0))';  
 SELECT @g.Reduce(15).ToString();  
 SELECT @g.Reduce(16).ToString();
 ```  
  
 이 예제에서는 두 번째 **SELECT** 문이 **LineString** 인스턴스를 반환합니다: `LineString(0 0, 16 0)`.  
  
### <a name="showing-an-example-where-the-original-start-and-end-points-are-lost"></a>원래의 시작점과 끝점이 사라진 예 보기  
 다음 예에서는 결과 인스턴스에서 원래의 시작점과 엔드포인트가 유지되지 않을 수도 있는 경우를 보여줍니다. 원래 시작점과 엔드포인트를 유지하면 잘못된 **LineString** 인스턴스가 생성되기 때문에 이 동작이 발생합니다.  
  
```  
DECLARE @g geometry = 'LINESTRING(0 0, 4 0, 2 .01, 1 0)';  
DECLARE @h geometry = @g.Reduce(1);  
SELECT @g.STIsValid() AS Valid  
SELECT @g.ToString() AS Original, @h.ToString() AS Reduced;  
```  
  
## <a name="see-also"></a>참고 항목  
 [확장 정적 기하 도형 메서드](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
