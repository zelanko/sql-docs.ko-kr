---
title: Error 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Error Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.error
- http://schemas.microsoft.com/analysisservices/2003/engine#Error
- urn:schemas-microsoft-com:xml-analysis#Error
helpviewer_keywords:
- Error element
ms.assetid: add670cb-cab2-42be-91a3-d0c385f29d16
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5b9b961a0d8d5a33cb0869b72e0250dee5456ca7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48210153"
---
# <a name="error-element-xmla"></a>Error 요소(XMLA)
  인스턴스에서 반환 된 오류에 대 한 정보가 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Message>  
   <Error   
      ErrorCode="unsignedint"   
      Severity="string"   
      Description="string"  
      Source="string"  
      HelpFile="string"  
   />  
</Message>  
<!-- or -->  
<Cell><!-- or row -->  
   <!-- A child element -->  
      <Error xmlns="urn:schemas-microsoft-com:xml-analysis:exception"  
         < ErrorCode>...</ErrorCode>  
         < Description>...</Description>  
         < Source>...</Source>  
         < HelpFile>...</HelpFile>  
      </Error>  
   <!-- /A child element -- >  
</Cell>  
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
  
## <a name="child-elements"></a>자식 요소  
  
|상위 항목|자식 요소|  
|--------------|--------------------|  
|[메시지](message-element-xmla.md)|없음|  
|[셀](cell-element-mddataset-xmla.md), [행](description-element-xmla.md)합니다 [ErrorCode](errorcode-element-xmla.md)를 [HelpFile](file-element-xmla.md), [원본](source-element-error-xmla.md)|  
  
## <a name="attributes"></a>특성  
  
|attribute|Description|  
|---------------|-----------------|  
|ErrorCode|필요한 `UnsignedInt` 특성 (경우에만 `Message` 부모 요소입니다.) 오류의 숫자 반환 코드를 포함합니다.|  
|Severity|선택적 `String` 특성 (경우에만 `Message` 부모 요소입니다.) 오류의 심각도를 포함합니다.|  
|Description|선택적 `String` 특성 (경우에만 `Message` 부모 요소입니다.) 오류에 대한 설명 텍스트를 포함합니다.|  
|원본|선택적 `String` 특성 (경우에만 `Message` 부모 요소입니다.) 오류를 발생시킨 구성 요소 이름을 포함합니다.|  
|HelpFile|선택적 `String` 특성 (경우에만 `Message` 부모 요소입니다.) 오류를 설명하는 도움말 파일 또는 항목의 경로 및 URL을 포함합니다.|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [Warning 요소 &#40;XMLA&#41;](warning-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
