---
title: Batch 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2f249402d3348e491a409da52db76f531bcd594f
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38981895"
---
# <a name="batch-element-xmla"></a>Batch 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  순차적으로 또는 Analysis Services 인스턴스에서 동시에 하나 이상의 XML Analysis (XMLA) 명령에 대 한 일괄 처리 작업으로 수행합니다.  
  
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
  
## <a name="element-characteristics"></a>요소 특성  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|자식 요소|[바인딩을](../../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md), [DataSource](../../../analysis-services/xmla/xml-elements-properties/datasource-element-xmla.md)를 [DataSourceView](../../../analysis-services/xmla/xml-elements-properties/datasourceview-element-xmla.md)를 [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md), [병렬](../../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md)<br /><br /> 다음 XMLA 명령 중 하나 이상이: [Alter](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md), [백업](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)합니다 [BeginTransaction](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)를 [ClearCache](../../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md), [ CommitTransaction](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md), [만듭니다](../../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md), [삭제](../../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)를 [DesignAggregations](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md), [Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md), [삽입](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [잠금](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)를 [MergePartitions](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)합니다 [NotifyTableChange](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md), [프로세스](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md), [복원](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md), [RollbackTransaction](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)를 [SetPasswordEncryptionKey](http://msdn.microsoft.com/fb262737-f0f4-4441-985e-3b2a94d00a9e)합니다 [문](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md), [구독](../../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md), [동기화](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)합니다 [잠금 해제](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)를 [업데이트](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md), [UpdateCells](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)|  
  
## <a name="attributes"></a>특성  
  
|attribute|Description|  
|---------------|-----------------|  
|ProcessAffectedObjects|선택적 **Boolean** 특성입니다. 다시 처리가 필요한 모든 개체를 처리할지 여부를 나타냅니다.<br /><br /> 경우 true로 설정 합니다 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 에 포함 된 개체를 처리 한 결과로 다시 처리 해야 하는 모든 개체를 처리 하는 인스턴스를 **일괄 처리** 명령입니다.<br /><br /> 경우로 **false**의 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스 처리에 포함 된 개체만 합니다 **일괄 처리** 명령입니다.|  
|트랜잭션|선택적 **Boolean** 특성입니다. **Batch** 명령에 포함된 명령을 단일 트랜잭션으로 처리할지, 아니면 개별 트랜잭션으로 처리할지를 나타냅니다.<br /><br /> True로 설정하면 **Batch** 명령에 포함된 모든 명령이 단일 트랜잭션으로 간주됩니다. 실패한 명령이 있으면 해당 명령 이전에 실행된 명령이 롤백되고 **Batch** 명령이 후속 명령을 실행하지 않고 중지됩니다.<br /><br /> **false**로 설정하면 **Batch** 명령이 모든 명령을 실행하고 성공적으로 완료되는 각 명령의 결과를 커밋합니다.|  
  
## <a name="remarks"></a>Remarks  
  
> [!WARNING]  
>  Command/Execute/Statement는 현재 Batch 작업에서 지원되지 않습니다.  
  
 XMLA에서 일괄 처리 작업을 수행 하는 방법에 대 한 자세한 내용은 참조 하세요. [일괄 처리 작업 수행 &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md)합니다.  
  
## <a name="see-also"></a>참고자료
 [명령 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
