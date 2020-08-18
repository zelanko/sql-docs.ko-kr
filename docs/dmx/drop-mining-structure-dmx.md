---
description: DROP MINING STRUCTURE(DMX)
title: DROP 마이닝 구조 (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ad77fb58a630765eb6361b30bde22a90f291b18d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88413370"
---
# <a name="drop-mining-structure-dmx"></a>DROP MINING STRUCTURE(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  지정한 마이닝 구조를 데이터베이스에서 삭제합니다. 이 구조에 연결된 모든 마이닝 모델도 데이터베이스에서 삭제됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP MINING STRUCTURE <structure>  
```  
  
## <a name="arguments"></a>인수  
 *구조체나*  
 구조 식별자입니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 데이터베이스에서 New Mailing 마이닝 구조를 삭제합니다.  
  
```  
DROP MINING STRUCTURE [New Mailing]  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [DMX&#40;Data Mining Extensions&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
