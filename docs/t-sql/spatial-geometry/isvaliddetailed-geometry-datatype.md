---
title: IsValidDetailed (geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- IsValidDetailed geometry
ms.assetid: 5a31e88a-ad7b-4ef7-b773-e2571f1cb3aa
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 285833fd707c524f3912fa68ca7e44878417f788
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="isvaliddetailed-geometry-datatype"></a>IsValidDetailed(geometry 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

올바르지 않은 공간 개체의 문제를 식별하는 데 도움이 되는 메시지를 반환합니다. 개체가 잘못되었을 경우 첫 번째 오류만 반환됩니다. 개체가 유효한 경우 24400 값이 반환됩니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.IsValidDetailed()  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **nvarchar(max)**  
  
 CLR 반환 형식: **string**  
  
## <a name="remarks"></a>Remarks  
 다음 표에는 가능한 반환 값이 있습니다.  
  
|반환 값|Description|  
|------------------|-----------------|  
|24400|Valid|  
|24401|유효하지 않으며 이유를 알 수 없습니다.|  
|24402|점({0})이 이 유형의 개체에서 유효하지 않은 격리된 점이므로 유효하지 않습니다.|  
|24403|다각형 가장자리의 일부 쌍이 겹치므로 유효하지 않습니다.|  
|24404|다각형 링({0})이 자체나 다른 링과 교차하므로 유효하지 않습니다.|  
|24405|일부 다각형 링이 자체나 다른 링과 교차하므로 유효하지 않습니다.|  
|24406|곡선({0})이 점에서 중복 제거되므로 유효하지 않습니다.|  
|24407|다각형 링({0})이 점({1})에서 선으로 축소되므로 유효하지 않습니다.|  
|24408|다각형 링({0})이 닫혀 있지 않으므로 유효하지 않습니다.|  
|24409|다각형 링({0})의 일부분이 다각형의 내부에 있으므로 유효하지 않습니다.|  
|24410|링({0})이 외부 링이 아닌 다각형 내의 첫 번째 링이므로 유효하지 않습니다.|  
|24411|링({0})이 다각형의 외부 링({1}) 바깥에 있으므로 유효하지 않습니다.|  
|24412|{0} 및 {1} 링이 있는 다각형의 내부가 연결되지 않으므로 유효하지 않습니다.|  
|24413|곡선({0})에 두 개의 겹치는 가장자리가 있으므로 유효하지 않습니다.|  
|24414|곡선({0})의 가장자리가 다른 곡선({1})의 가장자리와 겹치므로 유효하지 않습니다.|  
|24415|일부 다각형이 잘못된 링 구조를 가지므로 유효하지 않습니다.|  
|24416|점({1})에서 시작하는 곡선({0}) 가장자리가 대척점이 있는 중복 제거 호이거나 선이므로 유효하지 않습니다.|  
  
## <a name="examples"></a>예  
 다음 올바르지 않은 공간 개체의 예에서는 **IsValidDetailed()** 메서드가 동작하는 방법을 보여 줍니다.  
  
```sql  
DECLARE @p GEOMETRY = 'Polygon((2 2, 4 4, 4 2, 2 4, 2 2))'  
SELECT @p.IsValidDetailed()  
--Returns: 24404: Not valid because polygon ring (1) intersects itself or some other ring.  
```  
  
## <a name="see-also"></a>참고 항목  
 [geometry 인스턴스의 확장 메서드](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

