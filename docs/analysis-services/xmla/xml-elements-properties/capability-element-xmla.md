---
title: "Capability 요소 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Capability Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Capability
- http://schemas.microsoft.com/analysisservices/2003/engine#Capability
- microsoft.xml.analysis.capability
helpviewer_keywords:
- Capability element
ms.assetid: 544a733e-77fc-48a0-8f92-9cd1fdbcf824
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 50a1509e5b4b51778e329dec7bea9554cfca4234
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="capability-element-xmla"></a>Capability 요소(XMLA)
  부모 [ProtocolCapabilities](../../../analysis-services/xmla/xml-elements-headers/protocolcapabilities-element-xmla.md) 머리글 요소에서의 프로토콜 기능에 대한 지원을 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ProtocolCapabilities>  
   ...  
   <Capability>...</Capability>  
   ...  
</ProtocolCapabilities>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ProtocolCapabilities](../../../analysis-services/xmla/xml-elements-headers/protocolcapabilities-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **기능** 요소를 포함 하는 응용 프로그램 이진 또는 압축과 같은 특정 기능이 지원 됨을 나타냅니다는 **ProtocolCapabilities** 헤더 요소에는 인스턴스에서 또는 SOAP 요청의 SOAP 헤더 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 포함는 **ProtocolCapabilities** SOAP 응답의 SOAP 헤더에 헤더 요소입니다. **Capability** 요소의 값은 지원될 기능의 이름입니다.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]는 다음 표에 나열된 기능을 지원합니다.  
  
|기능 이름|설명|  
|---------------------|-----------------|  
|sx|이진 XML 지원|  
|xpress|압축 지원|  
  
## <a name="see-also"></a>관련 항목:  
 [관리 연결 및 세션 &#40; XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

