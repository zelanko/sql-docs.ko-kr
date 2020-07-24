---
title: 업데이트 (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f77d71eab284b695171e923cfe53b53575d45d94
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86971541"
---
# <a name="update-dmx"></a>UPDATE(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  데이터 마이닝 모델의 **NODE_CAPTION** 열을 변경 합니다.  
  
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
 **NODE_CAPTION** 열에 대 한 새 이름을 포함 하는 문자열입니다.  
  
 *조건 식*  
 (선택 사항) 열 목록에서 반환되는 값을 제한하는 조건입니다.  
  
## <a name="examples"></a>예  
 다음 예제에서 **UPDATE** 문은 클러스터의 기본 이름인를 `Cluster 1` `001` 보다 설명적인 이름으로 변경 합니다 `Likely Customers` .  
  
```  
UPDATE [TM Clustering].CONTENT  
SET NODE_CAPTION= 'Likely Customers'  
WHERE NODE_UNIQUE_NAME = '001'  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [DMX&#40;Data Mining Extensions&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
