---
title: Version 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Version Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Version
helpviewer_keywords:
- Version element
ms.assetid: fb26fe5d-de40-443b-a8bc-031c950552e6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2e8c8cde757b0de5fb4076c395ac915650a12d4a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48091313"
---
# <a name="version-element-assl"></a>Version 요소(ASSL)
  인스턴스의 읽기 전용 버전 번호를 포함 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 으로 표시 합니다 [Server](../objects/server-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Server>  
      ...  
      <Version>...</Version>  
   ...  
</Server>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Server](../objects/server-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `Version` 요소는 설치된 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 버전을 나타냅니다.  
  
 부모에 해당 하는 요소가 `Version` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Server>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Edition 요소 &#40;ASSL&#41;](edition-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
