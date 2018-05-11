---
title: Error 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a9903e86d5931d92222aec00f3896a2db78732f5
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="error-element-xmla"></a>Error 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]인스턴스에서 반환된 오류에 대한 정보를 포함합니다.  
  
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
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[메시지](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|  
|자식 요소|아래 표를 참조하세요.|  
  
|상위 항목|자식 요소|  
|--------------|--------------------|  
|[메시지](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|InclusionThresholdSetting|  
|[Cell](../../../analysis-services/xmla/xml-elements-properties/cell-element-mddataset-xmla.md), [row](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|[Description](../../../analysis-services/xmla/xml-elements-properties/description-element-xmla.md), [ErrorCode](../../../analysis-services/xmla/xml-elements-properties/errorcode-element-xmla.md), [HelpFile](../../../analysis-services/xmla/xml-elements-properties/helpfile-element-xmla.md), [Source](../../../analysis-services/xmla/xml-elements-properties/source-element-error-xmla.md)|  
  
## <a name="attributes"></a>특성  
  
|Attribute|설명|  
|---------------|-----------------|  
|ErrorCode|필요한 **UnsignedInt** 특성 (경우에만 **메시지** 부모 요소입니다.) 오류의 숫자 반환 코드를 포함합니다.|  
|Severity|선택적 **문자열** 특성 (경우에만 **메시지** 부모 요소입니다.) 오류의 심각도를 포함합니다.|  
|Description|선택적 **문자열** 특성 (경우에만 **메시지** 부모 요소입니다.) 오류에 대한 설명 텍스트를 포함합니다.|  
|원본|선택적 **문자열** 특성 (경우에만 **메시지** 부모 요소입니다.) 오류를 발생시킨 구성 요소 이름을 포함합니다.|  
|HelpFile|선택적 **문자열** 특성 (경우에만 **메시지** 부모 요소입니다.) 오류를 설명하는 도움말 파일 또는 항목의 경로 및 URL을 포함합니다.|  
  
## <a name="remarks"></a>주의  
  
## <a name="see-also"></a>관련 항목:  
 [Warning 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/warning-element-xmla.md)   
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
