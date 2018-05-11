---
title: Integration Services 컨테이너 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SSIS containers
- containers [Integration Services]
- containers [Integration Services], about containers
- control flow [Integration Services], containers
- SQL Server Integration Services containers
ms.assetid: 1b725922-ec59-4a47-9d55-e079463058f3
caps.latest.revision: 48
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 20ce53ebc4de2694039019857264b5821f3c6f2d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="integration-services-containers"></a>Integration Services 컨테이너
  컨테이너는 패키지에 구조를 제공하고 태스크에 서비스를 제공하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 의 개체입니다. 패키지의 반복 제어 흐름을 지원하고 태스크와 컨테이너를 의미 있는 작업 단위로 그룹화합니다. 컨테이너는 태스크 외에도 다른 컨테이너를 포함할 수 있습니다.  
  
 패키지는 컨테이너를 다음 용도로 사용합니다.  
  
-   폴더의 파일, 스키마 또는 SMO( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects) 개체와 같은 컬렉션의 각 요소에 대해 태스크를 반복합니다. 예를 들어 패키지는 여러 파일에 있는 Transact-SQL 문을 실행할 수 있습니다.  
  
-   지정한 식이 **false**가 될 때까지 태스크를 반복합니다. 예를 들어 패키지는 하루에 한 번씩 매일 다른 전자 메일 메시지를 일주일 동안 7번 보낼 수 있습니다.  
  
-   하나의 단위로 성공하거나 실패해야 하는 태스크와 컨테이너를 그룹화합니다. 예를 들어 패키지는 데이터베이스 테이블에서 행을 삭제하고 추가하는 태스크를 그룹화한 다음 특정 태스크가 실패하면 모든 태스크를 커밋하거나 롤백할 수 있습니다.  
  
## <a name="container-types"></a>컨테이너 유형  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 패키지 빌드를 위해 4가지 컨테이너 유형을 제공합니다. 다음 표에서는 각 컨테이너 유형을 나열합니다.  
  
|컨테이너|Description|  
|---------------|-----------------|  
|[Foreach 루프 컨테이너](../../integration-services/control-flow/foreach-loop-container.md)|열거자를 사용하여 제어 흐름을 반복적으로 실행합니다.|  
|[For 루프 컨테이너](../../integration-services/control-flow/for-loop-container.md)|조건을 테스트하여 제어 흐름을 반복적으로 실행합니다.|  
|[시퀀스 컨테이너](../../integration-services/control-flow/sequence-container.md)|태스크와 컨테이너를 패키지 제어 흐름의 하위 집합인 제어 흐름으로 그룹화합니다.|  
|[태스크 호스트 컨테이너](../../integration-services/control-flow/task-host-container.md)|단일 태스크에 서비스를 제공합니다.|  
  
 패키지와 이벤트 처리기도 컨테이너 유형입니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 패키지](../../integration-services/integration-services-ssis-packages.md) 및 [Integration Services&#40;SSIS&#41; 이벤트 처리기](../../integration-services/integration-services-ssis-event-handlers.md)를 참조하세요.  
  
### <a name="summary-of-container-properties"></a>컨테이너 속성 요약  
 모든 컨테이너 유형에는 공통된 속성 집합이 있습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 제공되는 그래픽 도구를 사용하여 패키지를 만들 경우 속성 창에는 Foreach 루프, For 루프 및 시퀀스 컨테이너에 대한 다음 속성이 나열됩니다. 태스크 호스트 컨테이너 속성은 태스크 호스트가 캡슐화하는 태스크를 구성하는 과정의 일부로 구성됩니다. 이 태스크를 구성할 때 태스크 호스트 속성을 설정합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|**DelayValidation**|컨테이너의 유효성 검사가 런타임까지 지연되는지 여부를 나타내는 부울 값입니다. 이 속성의 기본값은 **False**입니다.<br /><br /> 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.DelayValidation%2A>가 될 때까지 태스크를 반복합니다.|  
|**설명**|컨테이너 설명입니다. 이 속성에는 문자열이 포함되지만 비워 둘 수 있습니다.<br /><br /> 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.Description%2A>가 될 때까지 태스크를 반복합니다.|  
|**사용 안함**|컨테이너가 실행되는지 여부를 나타내는 부울 값입니다. 이 속성의 기본값은 **False**입니다.<br /><br /> 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.Disable%2A>가 될 때까지 태스크를 반복합니다.|  
|**DisableEventHandlers**|컨테이너와 연결된 이벤트 처리기가 실행되는지 여부를 나타내는 부울 값입니다. 이 속성의 기본값은 **False**입니다.|  
|**FailPackageOnFailure**|컨테이너에서 오류가 발생하는 경우 패키지가 실패하는지 여부를 지정하는 부울 값입니다. 이 속성의 기본값은 **False**입니다.<br /><br /> 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.FailPackageOnFailure%2A>가 될 때까지 태스크를 반복합니다.|  
|**FailParentOnFailure**|컨테이너에서 오류가 발생하는 경우 부모 컨테이너가 실패하는지 여부를 지정하는 부울 값입니다. 이 속성의 기본값은 **False**입니다.<br /><br /> 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.FailParentOnFailure%2A>가 될 때까지 태스크를 반복합니다.|  
|**ForcedExecutionValue**|**ForceExecutionValue** 가 **True**로 설정된 경우 컨테이너의 선택적 실행 값을 포함하는 개체입니다. 이 속성의 기본값은 **0**입니다.<br /><br /> 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ForcedExecutionValue%2A>가 될 때까지 태스크를 반복합니다.|  
|**ForcedExecutionValueType**|**ForcedExecutionValue**의 데이터 형식입니다. 이 속성의 기본값은 **Int32**입니다.|  
|**ForceExecutionResult**|패키지 또는 컨테이너 강제 실행 결과를 지정하는 값입니다. 가능한 값은 **None**, **Success**, **Failure**및 **Completion**입니다. 이 속성의 기본값은 **None**입니다.<br /><br /> 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ForceExecutionResult%2A>가 될 때까지 태스크를 반복합니다.|  
|**ForceExecutionValue**|컨테이너의 선택적 실행 값에 특정 값이 포함되도록 강제해야 하는지 여부를 나타내는 부울 값입니다. 이 속성의 기본값은 **False**입니다.<br /><br /> 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ForceExecutionValue%2A>가 될 때까지 태스크를 반복합니다.|  
|**ID**|패키지를 만들 때 할당된 컨테이너 GUID입니다. 이 속성은 읽기 전용입니다.<br /><br /> <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.ID%2A>가 될 때까지 태스크를 반복합니다.|  
|**IsolationLevel**|컨테이너 트랜잭션의 격리 수준입니다. 가능한 값은 **Unspecified**, **Chaos**, **ReadUncommitted**, **ReadCommitted**, **RepeatableRead**, **Serializable**및 **Snapshot**입니다. 이 속성의 기본값은 **Serializable**입니다. 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.IsolationLevel%2A>가 될 때까지 태스크를 반복합니다.|  
|**LocaleID**|Microsoft Win32 로캘입니다. 이 속성의 기본값은 로컬 컴퓨터 운영 체제의 로캘입니다.<br /><br /> 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LocaleID%2A>가 될 때까지 태스크를 반복합니다.|  
|**LoggingMode**|컨테이너의 로깅 동작을 지정하는 값입니다. 가능한 값은 **Disabled**, **Enabled**및 **UseParentSetting**입니다. 이 속성의 기본값은 **UseParentSetting**입니다. 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode>가 될 때까지 태스크를 반복합니다.|  
|**MaximumErrorCount**|컨테이너 실행이 중지될 때까지 발생할 수 있는 최대 오류 수입니다. 이 속성의 기본값은 **1**입니다.<br /><br /> 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.MaximumErrorCount%2A>가 될 때까지 태스크를 반복합니다.|  
|**이름**|컨테이너의 이름입니다.<br /><br /> 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.Name%2A>가 될 때까지 태스크를 반복합니다.|  
|**TransactionOption**|컨테이너의 트랜잭션 참여 옵션입니다. 가능한 값은 **NotSupported**, **Supported**및 **Required**입니다. 이 속성의 기본값은 **Supported**입니다. 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.DTSTransactionOption>가 될 때까지 태스크를 반복합니다.|  
  
 프로그래밍 방식으로 구성할 경우 Foreach 루프, For 루프, 시퀀스 및 태스크 호스트 컨테이너에 사용할 수 있는 모든 속성에 대한 자세한 내용은 다음 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] API 항목을 참조하십시오.  
  
-   T:Microsoft.SqlServer.Dts.Runtime.ForEachLoop  
  
-   T:Microsoft.SqlServer.Dts.Runtime.ForLoop  
  
-   T:Microsoft.SqlServer.Dts.Runtime.Sequence  
  
-   T:Microsoft.SqlServer.Dts.Runtime.TaskHost  
  
## <a name="objects-that-extend-container-functionality"></a>컨테이너 기능을 확장하는 개체  
 컨테이너는 실행 파일과 선행 제약 조건으로 구성된 제어 흐름을 포함하며 이벤트 처리기와 변수를 사용할 수도 있습니다. 단, 태스크 호스트 컨테이너는 예외입니다. 태스크 호스트 컨테이너는 단일 태스크를 캡슐화하기 때문에 선행 제약 조건을 사용하지 않습니다.  
  
### <a name="executables"></a>실행 파일  
 실행 파일은 컨테이너 수준 태스크와 해당 컨테이너에 있는 모든 컨테이너를 참조합니다. 실행 파일은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 제공하는 태스크 및 컨테이너 중 하나이거나 사용자 지정 태스크일 수 있습니다. 자세한 내용은 [Integration Services Tasks](../../integration-services/control-flow/integration-services-tasks.md)을(를) 참조하세요.  
  
### <a name="precedence-constraints"></a>선행 제약 조건  
 선행 제약 조건은 부모 컨테이너가 같은 컨테이너와 태스크를 정렬된 제어 흐름으로 연결합니다. 자세한 내용은 [Precedence Constraints](../../integration-services/control-flow/precedence-constraints.md)을(를) 참조하세요.  
  
### <a name="event-handlers"></a>이벤트 처리기  
 컨테이너 수준의 이벤트 처리기는 컨테이너 또는 컨테이너에 포함된 개체에 의해 발생한 이벤트에 응답합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 이벤트 처리기](../../integration-services/integration-services-ssis-event-handlers.md)를 참조하세요.  
  
### <a name="variables"></a>변수  
 컨테이너에서 사용되는 변수는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 제공하는 컨테이너 수준의 시스템 변수와 해당 컨테이너가 사용하는 사용자 정의 변수를 포함합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md)을 참조하세요.  
  
## <a name="break-points"></a>중단점  
 컨테이너의 중단점을 설정할 때 중단 조건이 **컨테이너가 OnVariableValueChanged 이벤트를 받는 경우 중단**인 경우 컨테이너 범위의 변수를 정의합니다.  
  
## <a name="see-also"></a>참고 항목  
 [제어 흐름](../../integration-services/control-flow/control-flow.md)  
  
  
