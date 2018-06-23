---
title: Subscribe 요소 (XMLA) | Microsoft Docs
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
- Subscribe Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Subscribe
- microsoft.xml.analysis.subscribe
- http://schemas.microsoft.com/analysisservices/2003/engine#Subscribe
helpviewer_keywords:
- Subscribe command
ms.assetid: aad50dd7-44d4-4d83-a973-187f9aed35ec
caps.latest.revision: 14
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 94caa1327febf0c7fd5a489c7558ea793977d027
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090936"
---
# <a name="subscribe-element-xmla"></a>Subscribe 요소(XMLA)
  추적에 구독 하 고 추적 이벤트를 포함 하는 행 집합을 반환 된 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <Subscribe>  
      <Object>...</Object>  
   </Subscribe>  
</Command>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Command](../xml-elements-properties/command-element-xmla.md)|  
|자식 요소|[개체](../xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `Subscribe` 명령을 구독 하 고 스트림이 지정된 된 추적의 행 집합에서 다시는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스. 추적 이외의 개체가에 지정 된 경우는 `Object` 요소 오류가 발생 합니다.  
  
 `Object` 요소가 지정되지 않은 경우 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에서 세션 추적을 정의 및 구독합니다. 세션 추적은 현재 세션의 고정된 추적 이벤트 집합을 반환합니다.  
  
 클라이언트 응용 프로그램에 대 한 연결을 종료 하는 경우이 명령에서 반환 된 행 집합 스트림이 종료 됩니다는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스의 경우 세션을는 `Subscribe` 명령을 실행 종료 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [명령 &#40;XMLA&#41;](xml-elements-commands.md)  
  
  