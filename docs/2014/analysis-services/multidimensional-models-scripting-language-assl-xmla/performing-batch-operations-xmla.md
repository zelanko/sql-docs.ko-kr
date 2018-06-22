---
title: 일괄 처리 작업 (XMLA) 수행 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- multiple projects
- XML for Analysis, batches
- parallel batch execution [XMLA]
- transactional batches
- serial batch execution [XMLA]
- XMLA, batches
- batches [XML for Analysis]
- nontransactional batches
ms.assetid: 731c70e5-ed51-46de-bb69-cbf5aea18dda
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 7f164ca12c1de105bcd73f9b371ff4bfe2e00182
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080081"
---
# <a name="performing-batch-operations-xmla"></a>일괄 작업 수행(XMLA)
  사용할 수는 [일괄 처리](../xmla/xml-elements-commands/batch-element-xmla.md) XML for Analysis (XMLA) 단일 XMLA를 사용 하는 여러 XMLA 명령을 실행 하려면 명령을 [Execute](../xmla/xml-elements-methods-execute.md) 메서드. `Batch` 명령에 포함된 여러 명령을 단일 트랜잭션으로 실행하거나 각 명령에 대한 개별 트랜잭션을 순차적으로 또는 병렬로 실행할 수 있습니다. 또한 여러 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체를 처리하기 위해 `Batch` 명령의 아웃오브 라인 바인딩 및 기타 속성을 지정할 수 있습니다.  
  
## <a name="running-transactional-and-nontransactional-batch-commands"></a>트랜잭션 및 비트랜잭션 Batch 명령  
 `Batch` 명령은 다음 두 가지 방법 중 하나로 실행됩니다.  
  
 **트랜잭션**  
 경우는 `Transaction` 특성은 `Batch` 명령을 설정 되어 true로는 `Batch` 명령 실행 명령에 포함 된 명령을 모두는 `Batch` 단일 트랜잭션 내에서 명령을-는 *트랜잭션* 일괄 처리 합니다.  
  
 트랜잭션 일괄 처리에서 실패한 명령이 있으면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 `Batch` 명령에서 실패한 명령 이전에 실행된 모든 명령을 롤백한 후 `Batch` 명령을 즉시 종료합니다. `Batch` 명령에서 아직 실행되지 않은 명령은 처리되지 않습니다. `Batch` 명령이 종료된 후 `Batch` 명령에서는 실패한 명령에서 발생한 모든 오류를 보고합니다.  
  
 **비트랜잭션**  
 경우는 `Transaction` 특성이 false로 설정 되어는 `Batch` 명령은에 포함 된 각 명령을 실행는 `Batch` 개별 트랜잭션에서 이루어지거나에서 명령을-는 *비트랜잭션* 일괄 처리 합니다. 비트랜잭션 일괄 처리에서 실패한 명령이 있더라도 `Batch` 명령은 실패한 명령 이후의 명령을 계속 실행합니다. `Batch` 명령은 `Batch` 명령에 포함된 모든 명령을 실행하려고 시도한 후 `Batch` 명령에서 발생한 모든 오류를 보고합니다.  
  
 `Batch` 명령에 포함된 명령에서 반환된 모든 결과는 `Batch` 명령에 포함된 명령의 순서대로 반환됩니다. `Batch` 명령에서 반환되는 결과는 `Batch` 명령이 트랜잭션인지 또는 비트랜잭션인지에 따라 달라집니다.  
  
> [!NOTE]  
>  경우는 `Batch` 명령와 같은 출력을 반환 하지 않는 명령이 포함 되어는 [잠금](../xmla/xml-elements-commands/lock-element-xmla.md) 명령 및 있는지 명령이 성공적으로 실행 되는 `Batch` 명령은 빈 반환 [루트](../xmla/xml-elements-properties/root-element-xmla.md) 요소 내 결과 요소입니다. `root` 요소가 비어 있으면 `Batch` 명령에 포함된 각 명령이 해당 명령의 결과에 해당하는 `root` 요소와 일치함을 의미합니다.  
  
### <a name="returning-results-from-transactional-batch-results"></a>트랜잭션 일괄 처리 결과에서 결과 반환  
 트랜잭션 일괄 처리 내에서 실행된 명령의 결과는 전체 `Batch` 명령이 완료되어야 반환됩니다. 각 명령을 실행한 후 결과를 반환하지 않는 이유는 트랜잭션 일괄 처리 중 실패한 명령이 발생하면 전체 `Batch` 명령 및 포함하는 모든 명령이 롤백되기 때문입니다. 모든 명령을 시작 하 고 성공적으로 실행 하는 경우는 [반환](../xmla/xml-elements-properties/return-element-xmla.md) 의 요소는 [ExecuteResponse](../xmla/xml-elements-objects-executeresponse.md) 에서 반환한 요소는 `Execute` 에 대 한 메서드는 `Batch` 명령에 포함 하나 [결과](../xmla/xml-elements-properties/results-element-xmla.md) 요소 하나를 포함 하는 요소를 `root` 에 포함 된 각 성공적으로 실행된 명령에 대 한 요소는 `Batch` 명령입니다. `Batch` 명령에 포함된 명령 중 시작할 수 없거나 완료하지 못한 명령이 있으면 `Execute` 메서드에서는 실패한 명령의 오류가 포함된 `Batch` 명령에 대한 SOAP 오류를 반환합니다.  
  
### <a name="returning-results-from-nontransactional-batch-results"></a>비트랜잭션 일괄 처리 결과에서 결과 반환  
 비트랜잭션 일과 처리 내에서 실행된 명령의 결과는 `Batch` 명령에 포함된 명령의 순서와 각 명령에서 반환된 순서를 기준으로 반환됩니다. `Batch` 명령에 포함된 명령을 하나도 시작할 수 없는 경우 `Execute` 메서드에서는 `Batch` 명령에 대한 오류가 포함된 SOAP 오류를 반환합니다. 하나 이상의 명령이 성공적으로 시작된 경우 `return` 명령의 `ExecuteResponse` 메서드에서 반환된 `Execute` 요소의 `Batch` 요소에는 `results` 요소가 포함하며, 이 results 요소에는 `root` 명령에 포함된 각 명령에 대한 하나의 `Batch` 요소가 들어 있습니다. 비트랜잭션 일괄 처리에서 하나 이상의 명령을 시작할 수 없거나 완료 하지 못한 경우는 `root` 실패 한 명령에 대 한 요소를 포함 한 [오류](../xmla/xml-elements-properties/error-element-xmla.md) 오류를 설명 하는 요소입니다.  
  
> [!NOTE]  
>  비트랜잭션 일괄 처리에 포함된 명령 중 하나라도 시작할 수 있으면 비트랜잭션 일괄 처리에 포함된 모든 명령에서 `Batch` 명령의 결과에 오류를 반환하더라도 비트랜잭션 일괄 처리는 성공적으로 실행된 것으로 간주됩니다.  
  
## <a name="using-serial-and-parallel-execution"></a>순차 및 병렬 실행 사용  
 `Batch` 명령을 사용하여 포함된 명령을 순차적으로 또는 병렬로 실행할 수 있습니다. 명령이 순차적으로 실행되는 경우 `Batch` 명령에서 현재 실행 중인 명령이 완료되어야 `Batch` 명령에 포함된 다음 명령을 시작할 수 있습니다. 명령이 병렬로 실행되는 경우 `Batch` 명령을 사용하여 여러 명령을 동시에 실행할 수 있습니다.  
  
 동시에 실행 될 명령을 추가한 명령을 병렬로 실행 하는 [병렬](../xmla/xml-elements-properties/parallel-element-xmla.md) 속성의는 `Batch` 명령입니다. 현재 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 순차적인 연속만 실행할 수 [프로세스](../xmla/xml-elements-commands/process-element-xmla.md) 명령만 병렬로 합니다. 와 같은 다른 모든 XMLA 명령은 [만들기](../xmla/xml-elements-commands/create-element-xmla.md) 또는 [Alter](../xmla/xml-elements-commands/alter-element-xmla.md)에 포함 된는 `Parallel` 속성 순차적으로 실행 됩니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 `Process` 속성에 포함된 모든 `Parallel` 명령을 병렬로 실행하려고 시도하지만 포함된 모든 `Process` 명령이 병렬로 실행될 수 있다고 보장할 수는 없습니다. 인스턴스에서 각 `Process` 명령을 분석하여 병렬로 실행할 수 없는 명령으로 결정되면 `Process` 명령이 순차적으로 실행됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 연결당 하나의 활성 트랜잭션을 지원하고 비트랜잭션 일괄 처리에서는 각 명령을 별개 트랜잭션으로 실행하므로 명령을 병렬로 실행하려면 `Transaction` 명령의 `Batch` 특성을 true로 설정해야 합니다. 비트랜잭션 일괄 처리에 `Parallel` 속성이 포함되면 오류가 발생합니다.  
  
### <a name="limiting-parallel-execution"></a>병렬 실행 제한  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서는 인스턴스가 실행 중인 컴퓨터에서 최대한 많은 `Process` 명령을 병렬로 실행하려고 시도합니다. `Process` 속성의 `maxParallel` 특성을 병렬로 실행할 수 있는 `Parallel` 명령의 최대 개수를 나타내는 값으로 설정하여 동시에 실행할 수 있는 `Process` 명령의 수를 제한할 수 있습니다.  
  
 예를 들어, `Parallel` 속성에는 다음과 같은 순서의 명령이 들어 있습니다.  
  
1.  `Create`  
  
2.  `Process`  
  
3.  `Alter`  
  
4.  `Process`  
  
5.  `Process`  
  
6.  `Process`  
  
7.  `Delete`  
  
8.  `Process`  
  
9. `Process`  
  
 이 `maxParalle` 속성의 `Parallel`l 특성은 2로 설정되었습니다. 따라서 인스턴스는 이전 명령 목록을 다음 목록에 설명된 대로 실행합니다.  
  
-   명령 1이 `Create` 명령이고 `Process` 명령만 병렬로 실행될 수 있으므로 명령 1이 순차적으로 실행됩니다.  
  
-   명령 1이 완료 된 후 명령 2 순차적으로 실행 합니다.  
  
-   2 명령이 완료 된 후 명령 3 순차적으로 실행 합니다.  
  
-   명령 4 및 5 3 명령을 완료 한 후 동시에 실행 합니다. 명령 6도 `Process` 명령이지만 `maxParallel` 속성이 2로 설정되었으므로 명령 6은 명령 4 및 5와 함께 병렬로 실행될 수 없습니다.  
  
-   명령 4 및 5가 완료된 후 명령 6이 순차적으로 실행됩니다.  
  
-   명령 6이 완료된 후 명령 7이 순차적으로 실행됩니다.  
  
-   명령 7이 완료된 후 명령 8 및 9가 병렬로 실행됩니다.  
  
## <a name="using-the-batch-command-to-process-objects"></a>Batch 명령을 사용하여 개체 처리  
 `Batch` 명령에는 여러 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 처리를 지원하기 위해 특별히 포함된 여러 가지 선택적 속성 및 특성이 있습니다.  
  
-   또한 `ProcessAffectedObjects` 명령의 `Batch` 특성은 지정된 개체를 처리하는 `Process` 명령에 포함된 `Batch` 명령의 결과로 다시 처리해야 하는 개체를 인스턴스에서 처리할지 여부를 나타냅니다.  
  
-   [바인딩](../xmla/xml-elements-properties/bindings-element-xmla.md) 속성 모두에서 사용 하는 아웃오브 라인 바인딩의 컬렉션이 포함는 `Process` 의 명령은 `Batch` 명령입니다.  
  
-   [DataSource](../xmla/xml-elements-properties/source-element-xmla.md) 속성의 모든 사용 되는 데이터 원본에 대 한는 아웃오브 라인 바인딩이 포함는 `Process` 의 명령은 `Batch` 명령입니다.  
  
-   [DataSourceView](../xmla/xml-elements-properties/datasourceview-element-xmla.md) 속성 모두에서 사용 하는 데이터 원본 뷰는 아웃오브 라인 바인딩이 포함 되어는 `Process` 의 명령은 `Batch` 명령입니다.  
  
-   [ErrorConfiguration](../xmla/xml-elements-properties/errorconfiguration-element-xmla.md) 속성은 방법을 지정 하는 `Batch` 모두에서 발생 한 오류를 처리 하는 명령 `Process` 에 포함 된 명령을 `Batch` 명령입니다.  
  
    > [!IMPORTANT]  
    >  `Process` 명령이 `Bindings` 명령에 포함된 경우 `DataSource` 명령에는 `DataSourceView`, `ErrorConfiguration`, `Process` 또는 `Batch` 속성이 포함될 수 없습니다. `Process` 명령에 대해 이러한 속성을 지정해야 하는 경우에는 `Batch` 명령이 포함된 `Process` 명령의 해당 속성에 필요한 정보를 제공합니다.  
  
## <a name="see-also"></a>관련 항목  
 [요소를 일괄 처리 &#40;XMLA&#41;](../xmla/xml-elements-commands/batch-element-xmla.md)   
 [요소를 처리할 &#40;XMLA&#41;](../xmla/xml-elements-commands/process-element-xmla.md)   
 [다차원 모델 개체 처리](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Analysis Services에서 XMLA를 사용하여 개발](developing-with-xmla-in-analysis-services.md)  
  
  