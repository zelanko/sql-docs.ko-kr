---
title: master 저장 프로시저 전송 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transfermasterspstask.f1
- sql13.dts.designer.transferstoredprocedurestask.general.f1
- sql13.dts.designer.transferstoredprocedurestask.storedprocedures.f1
helpviewer_keywords:
- Transfer Master Stored Procedures task [Integration Services]
ms.assetid: 81702560-48a3-46d1-a469-e41304c7af8e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a84a11092ab1cab6e252d16d010f991d8a865c0f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47761711"
---
# <a name="transfer-master-stored-procedures-task"></a>Master 저장 프로시저 전송 태스크
  master 저장 프로시저 전송 태스크는 **인스턴스의** master [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]데이터베이스 간에 하나 이상의 사용자 정의 저장 프로시저를 전송합니다. **master** 데이터베이스에서 저장 프로시저를 전송하려면 프로시저 소유자가 dbo여야 합니다.  
  
 모든 저장 프로시저를 전송하거나 지정된 저장 프로시저만을 전송하도록 Master 저장 프로시저 전송 태스크를 구성할 수 있습니다. 이 태스크는 시스템 저장 프로시저를 복사하지 않습니다.  
  
 전송될 Master 저장 프로시저가 대상에 이미 존재할 수 있습니다. 다음 방식으로 기존의 저장 프로시저를 처리하도록 Master 저장 프로시저 전송 태스크를 구성할 수 있습니다.  
  
-   기존의 저장 프로시저를 덮어씁니다.  
  
-   중복 저장 프로시저가 있는 경우 태스크가 실패합니다.  
  
-   중복 저장 프로시저를 건너뜁니다.  
  
 Master 저장 프로시저 전송 태스크는 런타임에 두 개의 SMO 연결 관리자를 사용해 원본 서버와 대상 서버로 연결합니다. SMO 연결 관리자는 Master 저장 프로시저 전송 태스크와 별도로 구성되며 Master 저장 프로시저 전송 태스크에서 참조됩니다. SMO 연결 관리자는 액세스할 서버 및 사용할 인증 모드를 지정합니다. 자세한 내용은 [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md)을 참조하세요.  
  
## <a name="transferring-stored-procedures-between-instances-of-sql-server"></a>SQL Server 인스턴스 간 저장 프로시저 전송  
 Master 저장 프로시저 전송 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원본 및 대상을 지원합니다.  
  
## <a name="events"></a>이벤트  
 Master 저장 프로시저 전송 태스크는 전송된 저장 프로시저의 수를 보고하는 정보 이벤트 및 저장 프로시저를 덮어쓰는 경우 경고 이벤트를 발생시킵니다.  
  
 Master 저장 프로시저 전송 태스크는 로그인 전송의 진행 상황은 보고하지 않으며 0% 및 100% 완료만 보고합니다.  
  
## <a name="execution-value"></a>실행 값  
 태스크의 **ExecutionValue** 속성에 정의된 실행 값은 전송된 저장 프로시저의 수를 반환합니다. master 저장 프로시저 전송 태스크의 **ExecValueVariable** 속성에 사용자 정의 변수를 할당하면 패키지 내의 다른 개체에서 저장 프로시저 전송에 대한 정보를 사용할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md) 및 [패키지에서 변수 사용](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)을 참조하세요.  
  
## <a name="log-entries"></a>로그 항목  
 Master 저장 프로시저 전송 태스크는 다음 사용자 지정 로그 항목을 포함합니다.  
  
-   TransferStoredProceduresTaskStartTransferringObjects  이 로그 항목은 전송이 시작되었음을 보고합니다. 로그 항목에 시작 시간이 포함됩니다.  
  
-   TransferSStoredProceduresTaskFinishedTransferringObjects  이 로그 항목은 전송이 완료되었음을 보고합니다. 로그 항목에 종료 시간이 포함됩니다.  
  
 또한 **OnInformation** 이벤트 로그 항목은 전송된 저장 프로시저의 수를 보고하며 대상의 저장 프로시저를 덮어쓸 때마다 **OnWarning** 이벤트 로그 항목이 기록됩니다.  
  
## <a name="security-and-permissions"></a>보안 및 사용 권한  
 사용자는 원본에서 **master** 데이터베이스의 저장 프로시저 목록을 볼 수 있는 권한이 있어야 하며 sysadmin 서버 역할의 멤버이거나 대상 서버의 **master** 데이터베이스에서 저장 프로시저를 만들 수 있는 권한이 있어야 합니다.  
  
## <a name="configuration-of-the-transfer-master-stored-procedures-task"></a>Master 저장 프로시저 전송 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [식 페이지](../../integration-services/expressions/expressions-page.md)  
  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferStoredProceduresTask.TransferStoredProceduresTask>  
  
### <a name="configuring-the-transfer-master-stored-procedures-task-programmatically"></a>태스크 프로그래밍 방식으로 Master 저장 프로시저 전송 구성  
  
## <a name="related-tasks"></a>관련 작업  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="transfer-master-stored-procedures-task-editor-general-page"></a>master 저장 프로시저 전송 태스크 편집기(일반 페이지)
  **master 저장 프로시저 전송 태스크 편집기** 대화 상자의 **일반** 페이지를 사용하여 master 저장 프로시저 전송 태스크의 이름을 지정하고 해당 태스크를 설명할 수 있습니다.  
  
> [!NOTE]  
>  이 태스크는 **dbo** 소유의 사용자 정의 저장 프로시저만 원본 서버의 **master** 데이터베이스에서 대상 서버의 **master** 데이터베이스로 전송합니다. 대상 서버의 **master** 데이터베이스에서 CREATE PROCEDURE 권한을 부여받았거나 대상 서버에서 **sysadmin** 고정 서버 역할의 멤버인 사용자만 해당 데이터베이스에 저장 프로시저를 만들 수 있습니다.  
  
### <a name="options"></a>Options  
 **이름**  
 master 저장 프로시저 전송 태스크에 사용할 고유 이름을 제공합니다. 이 이름은 태스크 아이콘에서 레이블로 사용됩니다.  
  
> [!NOTE]  
>  태스크 이름은 패키지 내에서 고유해야 합니다.  
  
 **설명**  
 master 저장 프로시저 전송 태스크에 대한 설명을 입력합니다.  
  
## <a name="transfer-master-stored-procedures-task-editor-stored-procedures-page"></a>master 저장 프로시저 전송 태스크 편집기(저장 프로시저 페이지)
  **master 저장 프로시저 전송 태스크 편집기** 대화 상자의 **저장 프로시저** 페이지를 사용하여 하나 이상의 사용자 정의 저장 프로시저를 **인스턴스의** master [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 다른 **인스턴스의** master [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]데이터베이스로 복사하기 위한 속성을 지정할 수 있습니다.  
  
> [!NOTE]  
>  이 태스크는 **dbo** 소유의 사용자 정의 저장 프로시저만 원본 서버의 **master** 데이터베이스에서 대상 서버의 **master** 데이터베이스로 전송합니다. 대상 서버의 **master** 데이터베이스에서 CREATE PROCEDURE 권한을 부여받았거나 대상 서버에서 **sysadmin** 고정 서버 역할의 멤버인 사용자만 해당 데이터베이스에 저장 프로시저를 만들 수 있습니다.  
  
### <a name="options"></a>Options  
 **SourceConnection**  
 목록에서 SMO 연결 관리자를 선택하거나 **\<새 연결...>** 을 클릭하여 원본 서버에 대한 새 연결을 만듭니다.  
  
 **DestinationConnection**  
 목록에서 SMO 연결 관리자를 선택하거나 **\<새 연결...>** 을 클릭하여 대상 서버에 대한 새 연결을 만듭니다.  
  
 **IfObjectExists**  
 대상 서버의 **master** 데이터베이스에 이미 있는 같은 이름의 사용자 정의 저장 프로시저를 태스크에서 처리하는 방법을 선택합니다.  
  
 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**FailTask**|대상 서버의 **master** 데이터베이스에 같은 이름의 저장 프로시저가 이미 있는 경우 태스크가 실패합니다.|  
|**Overwrite**|대상 서버의 **master** 데이터베이스에 있는 같은 이름의 저장 프로시저를 덮어씁니다.|  
|**Skip**|대상 서버의 **master** 데이터베이스에 있는 같은 이름의 저장 프로시저를 건너뜁니다.|  
  
 **TransferAllStoredProcedures**  
 원본 서버의 **master** 데이터베이스에 있는 모든 사용자 정의 저장 프로시저를 대상 서버로 복사할지 여부를 선택합니다.  
  
|값|설명|  
|-----------|-----------------|  
|**True**|**master** 데이터베이스의 모든 사용자 정의 저장 프로시저를 복사합니다.|  
|**False**|지정한 저장 프로시저만 복사합니다.|  
  
 **StoredProceduresList**  
 원본 서버의 **master** 데이터베이스에서 대상 **master** 데이터베이스로 복사할 사용자 정의 저장 프로시저를 선택합니다. 이 옵션은 **TransferAllStoredProcedures** 를 **False**로 설정한 경우에만 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 개체 전송 태스크](../../integration-services/control-flow/transfer-sql-server-objects-task.md)   
 [Integration Services 태스크](../../integration-services/control-flow/integration-services-tasks.md)   
 [제어 흐름](../../integration-services/control-flow/control-flow.md)  
  
  
