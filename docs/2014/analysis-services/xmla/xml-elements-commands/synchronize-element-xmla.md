---
title: Synchronize 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Synchronize Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.synchronize
- urn:schemas-microsoft-com:xml-analysis#Synchronize
- http://schemas.microsoft.com/analysisservices/2003/engine#Synchronize
helpviewer_keywords:
- Synchronize command
ms.assetid: 9401323c-feff-409a-a9da-94aee47e0563
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 13bdb64dbc3ba0b034af3a54ae10a50c403555a7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48225823"
---
# <a name="synchronize-element-xmla"></a>Synchronize 요소(XMLA)
  동기화 된 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 기존의 다른 데이터베이스와 데이터베이스입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <Synchronize>  
      <Source>...</Source>  
      <SynchronizeSecurity>...</SynchronizeSecurity>  
      <ApplyCompression>...</ApplyCompression>  
      <Locations>...</Locations>  
   </Synchronize>  
</Command>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Command](../xml-elements-properties/command-element-xmla.md)|  
|자식 요소|[ApplyCompression](../xml-elements-properties/applycompression-element-xmla.md)하십시오 [위치](../xml-elements-properties/locations-element-xmla.md)를 [소스](../xml-elements-properties/source-element-synchronize-xmla.md), [SynchronizeSecurity](../xml-elements-properties/security-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `Synchronize` 명령은 대상 데이터베이스를 `Source` 요소에 지정된 원본 인스턴스 및 데이터베이스와 동기화합니다. 필요에 따라 `Synchronize` 명령은 원본 데이터베이스에 정의된 원격 파티션을 동기화합니다.  
  
 백업 파일에 저장된 개체에 사용되는 저장소 모드에 따라 `Synchronize` 명령은 다음 표에 나열된 대로 정보를 동기화합니다.  
  
|저장소 모드|정보|  
|------------------|-----------------|  
|MOLAP(다차원 OLAP)|원본 데이터, 집계 및 메타데이터|  
|HOLAP(하이브리드 OLAP)|집계 및 메타데이터|  
|ROLAP(관계형 OLAP)|메타데이터|  
  
 `Synchronize` 명령 중에는 원본 데이터베이스에 읽기 잠금이 적용되고 대상 데이터베이스에 쓰기 잠금이 적용됩니다. 두 잠금은 모두 `Synchronize` 명령이 완료된 후 해제됩니다.  
  
 데이터베이스를 동기화 하는 방법에 대 한 자세한 내용은 참조 하세요. [Backing Up, Restoring, and 데이터베이스 동기화 &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [요소를 백업 &#40;XMLA&#41;](backup-element-xmla.md)   
 [요소를 일괄 처리 &#40;XMLA&#41;](batch-element-xmla.md)   
 [병렬 요소 &#40;XMLA&#41;](../xml-elements-properties/parallel-element-xmla.md)   
 [Restore 요소 &#40;XMLA&#41;](restore-element-xmla.md)   
 [명령 &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
