---
title: 요소 (XMLA) 일괄 처리 | Microsoft Docs
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
- Batch Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Batch
- microsoft.xml.analysis.batch
- http://schemas.microsoft.com/analysisservices/2003/engine#Batch
helpviewer_keywords:
- Batch command
ms.assetid: 818f3212-9605-4e34-8623-1154d9fae1f0
caps.latest.revision: 14
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 76fcd68ca71db298bc66dc63a3fa20c394c196c8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184790"
---
# <a name="batch-element-xmla"></a>Batch 요소(XMLA)
  순차 또는 병렬의 인스턴스에서 Analysis (XMLA) 명령에 대 한 하나 이상의 XML을 일괄 처리 작업으로 수행 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <Batch Transaction="Boolean" ProcessAffectedObjects="Boolean">  
      <Bindings>...</Bindings>  
      <DataSource>...</DataSource>  
      <DataSourceView>...</DataSourceView>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <Parallel>...</Parallel>  
      <!-- One or more XMLA commands -->  
   </Batch>  
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
|자식 요소|[바인딩](../xml-elements-properties/bindings-element-xmla.md), [DataSource](../xml-elements-properties/source-element-xmla.md), [DataSourceView](../xml-elements-properties/datasourceview-element-xmla.md), [ErrorConfiguration](../../scripting/objects/errorconfiguration-element-assl.md), [병렬](../xml-elements-properties/parallel-element-xmla.md)<br /><br /> One or more of the following XMLA commands: [Alter](alter-element-xmla.md), [Backup](backup-element-xmla.md), [BeginTransaction](begintransaction-element-xmla.md), [ClearCache](clearcache-element-xmla.md), [CommitTransaction](committransaction-element-xmla.md), [Create](create-element-xmla.md), [Delete](delete-element-xmla.md), [DesignAggregations](designaggregations-element-xmla.md), [Drop](drop-element-xmla.md), [Insert](insert-element-xmla.md), [Lock](lock-element-xmla.md), [MergePartitions](mergepartitions-element-xmla.md), [NotifyTableChange](notifytablechange-element-xmla.md), [Process](process-element-xmla.md), [Restore](restore-element-xmla.md), [RollbackTransaction](rollbacktransaction-element-xmla.md), [SetPasswordEncryptionKey](http://msdn.microsoft.com/en-us/fb262737-f0f4-4441-985e-3b2a94d00a9e), [Statement](statement-element-xmla.md), [Subscribe](subscribe-element-xmla.md), [Synchronize](synchronize-element-xmla.md), [Unlock](unlock-element-xmla.md), [Update](update-element-xmla.md), [UpdateCells](drop-element-xmla.md)|  
  
## <a name="attributes"></a>특성  
  
|attribute|Description|  
|---------------|-----------------|  
|ProcessAffectedObjects|선택적 `Boolean` 특성입니다. 다시 처리가 필요한 모든 개체를 처리할지 여부를 나타냅니다.<br /><br /> True로 설정하면 `Batch` 명령에 포함된 개체 처리의 결과로 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스가 다시 처리가 필요한 모든 개체를 처리합니다.<br /><br /> `false`로 설정하면 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스가 `Batch` 명령에 포함된 개체만 처리합니다.|  
|트랜잭션|선택적 `Boolean` 특성입니다. `Batch` 명령에 포함된 명령을 단일 트랜잭션으로 처리할지, 아니면 개별 트랜잭션으로 처리할지를 나타냅니다.<br /><br /> True로 설정하면 `Batch` 명령에 포함된 모든 명령이 단일 트랜잭션으로 간주됩니다. 실패한 명령이 있으면 해당 명령 이전에 실행된 명령이 롤백되고 `Batch` 명령이 후속 명령을 실행하지 않고 중지됩니다.<br /><br /> `false`로 설정하면 `Batch` 명령이 모든 명령을 실행하고 성공적으로 완료되는 각 명령의 결과를 커밋합니다.|  
  
## <a name="remarks"></a>Remarks  
  
> [!WARNING]  
>  Command/Execute/Statement는 현재 Batch 작업에서 지원되지 않습니다.  
  
 XMLA에서 일괄 처리 작업을 수행 하는 방법에 대 한 자세한 내용은 참조 [일괄 처리 작업 수행 &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [명령 &#40;XMLA&#41;](xml-elements-commands.md)  
  
  