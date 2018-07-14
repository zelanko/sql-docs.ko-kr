---
title: Cancel 요소 (XMLA) | Microsoft Docs
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
- Cancel Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.cancel
- http://schemas.microsoft.com/analysisservices/2003/engine#Cancel
- urn:schemas-microsoft-com:xml-analysis#Cancel
helpviewer_keywords:
- Cancel command
ms.assetid: de4062c1-7434-44dc-9f01-29fcf78963bd
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fb71b55e514a2e058d50cd1c923a3e0b794ac8f9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37173274"
---
# <a name="cancel-element-xmla"></a>Cancel 요소(XMLA)
  현재 실행 중인 명령을 취소는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <Cancel>  
      <ConnectionID>...</ConnectionID>  
      <SessionID>...</SessionID>  
      <SPID>...</SPID>  
      <CancelAssociated>...</CancelAssociated>  
   </Cancel>  
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
|자식 요소|[CancelAssociated](../xml-elements-properties/cancelassociated-element-xmla.md)하십시오 [ConnectionID](../xml-elements-properties/id-element-xmla.md)합니다 [SessionID](../xml-elements-properties/sessionid-element-xmla.md), [SPID](../xml-elements-properties/spid-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `Cancel` 명령은 세션 컨텍스트 내에서 현재 실행 중인 명령을 취소합니다. 클라이언트 응용 프로그램에서 세션을 요청하지 않은 경우 명령을 취소할 수 없습니다.  
  
 `Cancel` 명령을 실행하는 중에 `Batch` 명령을 실행하면 전체 `Batch` 명령이 취소됩니다. `Batch` 명령이 트랜잭션인 경우 `Batch` 명령에 포함된 모든 명령이 롤백됩니다. `Batch` 명령이 트랜잭션이 아닌 경우 `Batch` 명령 실행 당시 실행 중이던 `Cancel` 명령에 포함된 명령만 롤백됩니다. 비트랜잭션 `Batch` 명령에서 이미 실행된 명령은 롤백되지 않습니다.  
  
 일반적으로 `Cancel` 명령은 현재 활성 세션에서 실행 중인 명령을 취소하는 데 사용됩니다. 이때 `Cancel` 명령의 자식 요소는 지정하지 않아야 합니다. 또한 관리자는 `Cancel` 명령을 사용하여 현재 활성 세션을 제외한 세션 또는 연결에서 실행되는 명령을 취소할 수 있습니다. 특정 데이터베이스에 대한 관리자 권한이 있는 역할 멤버는 해당 데이터베이스에 해당하는 연결 또는 세션 명령을 취소할 수 있고, 서버 관리자는 특정 Analysis Services 인스턴스의 연결 및 세션 명령을 취소할 수 있습니다.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스의 현재 연결 및 세션 정보를 검색하려면 `Discover` 메서드를 실행하여 DISCOVER_CONNECTIONS 및 DISCOVER_SESSIONS 스키마 행 집합을 각각 요청합니다. 특정 데이터베이스에 대한 관리자 권한이 있는 역할 멤버는 DISCOVER_SESSIONS 스키마 행 집합의 SESSION_CURRENT_DATABASE 제한 열에 해당 데이터베이스를 지정하여 해당 데이터베이스에 대한 세션만 반환할 수 있습니다. 에 대 한 자세한 내용은 합니다 `Discover` 메서드를 참조 하세요 [Discover 메서드 &#40;XMLA&#41;](../xml-elements-methods-discover.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [요소를 일괄 처리 &#40;XMLA&#41;](batch-element-xmla.md)   
 [명령 &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
