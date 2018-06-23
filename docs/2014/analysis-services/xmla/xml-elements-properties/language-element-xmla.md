---
title: 언어 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Language Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Language
- microsoft.xml.analysis.language
- http://schemas.microsoft.com/analysisservices/2003/engine#Language
helpviewer_keywords:
- Language element
ms.assetid: cd998202-e43f-4c6c-8727-a15a76a520ea
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 5ea8c37369c45d35a8fe3c7366c2d5293e0c48a9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090523"
---
# <a name="language-element-xmla"></a>Language 요소(XMLA)
  부모에 대 한 로캘 식별자 (LCID)를 포함 [번역](translation-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Translation>  
   ...  
   <Language>...</Language>  
   ...  
</Translation>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|정수|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[번역](translation-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Language` 요소는 `Translation` 또는 `Name` 명령이 실행되는 동안 부모 `Translation` 요소가 부모 `Insert` 요소의 `Update` 요소를 지정된 언어로 특성 멤버에 할당하는 데 사용하는 LCID를 지정합니다.  
  
## <a name="see-also"></a>관련 항목  
 [요소를 삽입 &#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [Name 요소 &#40;XMLA&#41;](name-element-xmla.md)   
 [Update 요소 &#40;XMLA&#41;](../xml-elements-commands/update-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  