---
title: 작업 전송 태스크 | Microsoft Docs
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
f1_keywords:
- sql13.dts.designer.transferjobstask.f1
- sql13.dts.designer.transferjobstask.general.f1
- sql13.dts.designer.transferjobstask.jobs.f1
helpviewer_keywords:
- Transfer Jobs task [Integration Services]
ms.assetid: 1bf33885-9c5b-47e4-a549-f5920b66a1de
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d86f9b5ddd0456faa92348f6bce99edc37bb029b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="transfer-jobs-task"></a>작업 전송 태스크
  작업 전송 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 사이에서 하나 이상의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에이전트 작업을 전송합니다.  
  
 작업 전송 태스크는 모든 작업 또는 지정된 작업만 전송하도록 구성할 수 있습니다. 또한 전송된 작업을 대상에서 활성화할지 여부를 나타낼 수 있습니다.  
  
 전송할 작업이 대상에 이미 있을 수 있습니다. 기존 태스크가 있을 경우 처리할 수 있는 방식은 다음과 같습니다.  
  
-   기존 작업을 덮어씁니다.  
  
-   중복 작업이 있으면 전송이 실패하도록 합니다.  
  
-   중복 작업을 건너뜁니다.  
  
 작업 전송 태스크는 실행 시 하나 또는 두 개의 SMO 연결 관리자를 사용하여 원본과 대상을 연결합니다. SMO 연결 관리자는 작업 전송 태스크와 별도로 구성된 후 작업 전송 태스크에서 참조됩니다. SMO 연결 관리자는 액세스할 서버 및 서버 액세스 시 사용할 인증 모드를 지정합니다. 자세한 내용은 [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md)을 참조하세요.  
  
## <a name="transferring-jobs-between-instances-of-sql-server"></a>SQL Server 인스턴스 간 작업 전송  
 작업 전송 태스크의 원본 및 대상으로는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용할 수 있습니다. 원본 또는 대상으로 사용하는 버전에 대한 제한은 없습니다.  
  
## <a name="events"></a>이벤트  
 작업 전송 태스크는 전송된 작업 수를 보고하는 정보 이벤트와 작업을 덮어씀을 알리는 경고 이벤트를 생성합니다. 태스크는 작업 전송의 진행률을 보고하지 않으며 0% 및 100%(완료)만 보고합니다.  
  
## <a name="execution-value"></a>실행 값  
 태스크의 **ExecutionValue** 속성에 정의된 실행 값은 전송된 작업 수를 반환합니다. 사용자 정의 변수를 작업 전송 태스크의 **ExecValueVariable** 속성에 할당하여 작업 전송에 대한 정보를 패키지에 있는 다른 개체에서 사용할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md) 및 [패키지에서 변수 사용](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)을 참조하세요.  
  
## <a name="log-entries"></a>로그 항목  
 작업 전송 태스크는 다음과 같은 사용자 지정 로그 항목을 포함합니다.  
  
-   TransferJobsTaskStarTransferringObjects - 이 로그 항목은 전송이 시작되었음을 보고합니다. 로그 항목에 시작 시간이 포함됩니다.  
  
-   TransferJobsTaskFinishedTransferringObjects - 이 로그 항목은 전송이 완료되었음을 보고합니다. 로그 항목에 종료 시간이 포함됩니다.  
  
 이외에 **OnInformation** 이벤트의 로그 항목은 전송된 작업 수를 보고하며 **OnWarning** 이벤트의 로그 항목은 덮어쓴 각 대상 작업에 대해 기록됩니다.  
  
## <a name="security-and-permissions"></a>보안 및 사용 권한  
 작업을 전송하려면 사용자는 sysadmin 고정 서버 역할의 멤버이거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 원본 및 대상 인스턴스 모두에 있는 msdb 데이터베이스의 고정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에이전트 고정 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="configuration-of-the-transfer-jobs-task"></a>작업 전송 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [식 페이지](../../integration-services/expressions/expressions-page.md)  
  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법은 다음 항목을 참조하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferJobsTask.TransferJobsTask>  
  
## <a name="related-tasks"></a>관련 작업  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="transfer-jobs-task-editor-general-page"></a>작업 전송 태스크 편집기(일반 페이지)
  **작업 전송 태스크 편집기** 대화 상자의 **일반** 페이지를 사용하여 작업 전송 태스크의 이름을 지정하고 해당 태스크를 설명할 수 있습니다.  
  
> [!NOTE]  
>  대상 서버의 **sysadmin** 고정 서버 역할 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할 중 하나의 멤버만 대상 서버에서 작업을 만들 수 있습니다. 원본 서버의 작업에 액세스하려면 사용자는 최소한 원본 서버의 **SQLAgentUserRole** 고정 데이터베이스 역할의 멤버여야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할 및 해당 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)을 참조하세요.  
  
### <a name="options"></a>변수  
 **이름**  
 작업 전송 태스크에 사용할 고유 이름을 입력합니다. 이 이름은 태스크 아이콘에서 레이블로 사용됩니다.  
  
> [!NOTE]  
>  태스크 이름은 패키지 내에서 고유해야 합니다.  
  
 **설명**  
 작업 전송 태스크에 대한 설명을 입력합니다.  
  
## <a name="transfer-jobs-task-editor-jobs-page"></a>작업 전송 태스크 편집기(작업 페이지)
  **작업 전송 태스크 편집기** 대화 상자의 **작업** 페이지를 사용하여 하나 이상의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 한 인스턴스에서 다른 인스턴스로 복사하기 위한 속성을 지정할 수 있습니다.  
  
> [!NOTE]  
>  원본 서버의 작업에 액세스하려면 사용자가 적어도 서버에서 **SQLAgentUserRole** 고정 데이터베이스 역할의 멤버여야 합니다. 대상 서버에 작업을 만들려면 사용자가 **sysadmin** 고정 서버 역할의 멤버이거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할 중 하나여야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할 및 해당 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)을 참조하세요.  
  
### <a name="options"></a>변수  
 **SourceConnection**  
 목록에서 SMO 연결 관리자를 선택하거나 **\<새 연결...>** 을 클릭하여 원본 서버에 대한 새 연결을 만듭니다.  
  
 **DestinationConnection**  
 목록에서 SMO 연결 관리자를 선택하거나 **\<새 연결...>** 을 클릭하여 대상 서버에 대한 새 연결을 만듭니다.  
  
 **TransferAllJobs**  
 원본 서버에서 대상 서버로 모든 SQL Server 에이전트 작업을 복사할지, 아니면 지정한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업만 복사할지를 선택합니다.  
  
 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**True**|모든 작업을 복사합니다.|  
|**False**|지정한 작업만 복사합니다.|  
  
 **JobsList**  
 복사할 작업을 선택하려면 찾아보기 단추 **(…)** 를 클릭합니다. 하나 이상의 작업을 선택해야 합니다.  
  
> [!NOTE]  
>  복사할 작업을 선택하기 전에 **SourceConnection** 을 지정합니다.  
  
 **TransferAllJobs** 를 **True** 로 설정하면 **JobsList**옵션을 사용할 수 없습니다.  
  
 **IfObjectExists**  
 태스크에서 대상 서버에 이미 있는 작업과 이름이 동일한 작업을 처리하는 방법을 선택합니다.  
  
 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**FailTask**|대상 서버에 이름이 동일한 작업이 이미 있는 경우 태스크가 실패합니다.|  
|**Overwrite**|대상 서버에 이름이 동일한 태스크가 있는 경우 이를 덮어씁니다.|  
|**Skip**|대상 서버에 이름이 동일한 태스크가 있는 경우 이를 건너뜁니다.|  
  
 **EnableJobsAtDestination**  
 대상 서버로 복사한 작업을 활성화할지 여부를 선택합니다.  
  
 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**True**|대상 서버에서 작업을 활성화합니다.|  
|**False**|대상 서버에서 작업을 비활성화합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 태스크](../../integration-services/control-flow/integration-services-tasks.md)   
 [제어 흐름](../../integration-services/control-flow/control-flow.md)  
  
  
