---
title: Synchronize 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5c3a4d20c7799281f40fa6ae13e89010cebe1ec6
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="synchronize-element-xmla"></a>Synchronize 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  동기화는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 기존의 다른 데이터베이스를 사용 하 여 데이터베이스입니다.  
  
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
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|자식 요소|[ApplyCompression](../../../analysis-services/xmla/xml-elements-properties/applycompression-element-xmla.md), [위치](../../../analysis-services/xmla/xml-elements-properties/locations-element-xmla.md), [소스](../../../analysis-services/xmla/xml-elements-properties/source-element-synchronize-xmla.md), [SynchronizeSecurity](../../../analysis-services/xmla/xml-elements-properties/synchronizesecurity-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 **Synchronize** 명령은 대상 데이터베이스를 **Source** 요소에 지정된 원본 인스턴스 및 데이터베이스와 동기화합니다. 필요에 따라 **Synchronize** 명령은 원본 데이터베이스에 정의된 원격 파티션을 동기화합니다.  
  
 백업 파일에 저장된 개체에 사용되는 저장소 모드에 따라 **Synchronize** 명령은 다음 표에 나열된 대로 정보를 동기화합니다.  
  
|저장소 모드|정보|  
|------------------|-----------------|  
|MOLAP(다차원 OLAP)|원본 데이터, 집계 및 메타데이터|  
|HOLAP(하이브리드 OLAP)|집계 및 메타데이터|  
|ROLAP(관계형 OLAP)|메타데이터|  
  
 **Synchronize** 명령 중에는 원본 데이터베이스에 읽기 잠금이 적용되고 대상 데이터베이스에 쓰기 잠금이 적용됩니다. 두 잠금은 모두 **Synchronize** 명령이 완료된 후 해제됩니다.  
  
 데이터베이스 동기화 하는 방법에 대 한 자세한 내용은 참조 [Backing Up, Restoring, and Synchronizing &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [요소 & #40; 백업 XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)   
 [일괄 처리 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)   
 [Parallel 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md)   
 [요소 & #40; 복원 XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [명령 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
