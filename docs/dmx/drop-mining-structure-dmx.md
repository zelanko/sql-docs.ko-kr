---
title: DROP MINING STRUCTURE (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b83de343e94c9263ba1ca6c6c8f09be90f3793b2
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38052321"
---
# <a name="drop-mining-structure-dmx"></a>DROP MINING STRUCTURE(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 마이닝 구조를 데이터베이스에서 삭제합니다. 이 구조에 연결된 모든 마이닝 모델도 데이터베이스에서 삭제됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP MINING STRUCTURE <structure>  
```  
  
## <a name="arguments"></a>인수  
 *구조*  
 구조 식별자입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 데이터베이스에서 New Mailing 마이닝 구조를 삭제합니다.  
  
```  
DROP MINING STRUCTURE [New Mailing]  
```  
  
## <a name="see-also"></a>관련 항목  
 [Data Mining Extensions &#40;DMX&#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [Data Mining Extensions &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [DMX&#40;Data Mining Extensions&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
