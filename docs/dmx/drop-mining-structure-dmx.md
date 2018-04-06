---
title: DROP MINING STRUCTURE (DMX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP MINING STRUCTURE
- DROP_MINING_STRUCTURE
dev_langs:
- DMX
helpviewer_keywords:
- removing mining structures
- dropping mining structures
- DROP MINING STRUCTURE statement
- deleting mining structures
- mining structures [DMX], deleting
ms.assetid: 30df8c36-3a15-4d8c-98f3-0f8917be9fc8
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 955b0c8a70cf7b051515f88ff1c73a593522e873
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
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
  
## <a name="see-also"></a>관련 항목:  
 [Data Mining Extensions &#40; DMX &#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [Data Mining Extensions &#40; DMX &#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [DMX&#40;Data Mining Extensions&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
