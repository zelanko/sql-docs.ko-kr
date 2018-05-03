---
title: 요소 (XMLA) 일괄 처리 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Batch Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Batch
- microsoft.xml.analysis.batch
- http://schemas.microsoft.com/analysisservices/2003/engine#Batch
helpviewer_keywords:
- Batch command
ms.assetid: 818f3212-9605-4e34-8623-1154d9fae1f0
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 23f6c8d3ed1dbf073b09beec5c67b1b096f11e34
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="batch-element-xmla"></a>Batch 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]인스턴스에서 하나 이상의 XMLA(XML for Analysis) 명령을 일괄 처리 작업(순차 또는 병렬)으로 수행합니다.  
  
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
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|자식 요소|[바인딩](../../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md), [DataSource](../../../analysis-services/xmla/xml-elements-properties/datasource-element-xmla.md), [DataSourceView](../../../analysis-services/xmla/xml-elements-properties/datasourceview-element-xmla.md), [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md), [병렬](../../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md)<br /><br /> 다음 XMLA 명령 중 하나 이상이: [Alter](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md), [백업](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [BeginTransaction](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md), [ClearCache](../../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md), [ CommitTransaction](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md), [만들](../../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md), [삭제](../../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md), [DesignAggregations](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md), [Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md), [삽입](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [잠금](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md), [MergePartitions](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md), [NotifyTableChange](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md), [프로세스](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md), [복원](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md), [RollbackTransaction](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md), [SetPasswordEncryptionKey](http://msdn.microsoft.com/en-us/fb262737-f0f4-4441-985e-3b2a94d00a9e), [문을](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md), [구독](../../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md), [동기화](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md), [잠금 해제](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md), [업데이트](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md), [UpdateCells](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)|  
  
## <a name="attributes"></a>특성  
  
|Attribute|Description|  
|---------------|-----------------|  
|ProcessAffectedObjects|선택적 **Boolean** 특성입니다. 다시 처리가 필요한 모든 개체를 처리할지 여부를 나타냅니다.<br /><br /> 경우 true로 설정 된 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 포함 된 개체를 처리 한 결과로 다시 처리 해야 하는 모든 개체를 처리는 **일괄 처리** 명령입니다.<br /><br /> 경우로 설정 **false**, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스 처리에 포함 하는 개체에 대해서만 **일괄 처리** 명령입니다.|  
|트랜잭션|선택적 **Boolean** 특성입니다. **Batch** 명령에 포함된 명령을 단일 트랜잭션으로 처리할지, 아니면 개별 트랜잭션으로 처리할지를 나타냅니다.<br /><br /> True로 설정하면 **Batch** 명령에 포함된 모든 명령이 단일 트랜잭션으로 간주됩니다. 실패한 명령이 있으면 해당 명령 이전에 실행된 명령이 롤백되고 **Batch** 명령이 후속 명령을 실행하지 않고 중지됩니다.<br /><br /> **false**로 설정하면 **Batch** 명령이 모든 명령을 실행하고 성공적으로 완료되는 각 명령의 결과를 커밋합니다.|  
  
## <a name="remarks"></a>주의  
  
> [!WARNING]  
>  Command/Execute/Statement는 현재 Batch 작업에서 지원되지 않습니다.  
  
 XMLA에서 일괄 처리 작업을 수행 하는 방법에 대 한 자세한 내용은 참조 [일괄 처리 작업 수행 &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [명령 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
