---
title: 버전 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: bd3b74dbb2341427b4eadf92dad6e12d81f523ad
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="version-element-assl"></a>Version 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  인스턴스의 읽기 전용 버전 번호를 포함 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 나타내는 [서버](../../../analysis-services/scripting/objects/server-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Server>  
      ...  
      <Version>...</Version>  
   ...  
</Server>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[서버](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **버전** 요소 설명의 버전 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 가 설치 되어 있습니다.  
  
 부모에 해당 하는 요소 **버전** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Server>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Edition 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/edition-element-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
