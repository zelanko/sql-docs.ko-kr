---
title: 일괄 처리 작업 (XMLA) 수행 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6d8fc92672858886a3c770d485bc21f6eb9f8eaa
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="performing-batch-operations-xmla"></a>일괄 작업 수행(XMLA)
  사용할 수는 [일괄 처리](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) XML for Analysis (XMLA) 단일 XMLA를 사용 하는 여러 XMLA 명령을 실행 하려면 명령을 [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) 메서드. 에 포함 된 여러 명령을 실행할 수 있습니다는 **일괄 처리** 명령을 단일 트랜잭션으로 또는 각 명령에 대 한 개별 트랜잭션을, 차례 대로 또는 병렬로 합니다. 아웃오브 라인 바인딩 및 기타 속성을 지정할 수도 있습니다는 **일괄 처리** 여러 처리 명령을 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체입니다.  
  
## <a name="running-transactional-and-nontransactional-batch-commands"></a>트랜잭션 및 비트랜잭션 Batch 명령  
 **일괄 처리** 명령은 다음 두 가지 방법 중 하나에서 명령을 실행 합니다.  
  
 **트랜잭션**  
 경우는 **트랜잭션** 특성에는 **일괄 처리** 명령을 설정 되어 true로는 **일괄 처리** 명령 실행 명령에 포함 된 명령을 모두는 **일괄처리** 단일 트랜잭션 내에서 명령을-는 *트랜잭션* 일괄 처리 합니다.  
  
 트랜잭션 일괄 처리에서 실패 한 명령이 있으면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 모든 명령을 롤백한는 **일괄 처리** 실패 한 명령 이전에 실행 된 명령 및 **일괄 처리** 명령을 즉시 종료 합니다. 모든 명령에는 **일괄 처리** 아직 실행 하지 않은 명령이 실행 되지 않습니다. 후의 **일괄 처리** 명령이 종료 된 **일괄 처리** 명령이 실패 한 명령에 대해 발생 한 오류를 보고 합니다.  
  
 **비트랜잭션**  
 경우는 **트랜잭션** 특성이 false로 설정 되어는 **일괄 처리** 명령을 실행 하 여 포함 된 각 명령을 **일괄 처리** 별도 트랜잭션에서 명령을-는  *비트랜잭션* 일괄 처리 합니다. 비트랜잭션 일괄 처리에서 실패 한 명령이 있으면는 **일괄 처리** 명령은 계속 실패 한 명령 이후의 명령을 실행 합니다. 후는 **일괄 처리** 명령이 모든 명령을 실행 하려고 하는 **일괄 처리** 명령에는 **일괄 처리** 명령이 발생 한 오류를 보고 합니다.  
  
 에 포함 된 명령을 사용 하 여 반환 된 모든 결과 **일괄 처리** 명령에 포함 된 명령의 순서 대로 반환 되는 **일괄 처리** 명령입니다. 반환 된 결과 **일괄 처리** 명령 인지 여부에 따라 달라 집니다는 **일괄 처리** 트랜잭션인지 또는 비트랜잭션 명령입니다.  
  
> [!NOTE]  
>  경우는 **일괄 처리** 명령와 같은 출력을 반환 하지 않는 명령이 포함 되어는 [잠금](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md) 명령 및 있는지 명령이 성공적으로 실행 되는 **일괄 처리** 명령은 빈을 반환 합니다. [루트](../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) 결과 요소 내에서 요소입니다. 빈 **루트** 요소 각 명령이에 포함 된 한 **일괄 처리** 명령은 일치 하는 적절 한 **루트** 해당 명령의 결과 대 한 요소입니다.  
  
### <a name="returning-results-from-transactional-batch-results"></a>트랜잭션 일괄 처리 결과에서 결과 반환  
 전체 트랜잭션 일괄 처리 내에서 실행 된 명령의 결과 반환 되지 않습니다 **일괄 처리** 명령이 완료 되어야 합니다. 트랜잭션 일괄 처리 중 실패 이유는 명령이 전체 때문에 각 명령을 실행 한 후 결과 반환 하지는 **일괄 처리** 명령 및 포함 하는 모든 명령이 롤백됩니다. 모든 명령을 시작 하 고 성공적으로 실행 하는 경우는 [반환](../../analysis-services/xmla/xml-elements-properties/return-element-xmla.md) 의 요소는 [ExecuteResponse](../../analysis-services/xmla/xml-elements-objects-executeresponse.md) 요소에서 반환 되는 **Execute** 에 대 한 메서드는 **일괄 처리**  하나가 포함 된 명령 [결과](../../analysis-services/xmla/xml-elements-properties/results-element-xmla.md) 요소 하나를 포함 하는 요소를 **루트** 에 포함 된 각 성공적으로 실행된 명령에 대 한 요소는 **일괄처리** 명령입니다. 명령에 경우는 **일괄 처리** 명령을 시작할 수 없거나 완료 하지 못한는 **Execute** 에 대 한 SOAP 오류를 반환 하는 메서드는 **일괄 처리** 의 오류를 포함 하는 명령에서 실패 한 명령입니다.  
  
### <a name="returning-results-from-nontransactional-batch-results"></a>비트랜잭션 일괄 처리 결과에서 결과 반환  
 비트랜잭션 일과 처리 내에서 실행 된 명령의 결과에 포함 된 명령의 순서 대로 반환 됩니다는 **일괄 처리** 명령 각 명령에 의해 반환 되 고 있습니다. 경우에 포함 된 명령이 없습니다.는 **일괄 처리** 명령을 하나도 시작할 수 있습니다는 **Execute** 에 대 한 오류가 포함 된 SOAP 오류를 반환 하는 메서드는 **일괄 처리** 명령입니다. 하나 이상의 명령이 성공적으로 시작 되는 경우는 **반환** 의 요소는 **ExecuteResponse** 요소에서 반환 되는 **Execute** 에 대 한 메서드는 **일괄 처리**  하나가 포함 된 명령 **결과** 요소 하나를 포함 하는 요소를 **루트** 에 포함 된 각 명령에 대 한 요소는 **일괄 처리** 명령 . 비트랜잭션 일괄 처리에서 하나 이상의 명령을 시작할 수 없거나 완료 하지 못한 경우는 **루트** 실패 한 명령에 대 한 요소를 포함 한 [오류](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md) 오류를 설명 하는 요소입니다.  
  
> [!NOTE]  
>  비트랜잭션 일괄 처리에 포함 된 모든 명령의 결과에 오류를 반환 하는 경우에 비트랜잭션 일괄 처리는 성공적으로 실행으로 간주 됩니다 시작할 수 있는 비트랜잭션 일괄 처리에서 적어도 하나의 명령으로는 **일괄 처리**  명령입니다.  
  
## <a name="using-serial-and-parallel-execution"></a>순차 및 병렬 실행 사용  
 사용할 수는 **일괄 처리** 실행할 포함 된 명령을 순차적으로 또는 병렬로 명령입니다. 다음 명령에 포함 된 명령을 순차적으로 실행 되는 경우는 **일괄 처리** 명령에서 현재 실행 중인 명령을 시작할 수는 **일괄 처리** 명령이 완료 되어야 합니다. 명령을 병렬로 실행 될 때 여러 명령을 동시에 실행할 수는 **일괄 처리** 명령입니다.  
  
 동시에 실행 될 명령을 추가한 명령을 병렬로 실행 하는 [병렬](../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md) 속성의는 **일괄 처리** 명령입니다. 현재 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 순차적인 연속만 실행할 수 [프로세스](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) 명령만 병렬로 합니다. 와 같은 다른 모든 XMLA 명령은 [만들기](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md) 또는 [Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)에 포함 된는 **병렬** 속성 순차적으로 실행 됩니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 모두 실행 하려고 **프로세스** 에 포함 된 명령만 **병렬** 병렬로 속성 않을 수도 있는 포함 된 모든 있지만 **프로세스** 명령을 병렬로 실행 될 수 있습니다. 인스턴스를 각각 분석 **프로세스** 명령 인스턴스에서 명령을 병렬로 실행할 수 없습니다 결정 하는 경우는 **프로세스** 명령을 직렬으로 실행 됩니다.  
  
> [!NOTE]  
>  명령을 병렬로 실행 하는 **트랜잭션** 특성에는 **일괄 처리** 명령은 때문에 true로 설정 되어야 합니다 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 연결 및 비트랜잭션 당 하나의 활성 트랜잭션만 지원 각 명령을 별도의 트랜잭션에서 실행 일괄 처리입니다. 포함 하는 경우는 **병렬** 비트랜잭션 일괄 처리에서 속성, 오류가 발생 합니다.  
  
### <a name="limiting-parallel-execution"></a>병렬 실행 제한  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 만큼를 실행 하 려 **프로세스** 인스턴스가 실행 되는 컴퓨터의 제한까지 가능한 동시에 명령 합니다. 동시 실행 수를 제한할 수 **프로세스** 설정 하 여 명령을 **maxParallel** 특성에는 **병렬** 속성을 나타내는 값의 최대 개수 **프로세스** 병렬로 실행할 수 있는 명령입니다.  
  
 예를 들어 한 **병렬** 속성에 나열 된 시퀀스에서 다음 명령을 포함 합니다.  
  
1.  **만들기**  
  
2.  **처리**  
  
3.  **Alter**  
  
4.  **처리**  
  
5.  **처리**  
  
6.  **처리**  
  
7.  **Delete**  
  
8.  **처리**  
  
9. **처리**  
  
 **maxParalle**l 특성의 **병렬** 속성이 2로 설정 되어 있습니다. 따라서 인스턴스는 이전 명령 목록을 다음 목록에 설명된 대로 실행합니다.  
  
-   명령 1이 있으므로 명령 1이 순차적으로 실행 한 **만들기** 명령이 고 유일한 **프로세스** 명령을 병렬로 실행 될 수 있습니다.  
  
-   명령 1이 완료 된 후 명령 2 순차적으로 실행 합니다.  
  
-   2 명령이 완료 된 후 명령 3 순차적으로 실행 합니다.  
  
-   명령 4 및 5 3 명령을 완료 한 후 동시에 실행 합니다. 명령 6도 있지만 **프로세스** 명령, 명령 6은 때문에 명령 4 및 5와 병렬로 실행할 수 없습니다는 **maxParallel** 속성이 2로 설정 되어 있습니다.  
  
-   명령 4 및 5가 완료된 후 명령 6이 순차적으로 실행됩니다.  
  
-   명령 6이 완료된 후 명령 7이 순차적으로 실행됩니다.  
  
-   명령 7이 완료된 후 명령 8 및 9가 병렬로 실행됩니다.  
  
## <a name="using-the-batch-command-to-process-objects"></a>Batch 명령을 사용하여 개체 처리  
 **일괄 처리** 명령에는 여러 가지 선택적 속성 및 지원 하기 위해 특별히 포함 된 특성이 포함 된 다중 처리 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트:  
  
-   **ProcessAffectedObjects** 특성에는 **일괄 처리** 명령은 인스턴스 또한의 결과로 다시 처리 해야 하는 개체를 처리 해야 하는지 여부를 나타냅니다.는 **프로세스** 명령에 포함 된는 **일괄 처리** 명령 지정된 된 개체를 처리 합니다.  
  
-   [바인딩](../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md) 속성 모두에서 사용 하는 아웃오브 라인 바인딩의 컬렉션이 포함는 **프로세스** 의 명령은 **일괄 처리** 명령입니다.  
  
-   [DataSource](../../analysis-services/xmla/xml-elements-properties/datasource-element-xmla.md) 속성의 모든 사용 되는 데이터 원본에 대 한는 아웃오브 라인 바인딩이 포함는 **프로세스** 의 명령은 **일괄 처리** 명령입니다.  
  
-   [DataSourceView](../../analysis-services/xmla/xml-elements-properties/datasourceview-element-xmla.md) 속성 모두에서 사용 하는 데이터 원본 뷰는 아웃오브 라인 바인딩이 포함 되어는 **프로세스** 의 명령은 **일괄 처리** 명령입니다.  
  
-   [ErrorConfiguration](../../analysis-services/xmla/xml-elements-properties/errorconfiguration-element-xmla.md) 속성은 방법을 지정 하는 **일괄 처리** 모두에서 발생 한 오류를 처리 하는 명령 **프로세스** 는 에포함된명령을**일괄 처리** 명령입니다.  
  
    > [!IMPORTANT]  
    >  A **프로세스** 명령을 포함할 수 없습니다는 **바인딩**, **DataSource**, **DataSourceView**, 또는 **ErrorConfiguration**  속성을 하는 경우는 **프로세스** 명령에 포함 된 한 **일괄 처리** 명령입니다. 에 대 한 이러한 속성을 지정 해야 하는 경우는 **프로세스** 명령에서의 해당 속성에 필요한 정보를 제공 된 **일괄 처리** 명령을 포함 하는 **프로세스** 명령입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [일괄 처리 요소 & #40; XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)   
 [요소를 처리할 &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)   
 [다차원 모델 처리&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Analysis Services에서 XMLA를 사용 하 여 개발](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
