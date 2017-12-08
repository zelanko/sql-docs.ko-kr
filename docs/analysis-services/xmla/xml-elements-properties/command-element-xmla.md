---
title: "Command 요소 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Command Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.command
- Command
- urn:schemas-microsoft-com:xml-analysis#Command
- http://schemas.microsoft.com/analysisservices/2003/engine#Command
helpviewer_keywords: Command element
ms.assetid: 9abc14df-7cbe-46bc-ba0f-f0691c19afad
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9dad2fd03f81522873b5e40bb09c709fad4e2fbf
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="command-element-xmla"></a>Command 요소(XMLA)
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
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[실행](../../../analysis-services/xmla/xml-elements-methods-execute.md)|  
|자식 요소|[Alter](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md), [백업](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [일괄 처리](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md), [BeginTransaction](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md), [취소](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md), [ClearCache](../../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md), [CommitTransaction](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md), [만들](../../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md), [삭제](../../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md), [DesignAggregations](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md), [삭제](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md), [삽입](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [잠금](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md), [MergePartitions](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md), [NotifyTableChange](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md), [프로세스](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md), [복원](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md), [RollbackTransaction](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md), [SetPasswordEncryptionKey](http://msdn.microsoft.com/en-us/fb262737-f0f4-4441-985e-3b2a94d00a9e), [문을](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md), [구독](../../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md), [동기화](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md), [잠금 해제](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md), [업데이트](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md), [UpdateCells](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 **명령** 요소에서 사용 되는 **Execute** 메서드를 데이터 원본에 릴레이 명령입니다. Analysis (XMLA) 1.1 사양은 지원에 대 한 XML 동안는 **문을** 명령을 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 많은 새로운 XMLA 명령을 지원 합니다. 지원 되는 XMLA 명령에 대 한 자세한 내용은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], 참조 [명령 &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md).  
  
## <a name="see-also"></a>관련 항목:  
 [XML 데이터 형식 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
