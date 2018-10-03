---
title: Warning 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Warning Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Warning
- microsoft.xml.analysis.warning
- http://schemas.microsoft.com/analysisservices/2003/engine#Warning
helpviewer_keywords:
- Warning element
ms.assetid: a34a6caa-4b68-486b-8f50-cdc124c65888
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9f0dfa8e3cc45291a32885674fe5f77145aca2f0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079893"
---
# <a name="warning-element-xmla"></a>Warning 요소(XMLA)
  인스턴스에서 반환 된 경고에 대 한 정보가 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Message>  
   <Warning   
      ErrorCode="unsignedint"   
      Severity="string"   
      Description="string"  
      Source="string"  
      HelpFile="string"  
   />  
</Message>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[메시지](message-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="attributes"></a>특성  
  
|attribute|Description|  
|---------------|-----------------|  
|ErrorCode|필요한 `UnsignedInt` 특성입니다. 경고의 숫자 반환 코드를 포함합니다.|  
|Severity|선택적 `String` 특성입니다. 경고의 심각도를 포함합니다.|  
|Description|선택적 `String` 특성입니다. 경고에 대한 설명 텍스트를 포함합니다.|  
|원본|선택적 `String` 특성입니다. 경고를 생성한 구성 요소 이름을 포함합니다.|  
|HelpFile|선택적 `String` 특성입니다. 경고를 설명하는 도움말 파일 또는 항목의 경로 또는 URL을 포함합니다.|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [Error 요소 &#40;XMLA&#41;](error-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
