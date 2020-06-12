---
title: DROP 마이닝 구조 (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 33c2383cf6f83b59b1b7507fa4d7daaa9e82e82e
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83670266"
---
# <a name="drop-mining-structure-dmx"></a>DROP MINING STRUCTURE(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 마이닝 구조를 데이터베이스에서 삭제합니다. 이 구조에 연결된 모든 마이닝 모델도 데이터베이스에서 삭제됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP MINING STRUCTURE <structure>  
```  
  
## <a name="arguments"></a>인수  
 *구조체나*  
 구조 식별자입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 데이터베이스에서 New Mailing 마이닝 구조를 삭제합니다.  
  
```  
DROP MINING STRUCTURE [New Mailing]  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [DMX&#40;Data Mining Extensions&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
