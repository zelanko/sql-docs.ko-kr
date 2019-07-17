---
title: UPDATE (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2d28df68512f9c97faebf3ee00b2aa34a2b8d1a5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028674"
---
# <a name="update-dmx"></a>UPDATE(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  변경 된 **NODE_CAPTION** 데이터 마이닝 모델의 열입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
UPDATE <model>.CONTENT  
SET NODE_CAPTION='new caption'  
[WHERE <condition expression>]  
```  
  
## <a name="arguments"></a>인수  
 *model*  
 모델 식별자입니다.  
  
 *새 캡션*  
 에 대 한 새 이름을 포함 하는 문자열을 **NODE_CAPTION** 열입니다.  
  
 *조건 식*  
 (선택 사항) 열 목록에서 반환되는 값을 제한하는 조건입니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 **업데이트** 기본 이름을 변경 하는 명령문 `Cluster 1`, 클러스터에 대 한 `001` 보다 설명적인 이름으로 `Likely Customers`입니다.  
  
```  
UPDATE [TM Clustering].CONTENT  
SET NODE_CAPTION= 'Likely Customers'  
WHERE NODE_UNIQUE_NAME = '001'  
```  
  
## <a name="see-also"></a>관련 항목  
 [Data Mining Extensions &#40;DMX&#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [Data Mining Extensions &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [DMX&#40;Data Mining Extensions&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
