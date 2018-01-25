---
title: "(Geometry 데이터 형식)를 줄이는 | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Reduce_TSQL
- Reduce
dev_langs: TSQL
helpviewer_keywords: Reduce method
ms.assetid: 132184bf-c4d2-4a27-900d-8373445dce2a
caps.latest.revision: "30"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fb6c4a66f3233620ef5d24506d41e7659fc3b82d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="reduce-geometry-data-type"></a>Reduce(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

한 근사값을 반환는 주어진 **geometry** 인스턴스 인스턴스에서 지정 된 허용 오차로 Douglas-peucker 알고리즘의 확장을 실행 하 여 생성 합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.Reduce ( tolerance )  
```  
  
## <a name="arguments"></a>인수  
 *tolerance*  
 형식의 값은 **float**합니다. *허용 오차* 는 근사값 알고리즘에 대 한 입력을 허용 오차입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **기 하 도형**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>주의  
 컬렉션 형식의 경우이 알고리즘 무관 하 게 작동 각 **geometry** 인스턴스에 포함 된 합니다.  
  
 이 알고리즘을 수정 하지 않는 **지점** 인스턴스.  
  
 **LineString**, **CircularString**, 및 **CompoundCurve** 인스턴스에서 근사값 알고리즘에는 원래 시작점과 끝점의 인스턴스를 유지 하 고 반복적으로 다시 추가 지점 대부분 편차가 큰 지점이 없을 때까지 결과에서 지정된 된 허용 오차 보다 편차가 큰 원래 인스턴스에서 합니다.  
  
 `Reduce()`반환 된 **LineString**, **CircularString**, 또는 **CompoundCurve** 인스턴스에 대 한 **CircularString** 인스턴스.  `Reduce()`중 하나를 반환 된 **CompoundCurve** 또는 **LineString** 인스턴스에 대해 **CompoundCurve** 인스턴스.  
  
 **다각형** 인스턴스에서 근사값 알고리즘은 각 링에 독립적으로 적용 됩니다. 메서드가 생성 됩니다는 `FormatException` 경우 반환 된 **다각형** 인스턴스가 유효 하지 않습니다; 예를 들어는 유효 하지 않은 **MultiPolygon** 경우 인스턴스가 생성 되 `Reduce()` 각 간소화 하기 위해 적용 인스턴스 및 결과로 생성 된 링 겹치는 링입니다.  **CurvePolygon** 외부 링과 내부 링은 없는 사용 하 여 인스턴스 `Reduce()` 반환는 **CurvePolygon**, **LineString**, 또는 **지점** 인스턴스.  경우는 **CurvePolygon** 내부 링이 있는 **CurvePolygon** 또는 **MultiPoint** 인스턴스가 반환 됩니다.  
  
 원호 세그먼트가 발견되면 근사값 알고리즘이 지정된 허용 오차 절반 이내에서 해당 현으로 어림할 수 있는지 여부를 확인합니다.  현이 이 조건에 맞으면 계산에서 원호가 현으로 바뀝니다. 현이 이 조건에 맞지 않으면 원호는 그대로 유지되며 근사값 알고리즘이 나머지 세그먼트에 적용됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-reduce-to-simplify-a-linestring"></a>1. Reduce()를 사용하여 LineString 단순화  
 다음 예에서는 `LineString` 인스턴스를 만들고 `Reduce()`를 사용하여 인스턴스를 단순화합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 0 1, 1 0, 2 1, 3 0, 4 1)', 0);  
SELECT @g.Reduce(.75).ToString();  
```  
  
### <a name="b-using-reduce-with-varying-tolerance-levels-on-a-circularstring"></a>2. CircularString에서 다양한 허용 오차 수준과 함께 Reduce() 사용  
 다음 예제에서는 `Reduce()` 세 가지 허용 오차 수준과 함께 **CircularString** 인스턴스:  
  
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
  
 반환된 각 인스턴스는 끝점 (0 0) 및 (24 0)을 포함합니다.  
  
### <a name="c-using-reduce-with-varying-tolerance-levels-on-a-compoundcurve"></a>3. CompoundCurve에서 다양한 허용 오차 수준과 함께 Reduce() 사용  
 다음 예제에서는 `Reduce()` 두 가지 허용 오차 수준과 함께 **CompoundCurve** 인스턴스:  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE(CIRCULARSTRING(0 0, 8 8, 16 0, 20 -4, 24 0),(24 0, 20 4, 16 0))';  
 SELECT @g.Reduce(15).ToString();  
 SELECT @g.Reduce(16).ToString();
 ```  
  
 이 예제에서 두 번째 **선택** 문에서 반환 된 **LineString** 인스턴스: `LineString(0 0, 16 0)`합니다.  
  
### <a name="showing-an-example-where-the-original-start-and-end-points-are-lost"></a>원래의 시작점과 끝점이 사라진 예 보기  
 다음 예에서는 결과 인스턴스에서 원래의 시작점과 끝점이 유지되지 않을 수도 있는 경우를 보여 줍니다. 이 원래의 시작점과 유지 때문에 발생 및 시작점과 끝점이 잘못 된 초래 **LineString** 인스턴스.  
  
```  
DECLARE @g geometry = 'LINESTRING(0 0, 4 0, 2 .01, 1 0)';  
DECLARE @h geometry = @g.Reduce(1);  
SELECT @g.STIsValid() AS Valid  
SELECT @g.ToString() AS Original, @h.ToString() AS Reduced;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [확장 정적 기하 도형 메서드](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

