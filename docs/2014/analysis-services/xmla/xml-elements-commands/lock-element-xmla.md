---
title: 요소 (XMLA) 잠금 | Microsoft Docs
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
- Lock Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Lock
- microsoft.xml.analysis.lock
- http://schemas.microsoft.com/analysisservices/2003/engine#Lock
helpviewer_keywords:
- Lock command
ms.assetid: a819e805-4793-43bb-8af3-16a19f8bdab3
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 44225f211ac013edd82de08c9ca82f22cb349f96
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37209873"
---
# <a name="lock-element-xmla"></a>Lock 요소(XMLA)
  지정된 된 개체를 잠급니다를 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <Lock>  
      <ID>...</ID>  
      <Object>...</Object>  
      <Mode>...</Mode>  
   </Lock>  
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
|자식 요소|[ID](../xml-elements-properties/id-element-xmla.md)하십시오 [모드](../xml-elements-properties/mode-element-xmla.md), [개체](../xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `Lock` 명령은 현재 활성 트랜잭션 컨텍스트 내에서 공유되거나 배타적으로 사용되는 개체를 잠급니다. 데이터베이스 관리자 또는 서버 관리자만 명시적으로 `Lock` 명령을 실행할 수 있습니다. 개체가 잠겨 있으면 잠금을 해제할 때까지 트랜잭션을 커밋할 수 없습니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서는 공유 잠금과 배타적 잠금이라는 두 가지 잠금 유형을 지원합니다. 지 원하는 잠금 유형에 대 한 자세한 내용은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]를 참조 하세요 [Mode 요소 &#40;XMLA&#41;](../xml-elements-properties/mode-element-xmla.md)합니다.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]는 데이터베이스 잠금만 허용합니다. `Object` 요소는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스에 대한 개체 참조를 포함해야 합니다. `Object` 요소를 지정하지 않거나 `Object` 요소가 데이터베이스 이외의 개체를 참조하면 오류가 발생합니다.  
  
 다른 명령을 실행하면 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스에서 `Lock` 명령이 암시적으로 실행됩니다. 데이터베이스의 데이터 또는 메타데이터를 읽는 작업(예: `Discover` 명령을 실행하는 `Execute` 메서드 또는 `Statement` 메서드)을 수행하면 데이터베이스에서 암시적으로 공유 잠금이 실행됩니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스에서 개체의 데이터 또는 메타데이터 변경을 커밋하는 트랜잭션(예: `Execute` 명령을 실행하는 `Alter` 메서드)을 실행하면 데이터베이스에서 암시적으로 배타적 잠금이 실행됩니다.  
  
 모든 잠금은 현재 트랜잭션의 컨텍스트에 유지됩니다. 현재 트랜잭션이 커밋 또는 롤백되면 해당 트랜잭션 내에 정의된 모든 잠금이 자동으로 해제됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [요소 잠금 해제 &#40;XMLA&#41;](lock-element-xmla.md)   
 [명령 &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
