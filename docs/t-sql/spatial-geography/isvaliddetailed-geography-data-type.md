---
title: "IsValidDetailed (geography 데이터 형식) | Microsoft Docs"
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
- IsValidDetailed_TSQL
- IsValidDetailed
dev_langs:
- TSQL
helpviewer_keywords:
- IsValidDetailed geography
ms.assetid: f5f0b753-c825-43ce-987d-98655d8d8702
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: abe552b7afda98443decf0b66e81ae74f8a32b00
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="isvaliddetailed-geography-data-type"></a>IsValidDetailed(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  올바르지 않은 공간 개체의 문제를 식별하는 데 도움이 되는 메시지를 반환합니다. 개체가 잘못되었을 경우 첫 번째 오류만 반환됩니다. 개체가 유효한 경우 24400 값이 반환됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.IsValidDetailed()  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **nvarchar (max)**  
  
 CLR 반환 형식: **문자열**  
  
## <a name="remarks"></a>주의  
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
|24407|다각형 링 {0} 지점 {1 \}에서 선으로 축소 되므로 유효 하지 않습니다.|  
|24408|다각형 링({0})이 닫혀 있지 않으므로 유효하지 않습니다.|  
|24409|다각형 링({0})의 일부분이 다각형의 내부에 있으므로 유효하지 않습니다.|  
|24410|링({0})이 외부 링이 아닌 다각형 내의 첫 번째 링이므로 유효하지 않습니다.|  
|24411|다각형의 외부 링 {1 \} 외부에 링 {0} 때문에 유효 하지 않습니다.|  
|24412|링 {0} 및 {1 \}는 다각형의 내부가 연결 되어 있지 않으므로 유효 하지 않습니다.|  
|24413|곡선({0})에 두 개의 겹치는 가장자리가 있으므로 유효하지 않습니다.|  
|24414|{0} 곡선의 선분 겹치는 곡선 {1 \}의 가장자리가 있으므로 유효 하지 않습니다.|  
|24415|일부 다각형이 잘못된 링 구조를 가지므로 유효하지 않습니다.|  
|24416|곡선 가장자리 지점에서 시작 하는 {0} {1 \}는 대척점이 있는 중복 제거 호 이거나 선 이므로 유효 하지 않습니다.|  
  
## <a name="examples"></a>예  
 올바르지 않은 공간 개체의 다음 예제에서는 방법을 **isvaliddetailed ()** 메서드가 동작 합니다.  
  
```tsql  
DECLARE @p GEOGRAPHY = 'Polygon((2 2, 4 4, 4 2, 2 4, 2 2))'  
SELECT @p.IsValidDetailed()  
--Returns: 24409: Not valid because some portion of polygon ring (1) lies in the interior of a polygon.  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geography 인스턴스의 확장된 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
