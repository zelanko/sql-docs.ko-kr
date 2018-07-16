---
title: 요소 (XMLA) 명령 | Microsoft Docs
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
- Command Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.command
- Command
- urn:schemas-microsoft-com:xml-analysis#Command
- http://schemas.microsoft.com/analysisservices/2003/engine#Command
helpviewer_keywords:
- Command element
ms.assetid: 9abc14df-7cbe-46bc-ba0f-f0691c19afad
caps.latest.revision: 31
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f9b461e0ec565776ead270902cf6c01ebe7409d3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37332243"
---
# <a name="command-element-xmla"></a>Command 요소(XMLA)
  실행할 명령이 포함 된 [Execute](../xml-elements-methods-execute.md) 메서드.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Execute>  
   ...  
   <Command>  
      <Alter>...</Alter>  
      <!-- or -->  
      <Backup>...</Backup>  
      <!-- or -->  
      <Batch>...</Batch>  
      <!-- or -->  
      <BeginTransaction>...</BeginTransaction>  
      <!-- or -->  
      <Cancel>...</Cancel>  
      <!-- or -->  
      <ClearCache>...</ClearCache>  
      <!-- or -->  
      <CommitTransaction>...</CommitTransaction>  
      <!-- or -->  
      <Create>...</Create>  
      <!-- or -->  
      <Delete>...</Delete>  
      <!-- or -->  
      <DesignAggregations>...</DesignAggregations>  
      <!-- or -->  
      <Drop>...</Drop>  
      <!-- or -->  
      <Insert>...</Insert>  
      <!-- or -->  
      <Lock>...</Lock>  
      <!-- or -->  
      <MergePartitions>...</MergePartitions>  
      <!-- or -->  
      <NotifyTableChange>...</NotifyTableChange>  
      <!-- or -->  
      <Process>...</Process>  
      <!-- or -->  
      <Restore>...</Restore>  
      <!-- or -->  
      <RollbackTransaction>...</RollbackTransaction>  
      <!-- or -->  
      <SetPasswordEncryptionKey>...</SetPasswordEncryptionKey>  
      <!-- or -->  
      <Statement>...</Statement>  
      <!-- or -->  
      <Subscribe>...</Subscribe>  
      <!-- or -->  
      <Synchronize>...</Synchronize>  
      <!-- or -->  
      <Unlock>...</Unlock>  
      <!-- or -->  
      <Update>...</Update>  
      <!-- or -->  
      <UpdateCells>...</UpdateCells>  
   </Command>  
   ...  
</Execute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[실행](../xml-elements-methods-execute.md)|  
|자식 요소|[Alter](../xml-elements-commands/alter-element-xmla.md), [Backup](../xml-elements-commands/backup-element-xmla.md), [일괄 처리](../xml-elements-commands/batch-element-xmla.md)를 [BeginTransaction](../xml-elements-commands/begintransaction-element-xmla.md)를 [취소](../xml-elements-commands/cancel-element-xmla.md)를 [ClearCache](../xml-elements-commands/clearcache-element-xmla.md) [CommitTransaction](../xml-elements-commands/committransaction-element-xmla.md), [만듭니다](../xml-elements-commands/create-element-xmla.md)를 [삭제](../xml-elements-commands/delete-element-xmla.md)를 [DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md), [삭제](../xml-elements-commands/drop-element-xmla.md), [삽입](../xml-elements-commands/insert-element-xmla.md)합니다 [잠금](../xml-elements-commands/lock-element-xmla.md), [MergePartitions](../xml-elements-commands/mergepartitions-element-xmla.md), [NotifyTableChange](../xml-elements-commands/notifytablechange-element-xmla.md), [프로세스](../xml-elements-commands/process-element-xmla.md), [복원](../xml-elements-commands/restore-element-xmla.md)합니다 [RollbackTransaction](../xml-elements-commands/rollbacktransaction-element-xmla.md), [SetPasswordEncryptionKey](http://msdn.microsoft.com/en-us/fb262737-f0f4-4441-985e-3b2a94d00a9e), [문을](../xml-elements-commands/statement-element-xmla.md), [ 구독](../xml-elements-commands/subscribe-element-xmla.md), [동기화](../xml-elements-commands/synchronize-element-xmla.md)합니다 [잠금을 해제](../xml-elements-commands/unlock-element-xmla.md)를 [업데이트](../xml-elements-commands/update-element-xmla.md), [UpdateCells](../xml-elements-commands/drop-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `Command` 요소는 명령을 데이터 원본에 릴레이하기 위해 `Execute` 메서드에 사용됩니다. Analysis (XMLA) 1.1 사양을 지원에 대 한 XML 동안 합니다 `Statement` 명령인 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 많은 새로운 XMLA 명령을 지원 합니다. 지원 되는 XMLA 명령에 대 한 자세한 내용은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]를 참조 하세요 [명령 &#40;XMLA&#41;](../xml-elements-commands/xml-elements-commands.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [XML 데이터 형식 &#40;XMLA&#41;](../xml-data-types/xml-data-types-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
