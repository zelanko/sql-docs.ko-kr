---
title: IsValidDetailed(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 05f405bbbf06feac6108136c628db932b6b708bf
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36247565"
---
# <a name="isvaliddetailed-geography-data-type"></a>IsValidDetailed(geography 데이터 형식)
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
  
|반환 값|설명|  
|------------------|-----------------|  
|24400|Valid|  
|24401|유효하지 않으며 이유를 알 수 없습니다.|  
|24402|{0} 지점이 이 형식의 개체에서 유효하지 않은 격리된 지점이기 때문에 유효하지 않습니다.|  
|24403|다각형 가장자리의 일부 쌍이 겹치므로 유효하지 않습니다.|  
|24404|{0} 다각형 링이 자체나 다른 링과 교차하기 때문에 유효하지 않습니다.|  
|24405|일부 다각형 링이 자체나 다른 링과 교차하므로 유효하지 않습니다.|  
|24406|{0} 곡선이 지점에서 중복 제거되기 때문에 유효하지 않습니다.|  
|24407|{0} 다각형 링이 {1} 지점에서 선으로 축소되기 때문에 유효하지 않습니다.|  
|24408|{0} 다각형 링이 닫혀 있지 않기 때문에 유효하지 않습니다.|  
|24409|{0} 다각형 링의 일부분이 다각형의 내부에 있기 때문에 유효하지 않습니다.|  
|24410|{0} 링이 외부 링이 아닌 다각형 내의 첫 번째 링이기 때문에 유효하지 않습니다.|  
|24411|{0} 링이 다각형의 {1} 외부 링의 바깥에 있기 때문에 유효하지 않습니다.|  
|24412|{0} 및 {1} 링이 있는 다각형의 내부가 연결되지 않으므로 유효하지 않습니다.|  
|24413|{0} 곡선에 두 개의 겹치는 가장자리가 있으므로 유효하지 않습니다.|  
|24414|{0} 곡선의 가장자리가 다른 {1} 곡선의 가장자리와 겹치므로 유효하지 않습니다.|  
|24415|일부 다각형이 잘못된 링 구조를 가지므로 유효하지 않습니다.|  
|24416|{1} 지점에서 시작하는 {0} 곡선의 가장자리가 대척점이 있는 중복 제거 호이거나 선이므로 유효하지 않습니다.|  
  
## <a name="examples"></a>예  
 다음 올바르지 않은 공간 개체의 예에서는 **IsValidDetailed()** 메서드가 동작하는 방법을 보여 줍니다.  
  
```sql  
DECLARE @p GEOGRAPHY = 'Polygon((2 2, 4 4, 4 2, 2 4, 2 2))'  
SELECT @p.IsValidDetailed()  
--Returns: 24409: Not valid because some portion of polygon ring (1) lies in the interior of a polygon.  
```  
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
