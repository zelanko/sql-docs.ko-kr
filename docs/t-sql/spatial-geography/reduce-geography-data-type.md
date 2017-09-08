---
title: "(Geography 데이터 형식)를 줄이는 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Reduce_TSQL
- Reduce
dev_langs:
- TSQL
helpviewer_keywords:
- Reduce method
ms.assetid: c5dfa8c1-6764-41d8-9150-f3cb30633d3e
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c5b174f3f4b8daf99c402b110ba10d95345783d7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="reduce-geography-data-type-"></a>Reduce(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  한 근사값을 반환는 주어진 **geography** 인스턴스 인스턴스에서 지정 된 허용 오차로 Douglas-peucker 알고리즘을 실행 하 여 생성 합니다.  
  
 이 **geography** 데이터 형식 메서드 지원 **FullGlobe** 인스턴스 또는 반구 보다 큰 공간 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
.Reduce ( tolerance )  
```  
  
## <a name="arguments"></a>인수  
  
|||  
|-|-|  
|용어|정의|  
|*허용 오차*|형식의 값은 **float**합니다. *허용 오차* 는를 Douglas-peucker 알고리즘에 입력할 허용 오차입니다. *허용 오차* 는 양수 여야 합니다.|  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>주의  
 컬렉션 형식의 경우이 알고리즘 무관 하 게 작동 각 **geography** 인스턴스에 포함 된 합니다. 이 알고리즘을 수정 하지 않는 **지점** 인스턴스.  
  
 이 메서드는 끝점을 유지 하려고 **LineString** 인스턴스에 하지만 유효한 결과 유지 하기 위해 작업을 수행 하지 못할 수 있습니다.  
  
 경우 `Reduce()` 라고 음수 값을 가진이 메서드를 생성 합니다는 **ArgumentException**합니다. `Reduce()`에 사용되는 허용 오차는 양수여야 합니다.  
  
 Douglas-peucker 알고리즘의 작동 각 곡선 또는 링에서 **geography** 인스턴스의 시작점 및 끝점 제외 하 고 모든 요소를 제거 합니다. 제거 된 각 지점이 다시 추가 됩니다, 지점이 없을 때까지 가장 멀리 떨어진 지점부터 이상 *허용 오차* 결과에서입니다. 그러면 유효한 결과가 보장되므로 필요한 경우 결과가 유효하게 됩니다.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)],이 메서드가 확장 되었습니다 **FullGlobe** 인스턴스.  
  
 이 메서드는 정확하지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `LineString` 인스턴스를 만들고 `Reduce()`를 사용하여 인스턴스를 단순화합니다.  
  
```  
DECLARE @g geography = 'LineString(120 45, 120.1 45.1, 199.9 45.2, 120 46)'  
SELECT @g.Reduce(10000).ToString()  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geography 인스턴스의 확장된 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
