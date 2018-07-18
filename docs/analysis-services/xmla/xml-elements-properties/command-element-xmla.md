---
title: 요소 (XMLA) 명령 | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6886bcd7372d4071db562a612d934e34586cdea0
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979235"
---
# <a name="command-element-xmla"></a>Command 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  실행할 명령이 포함 된 [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) 메서드.  
  
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
  
## <a name="element-characteristics"></a>요소 특성  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[실행](../../../analysis-services/xmla/xml-elements-methods-execute.md)|  
|자식 요소|[Alter](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md), [Backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [일괄 처리](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)를 [BeginTransaction](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)를 [취소](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)를 [ClearCache](../../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md) [CommitTransaction](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md), [만듭니다](../../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)를 [삭제](../../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)를 [DesignAggregations](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md), [삭제](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md), [삽입](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)합니다 [잠금](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md), [MergePartitions](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md), [NotifyTableChange](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md), [프로세스](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md), [복원](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)합니다 [RollbackTransaction](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md), [SetPasswordEncryptionKey](http://msdn.microsoft.com/fb262737-f0f4-4441-985e-3b2a94d00a9e), [문을](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md), [ 구독](../../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md), [동기화](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)합니다 [잠금을 해제](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)를 [업데이트](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md), [UpdateCells](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 **명령** 요소에 사용 되는 **Execute** 릴레이 명령 데이터 원본에 대 한 메서드. Analysis (XMLA) 1.1 사양을 지원에 대 한 XML 동안 합니다 **문을** 명령을 Analysis Services는 많은 새로운 XMLA 명령을 지원 합니다. 지원 되는 XMLA 명령에 대 한 자세한 내용은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]를 참조 하세요 [명령 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)합니다.  
  
## <a name="see-also"></a>참고자료
 [XML 데이터 형식 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
