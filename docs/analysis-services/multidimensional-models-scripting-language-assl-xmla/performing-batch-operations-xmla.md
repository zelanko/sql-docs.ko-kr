---
title: 일괄 작업 수행 (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6c451d13016915c9218efb2963429f8f5a7709e2
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52544230"
---
# <a name="performing-batch-operations-xmla"></a>일괄 작업 수행(XMLA)
  사용할 수는 [일괄 처리](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla) XMLA (XML for Analysis) 단일 XMLA를 사용 하는 여러 XMLA 명령을 실행할 명령을 [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) 메서드. 에 포함 된 여러 명령을 실행할 수 있습니다 합니다 **일괄 처리** 명령을 단일 트랜잭션으로 또는 각 명령에 대 한 개별 트랜잭션을, 직렬에서 또는 병렬입니다. 아웃오브 라인 바인딩 및 기타 속성을 지정할 수도 있습니다는 **일괄 처리** 여러 처리 명령을 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체입니다.  
  
## <a name="running-transactional-and-nontransactional-batch-commands"></a>트랜잭션 및 비트랜잭션 Batch 명령  
 합니다 **일괄 처리** 명령이 두 가지 방법 중 하나에서 명령을 실행 합니다.  
  
 **트랜잭션**  
 경우는 **트랜잭션** 특성을 **일괄 처리** 명령 집합은 true로는 **일괄 처리** 명령이 실행 명령에 포함 된 명령의 모든는 **일괄처리** 트랜잭션 a는 단일 명령을 *트랜잭션* 일괄 처리 합니다.  
  
 트랜잭션 일괄 처리에서 실패 한 명령이 있으면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 모든 명령을 롤백한 합니다 **일괄 처리** 실패 한 명령 전에 실행 된 명령 및 **일괄 처리** 명령을 즉시 종료 합니다. 모든 명령에는 **일괄 처리** 아직 실행 되지 않은 명령 실행 되지 않습니다. 후 합니다 **일괄 처리** 명령이 종료 합니다 **일괄 처리** 명령에서는 실패 한 명령에 발생 한 모든 오류를 보고 합니다.  
  
 **비트랜잭션**  
 경우는 **트랜잭션** 특성이 false로 설정 된를 **일괄 처리** 명령은에 포함 된 각 명령을 실행 합니다 **일괄 처리** 트랜잭션을 별도의 명령을  *비트랜잭션* 일괄 처리 합니다. 비트랜잭션 일괄 처리에서 실패 한 명령이 있으면 합니다 **일괄 처리** 명령은 실패 한 명령 이후의 명령을 계속 합니다. 후는 **일괄 처리** 명령이 모든 명령을 실행 하려고 하는 **일괄 처리** 명령에 포함는 **일괄 처리** 명령을 발생 한 모든 오류를 보고 합니다.  
  
 에 포함 된 명령을 사용 하 여 반환 된 모든 결과 **일괄 처리** 는 명령에 포함 된 동일한 순서로 반환 됩니다 합니다 **일괄 처리** 명령입니다. 반환한 결과 **일괄 처리** 명령 인지 여부에 따라 달라 집니다를 **일괄 처리** 트랜잭션인지 또는 비트랜잭션 명령입니다.  
  
> [!NOTE]  
>  경우를 **일괄 처리** 명령와 같은 출력을 반환 하지 않는 명령을 포함 합니다 [잠금](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) 명령 및는 명령이 성공적으로 실행 되는 **일괄 처리** 명령은 빈을 반환 합니다. [루트](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/root-element-xmla) 결과 요소 내의 요소입니다. 빈 **루트** 요소에 포함 된 각 명령 하면를 **일괄 처리** 명령은 일치 하는 적절 한 **루트** 해당 명령의 결과 대 한 요소입니다.  
  
### <a name="returning-results-from-transactional-batch-results"></a>트랜잭션 일괄 처리 결과에서 결과 반환  
 트랜잭션 일괄 처리 내에서 실행 된 명령의 결과는 전체 될 때까지 반환 되지 않습니다 **일괄 처리** 명령이 완료 되어야 합니다. 한 명령이 실패는 트랜잭션 일괄 처리는 발생 하면 전체 때문에 각 명령을 실행 한 후에 결과가 반환 되지 않습니다 **일괄 처리** 명령 및 포함 하는 모든 명령이 롤백됩니다. 모든 명령을 시작 하 고 성공적으로 실행 하는 경우는 [반환](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/return-element-xmla) 의 요소를 [ExecuteResponse](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects-executeresponse) 에서 반환한 요소를 **Execute** 에 대 한 메서드는 **일괄 처리**  하나의 [결과](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/results-element-xmla) 차례로 하나를 포함 하는 요소 **루트** 에 포함 된 각 성공적으로 실행된 명령에 대 한 요소는 **일괄처리** 명령입니다. 명령에 하는 경우는 **일괄 처리** 명령을 시작할 수 없거나 완료 하지 못한를 **Execute** 에 대 한 SOAP 오류를 반환 하는 메서드를 **일괄 처리** 의 오류를 포함 하는 명령을 실패 한 명령입니다.  
  
### <a name="returning-results-from-nontransactional-batch-results"></a>비트랜잭션 일괄 처리 결과에서 결과 반환  
 비트랜잭션 일과 처리 내에서 실행 된 명령의 결과 명령에 포함 된 순서 대로 반환 됩니다 합니다 **일괄 처리** 명령와 각 명령에 의해 반환 됩니다. 경우에 포함 된 명령이 없습니다는 **일괄 처리** 명령을 성공적으로 시작할 수는 **Execute** 에 대 한 오류가 포함 된 SOAP 오류를 반환 하는 메서드를 **일괄 처리** 명령. 이상의 명령이 성공적으로 시작 하는 경우는 **반환** 의 요소를 **ExecuteResponse** 에서 반환한 요소를 **Execute** 에 대 한 메서드는 **일괄 처리**  하나의 **결과** 차례로 하나를 포함 하는 요소 **루트** 요소에 포함 된 각 명령에 대 한 합니다 **Batch** 명령 . 비트랜잭션 일괄 처리에서 명령을 하나 이상 시작할 수 없거나 완료 하지 못한 경우 합니다 **루트** 실패 한 명령에 대 한 요소에 포함 되어는 [오류](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/error-element-xmla) 오류를 설명 하는 요소입니다.  
  
> [!NOTE]  
>  비트랜잭션 일괄 처리에 포함 된 모든 명령 결과에 오류를 반환 하는 경우에 비트랜잭션 일괄 처리를 성공적으로 실행으로 간주 됩니다으로 하나 이상의 명령을 비트랜잭션 일괄 처리를 시작할 수는 **일괄 처리**  명령입니다.  
  
## <a name="using-serial-and-parallel-execution"></a>순차 및 병렬 실행 사용  
 사용할 수는 **일괄 처리** 실행할 포함 된 명령을 순차적으로 또는 병렬로 명령입니다. 에 포함 된 명령을 순차적으로 실행 되는 경우 다음 명령을 **일괄 처리** 명령에서 현재 실행 중인 명령을 시작할 수는 **일괄 처리** 명령이 완료 되어야 합니다. 여러 명령의 명령을 병렬로 실행 될 때에서 동시에 실행할 수 있습니다 합니다 **일괄 처리** 명령입니다.  
  
 명령을 병렬로 실행 하려면 병렬로 실행할 명령을 추가한 합니다 [병렬](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/parallel-element-xmla) 의 속성을 **일괄 처리** 명령 합니다. 현재 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 순차적인 연속만 실행할 수 있습니다 [프로세스](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla) 명령만 병렬로 합니다. 와 같은 다른 모든 XMLA 명령은 [Create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla) 또는 [Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)에 포함 된 합니다 **병렬** 속성 순차적으로 실행 됩니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 모든 실행 하려고 **프로세스** 명령에 포함 합니다 **병렬** 병렬로 속성 보장할 수 없습니다는 포함 된 모든 하지만 **프로세스** 명령을 병렬로 실행 될 수 있습니다. 각 인스턴스를 분석 **프로세스** 명령 인스턴스 명령을 병렬로 실행할 수 없음을 확인 하는 경우를 **프로세스** 명령을 순차적으로 실행 됩니다.  
  
> [!NOTE]  
>  명령을 병렬로 실행 하는 **트랜잭션** 특성을 **일괄 처리** 명령은 때문에 true로 설정 되어야 합니다 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 연결과 비트랜잭션 당 하나의 활성 트랜잭션만 지원 각 명령을 별도 트랜잭션에서 실행 하는 일괄 처리 합니다. 포함 하는 경우는 **병렬** 비트랜잭션 일괄 처리에서 속성에 오류가 발생 합니다.  
  
### <a name="limiting-parallel-execution"></a>병렬 실행 제한  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 만큼 실행 하려고 **프로세스** 인스턴스가 실행 되는 컴퓨터의 한도까지 최대한 병렬로 명령입니다. 동시 실행 수를 제한할 수 있습니다 **프로세스** 설정 하 여 명령을 **maxParallel** 특성을 **병렬** 속성을 나타내는 값을 최대 **프로세스** 병렬로 실행할 수 있는 명령입니다.  
  
 예를 들어, 한 **병렬** 속성에 나열 된 시퀀스에서 다음 명령을 포함 되어 있습니다.  
  
1.  **만들기**  
  
2.  **처리**  
  
3.  **Alter**  
  
4.  **처리**  
  
5.  **처리**  
  
6.  **처리**  
  
7.  **Delete**  
  
8.  **처리**  
  
9. **처리**  
  
 합니다 **maxParalle**특성은이 **병렬** 속성이 2로 설정 됩니다. 따라서 인스턴스는 이전 명령 목록을 다음 목록에 설명된 대로 실행합니다.  
  
-   명령 1이 있으므로 명령 1 순차적으로 실행 된 **만들기** 명령 및 전용 **프로세스** 명령을 병렬로 실행 될 수 있습니다.  
  
-   명령 1이 완료 된 후 2 명령이 순차적으로 실행 됩니다.  
  
-   명령은 3 2 명령이 완료 되 면 순차적으로 실행 합니다.  
  
-   명령 4 및 5 3 명령을 완료 한 후 병렬로 실행 됩니다. 명령 6도은 **프로세스** 명령, 명령 6은 때문에 명령 4 및 5와 함께 병렬로 실행할 수 없습니다는 **maxParallel** 속성이 2로 설정 됩니다.  
  
-   명령 4 및 5가 완료된 후 명령 6이 순차적으로 실행됩니다.  
  
-   명령 6이 완료된 후 명령 7이 순차적으로 실행됩니다.  
  
-   명령 7이 완료된 후 명령 8 및 9가 병렬로 실행됩니다.  
  
## <a name="using-the-batch-command-to-process-objects"></a>Batch 명령을 사용하여 개체 처리  
 합니다 **일괄 처리** 명령에는 여러 가지 선택적 속성 및 지원 하기 위해 특별히 포함 된 특성이 포함 된 여러 처리 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트:  
  
-   **ProcessAffectedObjects** 특성을 **일괄 처리** 명령은 인스턴스 또한의 결과로 다시 처리 해야 하는 개체를 처리 해야 하는지 여부를 나타냅니다는 **프로세스** 명령에 포함 된 합니다 **일괄 처리** 지정된 된 개체를 처리 합니다.  
  
-   [바인딩](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/bindings-element-xmla) 속성의 모든 사용 되는 아웃오브 라인 바인딩의 컬렉션을 포함 합니다 **프로세스** 명령에 **일괄 처리** 명령.  
  
-   [데이터 원본](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasource-element-xmla) 속성의 모든 사용 되는 데이터 원본에 대 한 아웃오브 라인 바인딩을 포함 합니다 **프로세스** 명령에 **일괄 처리** 명령입니다.  
  
-   [DataSourceView](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourceview-element-xmla) 속성의 모든 사용을 데이터 원본 뷰에 대 한 아웃오브 라인 바인딩을 포함 합니다 **프로세스** 명령에 **일괄 처리** 명령입니다.  
  
-   [ErrorConfiguration](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/errorconfiguration-element-xmla) 속성이 나타나는 방식을 지정 합니다 **일괄 처리** 모두에서 발생 한 오류를 처리 하는 명령 **프로세스** 합니다 에포함된명령을**일괄 처리** 명령입니다.  
  
    > [!IMPORTANT]  
    >  A **프로세스** 명령을 포함할 수 없습니다는 **바인딩**를 **DataSource**, **DataSourceView**, 또는 **ErrorConfiguration**  속성인 경우는 **프로세스** 명령에 포함 된를 **일괄 처리** 명령입니다. 에 대 한 이러한 속성을 지정 해야 하는 경우는 **프로세스** 명령에서의 해당 속성에 필요한 정보를 제공 합니다 **일괄 처리** 명령을 포함 하는 **프로세스** 명령입니다.  
  
## <a name="see-also"></a>관련 항목  
 [요소를 일괄 처리 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla)   
 [요소를 처리할 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)   
 [다차원 모델 처리&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Analysis Services에서 XMLA를 사용하여 개발](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
