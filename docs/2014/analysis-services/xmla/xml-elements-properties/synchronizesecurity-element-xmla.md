---
title: SynchronizeSecurity 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- SynchronizeSecurity Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.synchronizesecurity
- http://schemas.microsoft.com/analysisservices/2003/engine#SynchronizeSecurity
- urn:schemas-microsoft-com:xml-analysis#SynchronizeSecurity
helpviewer_keywords:
- SynchronizeSecurity element
ms.assetid: d37dbb95-f4a4-44ac-8eb9-f661d5bb5018
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dee99edf98aec8a9cd3b11add261cd941f9c9a0c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37330263"
---
# <a name="synchronizesecurity-element-xmla"></a>SynchronizeSecurity 요소(XMLA)
  하는 동안 역할 및 권한과 같은 보안 정의 동기화 하는 방법을 지정 된 [동기화](../xml-elements-commands/synchronize-element-xmla.md) 명령입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Synchronize>  
   ...  
   <SynchronizeSecurity>...</SynchronizeSecurity>  
   ...  
</Synchronize>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*SkipMembership*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[동기화](../xml-elements-commands/synchronize-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Security` 요소에 역할 및 권한과 같은 보안 정의 정의 하는지 여부를 결정 합니다는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 동기화 하는 동안는 `Synchronize` 명령입니다. 또한 보안 정의의 멤버로 정의된 Windows 사용자 계정 및 그룹을 `Synchronize` 명령의 일부로 포함할지 여부도 결정합니다.  
  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*SkipMembership*|`Synchronize` 명령을 실행하는 동안 보안 정의는 포함하지만 멤버 등록 정보는 제외합니다.|  
|*CopyAll*|`Synchronize` 명령을 실행하는 동안 보안 정의 및 멤버 등록 정보를 포함합니다.|  
|*IgnoreSecurity*|`Synchronize` 명령을 실행하는 동안 보안 정의를 제외합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [보안 요소 &#40;XMLA&#41;](security-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
