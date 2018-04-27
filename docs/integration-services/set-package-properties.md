---
title: 패키지 속성 설정 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Integration Services packages, properties
- properties [Integration Services]
- checkpoints [Integration Services]
- execution properties [Integration Services]
- packages [Integration Services], properties
- identification properties [Integration Services]
- passwords [Integration Services]
- SSIS packages, properties
- transaction properties [Integration Services]
- updating package properties
- forced execution value properties [Integration Services]
- security properties [Integration Services]
- version properties [Integration Services]
- SQL Server Integration Services packages, properties
ms.assetid: 13f81c3e-2b18-4f83-b445-a2f4a2c560aa
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 89564adcf11f815413fefaeb2701431c37b898c4
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="set-package-properties"></a>패키지 속성 설정
  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 가 제공하는 그래픽 인터페이스를 사용하여 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 패키지를 만들 때는 속성 창에서 패키지 개체의 속성을 설정합니다.  
  
 **속성** 창에는 속성이 항목별 및 사전순으로 제공됩니다. **속성** 창을 항목별로 정렬하려면 항목별 아이콘을 클릭합니다.  
  
 항목별로 정렬되면 **속성** 창의 속성이 다음과 같은 항목에 따라 그룹화됩니다.  
  
-   [검사점](#Checkpoints)  
  
-   [실행](#Execution)  
  
-   [강제 실행 값](#ForcedExecutionValue)  
  
-   [ID](#Identification)  
  
-   [기타](#Misc)  
  
-   [보안](#Security)  
  
-   [트랜잭션](#Transactions)  
  
-   [버전](#Version)  
  
 **속성** 창에서 설정할 수 없는 추가 패키지 속성에 대한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.Package>를 참조하세요.  
  
### <a name="to-set-package-properties-in-the-properties-window"></a>속성 창에서 패키지 속성을 설정하려면  
  
-   [패키지의 속성 설정](http://msdn.microsoft.com/library/0d20346e-475c-412f-b3ff-7bce25242b7a)  
  
## <a name="properties-by-category"></a>항목별 속성  
 다음 표에서는 항목별 패키지 속성을 나열합니다.  
  
###  <a name="Checkpoints"></a> 검사점  
 이 항목의 속성을 사용하면 제어 흐름 시작부터 패키지를 다시 실행하는 대신 패키지 제어 흐름의 오류 발생 시점으로부터 패키지를 다시 시작할 수 있습니다. 자세한 내용은 [검사점을 사용하여 패키지 다시 시작](../integration-services/packages/restart-packages-by-using-checkpoints.md)을 참조하세요.  
  
|속성|Description|  
|--------------|-----------------|  
|**CheckpointFileName**|패키지를 다시 시작하도록 만드는 검사점 정보를 캡처하는 파일 이름입니다. 패키지가 성공적으로 종료되면 이 파일이 삭제됩니다.|  
|**CheckpointUsage**|패키지를 다시 시작할 수 있는 시점을 지정합니다. 가능한 값은 **Never**, **IfExists**및 **Always**입니다. 이 속성의 기본값은 **Never**이며 이 경우 패키지를 다시 시작할 수 없습니다. 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.DTSCheckpointUsage>를 참조하세요.|  
|**SaveCheckpoints**|패키지가 실행될 때 검사점 파일에 검사점이 기록되는지 여부를 지정합니다. 이 속성의 기본값은 **False**입니다.|  
  
> [!NOTE]  
>  dtexec의 **/CheckPointing on** 옵션은 패키지의 **SaveCheckpoints** 속성을 True로 설정하고 **CheckpointUsage** 속성을 Always로 설정하는 것과 같습니다. 자세한 내용은 [dtexec Utility](../integration-services/packages/dtexec-utility.md)를 참조하세요.  
  
###  <a name="Execution"></a> 실행  
 이 항목의 속성은 패키지 개체의 런타임 동작을 구성합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|**DelayValidation**|패키지가 실행될 때까지 패키지 유효성 검사를 지연할지 여부를 나타냅니다. 이 속성의 기본값은 **False**입니다.|  
|**사용 안함**|패키지가 비활성화되는지 여부를 나타냅니다. 이 속성의 기본값은 **False**입니다.|  
|**DisableEventHandlers**|패키지 이벤트 처리기가 실행되는지 여부를 지정합니다. 이 속성의 기본값은 **False**입니다.|  
|**FailPackageOnFailure**|패키지 구성 요소에서 오류가 발생하는 경우 패키지가 실패하는지 여부를 지정합니다. 이 속성의 유효한 값은 **False**가 유일합니다.|  
|**FailParentOnError**|자식 컨테이너에서 오류가 발생하는 경우 부모 컨테이너가 실패하는지 여부를 나타냅니다. 이 속성의 기본값은 **False**입니다.|  
|**MaxConcurrentExecutables**|패키지에서 동시에 실행할 수 있는 실행 파일 수입니다. 이 속성의 기본값은 **-1**이며 이 경우 한계가 없습니다.|  
|**MaximumErrorCount**|패키지 실행이 중지될 때까지 발생할 수 있는 최대 오류 수입니다. 이 속성의 기본값은 **1**입니다.|  
|**PackagePriorityClass**|패키지 스레드의 Win32 스레드 우선 순위 클래스입니다. 가능한 값은 **Default**, **AboveNormal**, **Normal**, **BelowNormal**및 **Idle**입니다. 이 속성의 기본값은 **Default**입니다. 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.DTSPriorityClass>를 참조하세요.|  
  
###  <a name="ForcedExecutionValue"></a> 강제 실행 값  
 이 범주의 속성은 패키지의 선택적 실행 값을 구성합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|**ForcedExecutionValue**|ForceExecutionValue가 **True**로 설정된 경우 패키지가 반환하는 선택적 실행 값을 지정하는 값입니다. 이 속성의 기본값은 **0**입니다.|  
|**ForcedExecutionValueType**|ForcedExecutionValue의 데이터 형식입니다. 이 속성의 기본값은 **Int32**입니다.|  
|**ForceExecutionValue**|컨테이너의 선택적 실행 값에 특정 값이 포함되도록 강제해야 하는지 여부를 나타내는 부울 값입니다. 이 속성의 기본값은 **False**입니다.|  
  
###  <a name="Identification"></a> ID  
 이 항목의 속성은 패키지의 고유 식별자 및 이름과 같은 정보를 제공합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|**CreationDate**|패키지를 만든 날짜입니다.|  
|**CreatorComputerName**|패키지를 만든 컴퓨터의 이름입니다.|  
|**CreatorName**|패키지를 만든 사용자의 이름입니다.|  
|**설명**|패키지 기능에 대한 설명입니다.|  
|**ID**|패키지를 만들 때 할당된 패키지 GUID입니다. 이 속성은 읽기 전용입니다. **ID** 속성의 새 임의 값을 생성하려면 드롭다운 목록에서 **\<새 ID 생성\>** 을 선택합니다.|  
|**이름**|패키지의 이름입니다.|  
|**PackageType**|패키지 유형입니다. 가능한 값은 **Default**, **DTSDesigner**, **DTSDesigner100**, **DTSWizard**, **SQLDBMaint**및 **SQLReplication**입니다. 이 속성의 기본값은 **Default**입니다. 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.DTSPackageType>를 참조하세요.|  
  
###  <a name="Misc"></a> 기타  
 이 항목의 속성은 패키지에서 사용하는 구성 및 식에 액세스하고 패키지의 로캘 및 로깅 모드에 대한 정보를 제공하는 데 사용됩니다. 자세한 내용은 [패키지에서 속성 식 사용](../integration-services/expressions/use-property-expressions-in-packages.md)을 참조하세요.  
  
|속성|Description|  
|--------------|-----------------|  
|**구성**|패키지에서 사용되는 구성 모음입니다. 패키지 구성을 보고 구성하려면 찾아보기 단추 **(…)** 를 클릭합니다.|  
|**식**|패키지 속성에 대한 식을 만들려면 찾아보기 단추 **(…)** 를 클릭합니다.<br /><br /> 속성 창에 나열된 속성뿐만 아니라 개체 모델에 포함되는 모든 패키지 속성에 대한 속성 식을 만들 수 있습니다.<br /><br /> 자세한 내용은 [패키지에서 속성 식 사용](../integration-services/expressions/use-property-expressions-in-packages.md)을 참조하세요.<br /><br /> 기존 속성 식을 보려면 **Expressions**를 확장합니다. 식을 수정하고 계산하려면 식 입력란에 있는 찾아보기 단추 **(…)** 를 클릭합니다.|  
|**ForceExecutionResult**|패키지의 실행 결과입니다. 가능한 값은 **None**, **Success**, **Failure**및 **Completion**입니다. 이 속성의 기본값은 **None**입니다. 자세한 내용은 T:Microsoft.SqlServer.Dts.Runtime.DTSForcedExecResult를 참조하세요.|  
|**LocaleId**|Microsoft Win32 로캘입니다. 이 속성의 기본값은 로컬 컴퓨터 운영 체제의 로캘입니다.|  
|**LoggingMode**|패키지의 로깅 동작을 지정하는 값입니다. 가능한 값은 **Disabled**, **Enabled**및 **UseParentSetting**입니다. 이 속성의 기본값은 **UseParentSetting**입니다. 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode>를 참조하세요.|  
|**OfflineMode**|패키지가 오프라인 모드인지 여부를 나타냅니다. 이 속성은 읽기 전용입니다. 이 속성은 프로젝트 수준에서 설정됩니다. 일반적으로 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너는 패키지에서 원본 및 대상과 연결된 메타데이터의 유효성을 검사하는 데 사용되는 각 데이터 원본에 연결을 시도합니다. 패키지를 열기 전이라도 **SSIS** 메뉴의 **오프라인으로 작업** 을 설정하면 데이터 원본을 사용할 수 없을 때 이러한 연결이 시도됨으로써 유효성 검사 오류가 발생하는 것을 방지할 수 있습니다. 또한 **오프라인으로 작업** 을 설정하여 디자이너에서의 작업 속도를 높이고, 패키지의 유효성을 검사하려는 경우에만 이 옵션을 해제할 수도 있습니다.|  
|**SuppressConfigurationWarnings**|구성에 의해 생성된 경고가 표시되지 않는지 여부를 나타냅니다. 이 속성의 기본값은 **False**입니다.|  
|**UpdateObjects**|새로운 버전을 사용할 수 있는 경우 패키지에 포함된 새로운 버전의 개체를 사용하도록 패키지가 업데이트되는지 여부를 나타냅니다. 예를 들어 이 속성이 **True**로 설정된 경우 대량 삽입 태스크를 포함하는 패키지는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 제공하는 새로운 버전의 대량 삽입 태스크를 사용하도록 업데이트됩니다. 이 속성의 기본값은 **False**입니다.|  
  
###  <a name="Security"></a> 보안  
 이 항목의 속성은 패키지의 보호 수준을 설정하는 데 사용됩니다. 자세한 내용은 [Access Control for Sensitive Data in Packages](../integration-services/security/access-control-for-sensitive-data-in-packages.md)을 참조하세요.  
  
|속성|Description|  
|--------------|-----------------|  
|**PackagePassword**|암호가 필요한 패키지 보호 수준(**EncryptSensitiveWithPassword** 및 **EncryptAllWithPassword**)에 대한 암호입니다.|  
|**ProtectionLevel**|패키지의 보호 수준입니다. 가능한 값은 **DontSaveSensitive**, **EncryptSensitiveWithUserKey**, **EncryptSensitiveWithPassword**, **EncryptAllWithPassword**및 **ServerStorage**입니다. 이 속성의 기본값은 **EncryptSensitiveWithUserKey**입니다. 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.DTSProtectionLevel>를 참조하세요.|  
  
###  <a name="Transactions"></a> 트랜잭션  
 이 항목의 속성은 격리 수준과 패키지의 트랜잭션 옵션을 구성합니다. 자세한 내용은 [Integration Services 트랜잭션](../integration-services/integration-services-transactions.md)을 참조하세요.  
  
|속성|Description|  
|--------------|-----------------|  
|**IsolationLevel**|패키지 트랜잭션의 격리 수준입니다. 가능한 값은 **Unspecified**, **Chaos**, **ReadUncommitted**, **ReadCommitted**, **RepeatableRead**, **Serializable**및 **Snapshot**입니다. 이 속성의 기본값은 **Serializable**입니다.<br /><br /> 참고: **IsolationLevel** 속성의 **Snapshot** 값은 패키지 트랜잭션에 사용할 수 없습니다. 따라서 **IsolationLevel** 속성으로는 패키지 트랜잭션의 격리 수준을 **Shapshot**으로 설정할 수 없습니다. 패키지 트랜잭션을 **Snapshot**으로 설정하려면 SQL 쿼리를 대신 사용해야 합니다. 자세한 내용은 [SET TRANSACTION ISOLATION LEVEL&#40;Transact-SQL&#41;](../t-sql/statements/set-transaction-isolation-level-transact-sql.md)을 참조하세요.<br /><br /> **IsolationLevel** 속성 값을 **TransactionOption** 로 설정한 경우에만 **Required**속성이 패키지 트랜잭션에 적용됩니다.<br /><br /> 다음과 같은 경우 자식 컨테이너에서 요청하는 **IsolationLevel** 속성 값이 무시됩니다.<br />자식 컨테이너의 **TransactionOption** 속성 값이 **Supported**일 경우<br />자식 컨테이너가 부모 컨테이너의 트랜잭션에 참여하는 경우<br /><br /> 컨테이너에서 요청하는 **IsolationLevel** 속성 값은 컨테이너가 새 트랜잭션을 시작할 때만 적용됩니다. 다음과 같은 경우 컨테이너가 새 트랜잭션을 시작합니다.<br />컨테이너의 **TransactionOption** 속성 값이 **Required**일 경우<br />부모가 트랜잭션을 시작하지 않은 경우<br /><br /> <br /><br /> 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.IsolationLevel%2A>를 참조하세요.|  
|**TransactionOption**|패키지의 트랜잭션 참여 옵션입니다. 가능한 값은 **NotSupported**, **Supported**및 **Required**입니다. 이 속성의 기본값은 **Supported**입니다. 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.DTSTransactionOption>를 참조하세요.|  
  
###  <a name="Version"></a> 버전  
 이 항목의 속성은 패키지 개체의 버전에 대한 정보를 제공합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|**VersionBuild**|패키지 빌드의 버전 번호입니다.|  
|**VersionComments**|패키지 버전에 대한 설명입니다.|  
|**VersionGUID**|패키지 버전의 GUID입니다. 이 속성은 읽기 전용입니다.|  
|**VersionMajor**|패키지의 최신 주 버전입니다.|  
|**VersionMinor**|패키지의 최신 부 버전입니다.|  

## <a name="set-package-properties-in-the-properties-window"></a>속성 창에서 패키지 속성 설정 
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 구성할 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  **솔루션 탐색기**에서 패키지를 두 번 클릭하여 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너로 열거나 마우스 오른쪽 단추로 클릭하고 **디자이너 보기**를 선택합니다.  
  
3.  **제어 흐름** 탭을 클릭한 후 다음 중 하나를 수행합니다.  
  
    -   제어 흐름 디자인 화면 배경의 아무 위치나 마우스 오른쪽 단추로 클릭한 후 **속성**을 클릭합니다.  
  
    -   **보기** 메뉴에서 **속성 창**을 클릭합니다.  
  
4.  **속성** 창에서 패키지 속성을 편집합니다.  
  
5.  **파일** 메뉴에서 **선택한 항목 저장** 을 클릭하여 업데이트된 패키지를 저장합니다.  
  
