---
title: "Password 요소 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Password Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Password
- urn:schemas-microsoft-com:xml-analysis#Password
- microsoft.xml.analysis.password
helpviewer_keywords: Password element
ms.assetid: 8a0603bd-f6a1-4b86-84f1-c83d0b03951b
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 64bd2da0a5e2ef508feaa00279f57b4604066d1e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="password-element-xmla"></a>Password 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]부모에 사용할 암호를 결정 [백업](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md) 또는 [복원](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) 명령 암호화에 백업 파일 암호 해독 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Backup> <!-- or Restore -->  
   ...  
   <Password>...</Password>  
   ...  
</Backup>  
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
|부모 요소|[백업](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [복원](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>주의  
 **Backup** 명령의 경우 **Password** 요소가 포함되어 있지 않거나 빈 문자열을 포함하면 백업 파일이 암호화되지 않습니다.  
  
 **Restore** 명령의 경우 암호화된 백업 파일을 복원하는 동안 **Password** 요소가 포함되어 있지 않거나 빈 문자열을 포함하면 오류가 발생합니다.  
  
 **Location** 요소가 **Backup** 또는 **Restore** 명령에 포함되어 있는 경우 백업 및 원격 백업 파일 모두에 대해 같은 **Password** 요소가 사용됩니다. 원격 백업 파일에 대 한 자세한 내용은 참조 하세요. [Backing Up, Restoring, 및 데이터베이스 동기화 &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>관련 항목:  
 [Location 요소 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)   
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
