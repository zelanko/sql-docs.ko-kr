---
title: Reduce(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
ms.assetid: c5dfa8c1-6764-41d8-9150-f3cb30633d3e
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: db28891a7e1bed887f3a8d58a5994734d65b9185
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85705844"
---
# <a name="reduce-geography-data-type-"></a>Reduce(geography 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  인스턴스에서 지정된 허용 오차로 Douglas-Peucker 알고리즘을 실행하여 생성한 지정된 **geography** 인스턴스에 대한 근사값을 반환합니다.  
  
 이 **geography** 데이터 형식 메서드는 **FullGlobe** 인스턴스 또는 반구보다 큰 공간 인스턴스를 지원합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.Reduce ( tolerance )  
```  
  
## <a name="arguments"></a>인수  
  
|||  
|-|-|  
|용어|정의|  
|*tolerance*|**float** 형식의 값입니다. *tolerance*는 Douglas-Peucker 알고리즘에 입력할 허용 오차입니다. *tolerance*는 양수여야 합니다.|  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>설명  
 컬렉션 형식의 경우 이 알고리즘은 인스턴스에 포함된 각 **geography**에 대해 독립적으로 작동합니다. 이 알고리즘은 **Point** 인스턴스를 수정하지는 않습니다.  
  
 이 메서드는 **LineString** 인스턴스의 엔드포인트를 유지하려고 하지만 유효한 결과를 유지하기 위해 이러한 엔드포인트를 유지하지 못할 수 있습니다.  
  
 음수 값을 사용하여 `Reduce()`를 호출하면 이 메서드는 **ArgumentException**을 발생시킵니다. `Reduce()`에 사용되는 허용 오차는 양수여야 합니다.  
  
 Douglas-Peucker 알고리즘은 시작점과 끝점을 제외한 모든 지점을 제거하여 **geography** 인스턴스의 각 곡선 또는 링에서 작동합니다. 가장 멀리 떨어진 지점부터 결과의 *허용 오차*보다 큰 지점이 없을 때까지 제거된 각 지점이 다시 추가됩니다. 그러면 유효한 결과가 보장되므로 필요한 경우 결과가 유효하게 됩니다.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 이 메서드는 **FullGlobe** 인스턴스로 확장되었습니다.  
  
 이 메서드는 정확하지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `LineString` 인스턴스를 만들고 `Reduce()`를 사용하여 인스턴스를 단순화합니다.  
  
```  
DECLARE @g geography = 'LineString(120 45, 120.1 45.1, 199.9 45.2, 120 46)'  
SELECT @g.Reduce(10000).ToString()  
```  
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
