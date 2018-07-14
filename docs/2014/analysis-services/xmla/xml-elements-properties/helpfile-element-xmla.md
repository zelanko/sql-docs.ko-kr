---
title: HelpFile 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- HelpFile Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#HelpFile
- http://schemas.microsoft.com/analysisservices/2003/engine#HelpFile
- microsoft.xml.analysis.helpfile
helpviewer_keywords:
- HelpFile element
ms.assetid: 537ea7a8-5064-4a31-b0cd-ab7e891fef09
caps.latest.revision: 10
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6ccf47f3e47e6521dd9c3909b71315ae4d9768de
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37195983"
---
# <a name="helpfile-element-xmla"></a>HelpFile 요소(XMLA)
  부모 [Error](error-element-xmla.md) 요소를 설명하는 도움말 파일 또는 항목의 경로 및 URL을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Error>  
   ...  
   <HelpFile>...</HelpFile>  
   ...  
</Error>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[오류](error-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
