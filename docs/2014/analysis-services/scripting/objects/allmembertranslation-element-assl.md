---
title: AllMemberTranslation 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AllMemberTranslation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AllMemberTranslation
helpviewer_keywords:
- AllMemberTranslation element
ms.assetid: 31ec0c44-8f1d-457c-9e8b-61dd5bc468f7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2453a6a41fbafd35b952017fca9e04e8858713fe
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48121803"
---
# <a name="allmembertranslation-element-assl"></a>AllMemberTranslation 요소(ASSL)
  모든 멤버의 캡션에 대 한 번역을 포함 한 [계층](hierarchy-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AllMemberTranslations>  
   <AllMemberTranslation xsi:type="Translation">...  
   </AllMemberTranslation>  
</AllMemberTranslations>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|[번역](translation-element-assl.md)|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AllMemberTranslations](../collections/translations-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 AMO(Analysis Management Object) 개체 모델에서 `AllMemberTranslations` 컬렉션의 부모에 해당하는 요소는 <xref:Microsoft.AnalysisServices.Hierarchy>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [Translation 요소 &#40;ASSL&#41;](translation-element-assl.md)   
 [Hierarchy 요소 &#40;ASSL&#41;](hierarchy-element-assl.md)   
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
