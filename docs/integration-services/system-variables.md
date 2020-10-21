---
description: 시스템 변수
title: 시스템 변수 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], variables
- tasks [Integration Services], variables
- system variables [Integration Services]
- event handlers [Integration Services], variables
- variables [Integration Services], system
ms.assetid: efecd0d4-1489-4eba-a8fe-275d647058b8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cf44509a479e66175d89c38c42595e418dc6c750
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192409"
---
# <a name="system-variables"></a>시스템 변수

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에서는 런타임 패키지 및 해당 개체에 대한 정보가 저장되는 일련의 시스템 변수를 제공합니다. 이러한 변수를 식 및 속성 식에서 사용하여 패키지, 컨테이너, 태스크 및 이벤트 처리기를 사용자 지정할 수 있습니다.  
  
 SQL 실행 태스크에서 변수를 매개 변수에 매핑하는 데 사용되는 매개 변수 바인딩에 시스템 변수와 사용자 정의 변수를 포함한 모든 변수를 사용할 수 있습니다.  
  
## <a name="system-variables-for-packages"></a>패키지의 시스템 변수  
 다음 표에서는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 패키지에 대해 제공하는 시스템 변수에 대해 설명합니다.  
  
|시스템 변수|데이터 형식|Description|  
|---------------------|---------------|-----------------|  
|**CancelEvent**|Int32|태스크 실행을 중지해야 함을 나타내기 위해 태스크가 표시할 수 있는 Windows 이벤트 개체에 대한 핸들입니다.|  
|**ContainerStartTime**|DateTime|컨테이너의 시작 시간입니다.|  
|**CreationDate**|DateTime|패키지를 만든 날짜입니다.|  
|**CreatorComputerName**|String|패키지를 만든 컴퓨터입니다.|  
|**CreatorName**|String|패키지를 만든 사용자의 이름입니다.|  
|**ExecutionInstanceGUID**|String|실행 중인 패키지의 고유 식별자입니다.|  
|**FailedConfigurations**|String|실패한 패키지 구성 이름입니다.|  
|**IgnoreConfigurationsOnLoad**|부울|패키지를 로드할 때 패키지 구성을 무시할지 여부를 지정합니다.|  
|**InteractiveMode**|부울|패키지가 대화형 모드에서 실행 중인지 여부를 나타냅니다. [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 패키지를 실행 중인 경우 이 속성은 **True**로 설정됩니다. **DTExec** 명령 프롬프트 유틸리티를 사용하여 패키지를 실행 중인 경우 이 속성은 **False**로 설정됩니다.|  
|**LocaleId**|Int32|패키지에서 사용되는 로캘입니다.|  
|**MachineName**|String|패키지가 실행 중인 컴퓨터 이름입니다.|  
|**OfflineMode**|부울|패키지가 오프라인 모드인지 여부를 나타냅니다. 오프라인 모드에서는 데이터 원본에 연결하지 않습니다.|  
|**PackageID**|String|패키지의 고유 식별자입니다.|  
|**PackageName**|String|패키지의 이름입니다.|  
|**StartTime**|DateTime|패키지 실행을 시작한 시간입니다.|  
|**ServerExecutionID**|Int64|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버에서 실행되는 패키지의 실행 ID입니다.<br /><br /> 기본값은 영입니다. 이 값은 패키지가 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버에서 ISServerExec에 의해 실행되는 경우에만 변경됩니다. 자식 패키지가 있으면 값이 부모 패키지에서 자식 패키지로 전달됩니다.|  
|**UserName**|String|패키지를 시작한 사용자의 계정입니다. 사용자 이름은 도메인 이름에 의해 한정됩니다.|  
|**VersionBuild**|Int32|패키지 버전입니다.|  
|**VersionComment**|String|패키지 버전에 대한 설명입니다.|  
|**VersionGUID**|String|버전의 고유 식별자입니다.|  
|**VersionMajor**|Int32|패키지의 주 버전입니다.|  
|**VersionMinor**|Int32|패키지의 부 버전입니다.|  
  
## <a name="system-variables-for-containers"></a>컨테이너의 시스템 변수  
 다음 표에서는 For 루프, Foreach 루프 및 시퀀스 컨테이너에 대해 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 제공하는 시스템 변수에 대해 설명합니다.  
  
|시스템 변수|데이터 형식|Description|컨테이너|  
|---------------------|---------------|-----------------|---------------|  
|**LocaleId**|Int32|컨테이너에서 사용되는 로캘입니다.|For 루프 컨테이너<br /><br /> Foreach 루프 컨테이너<br /><br /> 시퀀스 컨테이너|  
  
## <a name="system-variables-for-tasks"></a>태스크의 시스템 변수  
 다음 표에서는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 태스크에 대해 제공하는 시스템 변수에 대해 설명합니다.  
  
|시스템 변수|데이터 형식|Description|  
|---------------------|---------------|-----------------|  
|**CreationName**|String|작업의 이름입니다.|  
|**LocaleId**|Int32|태스크에서 사용되는 로캘입니다.|  
|**TaskID**|String|태스크의 고유 식별자입니다.|  
|**TaskName**|String|태스크의 이름입니다.|  
|**TaskTransactionOption**|Int32|태스크에서 사용되는 트랜잭션 옵션입니다.|  
  
## <a name="system-variables-for-event-handlers"></a>이벤트 처리기의 시스템 변수  
 다음 표에서는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 이벤트 처리기에 대해 제공하는 시스템 변수에 대해 설명합니다. 일부 변수는 특정 이벤트 처리기에서만 사용할 수 있습니다.  
  
|시스템 변수|데이터 형식|Description|이벤트 처리기|  
|---------------------|---------------|-----------------|-------------------|  
|**취소**|부울|오류, 경고 또는 쿼리 취소가 발생할 때 이벤트 처리기 실행이 중지되는지 여부를 나타냅니다.|OnError 이벤트 처리기<br /><br /> OnWarning 이벤트 처리기<br /><br /> OnQueryCancel 이벤트 처리기|  
|**ErrorCode**|Int32|오류 식별자입니다.|OnError 이벤트 처리기<br /><br /> OnInformation 이벤트 처리기<br /><br /> OnWarning 이벤트 처리기|  
|**ErrorDescription**|String|오류에 대한 설명입니다.|OnError 이벤트 처리기<br /><br /> OnInformation 이벤트 처리기<br /><br /> OnWarning 이벤트 처리기|  
|**ExecutionStatus**|부울|현재 실행 상태입니다.|OnExecStatusChanged 이벤트 처리기|  
|**ExecutionValue**|DBNull|실행 값입니다.|OnTaskFailed 이벤트 처리기|  
|**LocaleId**|Int32|이벤트 처리기에서 사용되는 로캘입니다.|모든 이벤트 처리기|  
|**PercentComplete**|Int32|완료된 작업의 백분율입니다.|OnProgress 이벤트 처리기|  
|**ProgressCountHigh**|Int32|OnProgress 이벤트에 의해 처리된 전체 작업 개수를 나타내는 64비트 값의 상위 부분입니다.|OnProgress 이벤트 처리기|  
|**ProgressCountLow**|Int32|OnProgress 이벤트에 의해 처리된 전체 작업 개수를 나타내는 64비트 값의 하위 부분입니다.|OnProgress 이벤트 처리기|  
|**ProgressDescription**|String|진행률에 대한 설명입니다.|OnProgress 이벤트 처리기|  
|**Propagate**|부울|이벤트가 상위 수준의 이벤트 처리기로 전달되는지 여부를 나타냅니다.<br /><br /> 참고: 패키지의 유효성을 검사하는 동안에는 **Propagate** 변수의 값이 무시됩니다. 자식 패키지에서 **Propagate** 를 **False** 로 설정해도 이벤트가 부모 패키지로 전달될 수 있습니다.|모든 이벤트 처리기|  
|**SourceDescription**|String|이벤트 처리기에서 이벤트를 발생시킨 실행 개체에 대한 설명입니다.|모든 이벤트 처리기|  
|**SourceID**|String|이벤트 처리기에서 이벤트를 발생시킨 실행 개체의 고유 식별자입니다.|모든 이벤트 처리기|  
|**SourceName**|String|이벤트 처리기에서 이벤트를 발생시킨 실행 개체의 이름입니다.|모든 이벤트 처리기|  
|**VariableDescription**|String|변수 설명입니다.|OnVariableValueChanged 이벤트 처리기|  
|**VariableID**|String|변수의 고유 식별자입니다.|OnVariableValueChanged 이벤트 처리기|  
  
## <a name="system-variables-in-parameter-bindings"></a>매개 변수 바인딩의 시스템 변수  
 패키지 실행 시 테이블의 시스템 변수 값을 저장하면 유용합니다. 예를 들어 테이블을 동적으로 만들고 이 테이블을 만든 패키지 실행 인스턴스의 GUID를 테이블 열에 쓰는 패키지가 있을 수 있습니다.  
  
 시스템 변수를 사용하여 SQL 실행 태스크에서 사용되는 SQL 문의 매개 변수에 매핑하는 경우 각 매개 변수 바인딩의 데이터 형식을 시스템 변수의 데이터 형식으로 설정해야 합니다. 그렇게 하지 않으면 시스템 변수 값이 올바르게 번역되지 않을 수 있습니다. 예를 들어 패키지의 실행 인스턴스에 대한 GUID를 나타내는 문자열을 포함하는 문자열 데이터 형식의 **ExecutionInstanceGUID** 시스템 변수를 GUID 데이터 형식의 매개 변수 바인딩에 사용하면 패키지 인스턴스의 GUID가 올바르게 번역되지 않습니다.  
  
 이 규칙은 사용자 정의 변수에도 적용됩니다. 그러나 시스템 변수 데이터 형식의 경우 변경할 수 없으므로 데이터 형식에 맞게 적절하게 사용해야 하는 반면 사용자 정의 데이터 형식은 보다 융통성이 높습니다. 매개 변수 바인딩에 사용되는 사용자 정의 변수는 일반적으로 매핑되는 매개 변수의 데이터 형식과 호환 가능한 데이터 형식으로 정의됩니다.  
  
## <a name="related-tasks"></a>관련 작업  
 [쿼리 매개 변수를 SQL 실행 태스크의 변수에 매핑](./control-flow/execute-sql-task.md)  
  
