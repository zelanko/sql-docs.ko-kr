---
title: "데이터베이스 전송 태스크 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.transferdatabasetask.f1
- sql13.dts.designer.transferdatabasetask.general.f1
- sql13.dts.designer.transferdatabasetask.database.f1
- sql13.dts.designer.transferdatabasetask.sourcedbfiles.f1
- sql13.dts.designer.transferdatabasetask.destdbfiles.f1
helpviewer_keywords:
- Transfer Database task [Integration Services]
ms.assetid: b9a2e460-cdbc-458f-8df8-06b8b2de3d67
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 8806c102eaec2c2540374bfaddc33b76d8f6e584
ms.openlocfilehash: 29f66d1eeed7e2af0df962b62020169fb2095f6e
ms.contentlocale: ko-kr
ms.lasthandoff: 08/11/2017

---
# <a name="transfer-database-task"></a>데이터베이스 전송 태스크
  데이터베이스 전송 태스크는 두 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 간에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]데이터베이스를 전송합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체를 복사하여 전송하는 다른 태스크와 달리 데이터베이스 전송 태스크는 데이터베이스를 복사 또는 이동할 수 있습니다. 동일한 서버 내에서 데이터베이스를 복사하는 데도 전송 태스크를 사용할 수 있습니다.  
  
## <a name="offline-and-online-modes"></a>오프라인 및 온라인 모드  
 온라인 또는 오프라인 모드에서 데이터베이스를 전송할 수 있습니다. 온라인 모드를 사용하는 경우 데이터베이스는 연결된 상태를 유지하며 데이터베이스 개체를 복사하는 SMO(SQL Management Object)를 통해 전송됩니다. 오프라인 모드를 사용하는 경우 데이터베이스가 분리된 상태로 데이터베이스 파일을 복사 또는 이동하며 성공적으로 전송을 완료한 다음 대상에 데이터베이스를 연결합니다. 데이터베이스를 복사하면 복사가 완료될 때 자동으로 원본에 다시 연결됩니다. 오프라인 모드에서는 좀 더 빠르게 데이터베이스를 복사할 수 있지만 전송하는 동안 데이터베이스를 사용할 수 없습니다.  
  
 오프라인 모드를 사용하려면 데이터베이스 파일을 가진 대상 서버 및 원본 서버에 네트워크 파일 공유를 지정해야 합니다. 폴더를 공유하여 사용자가 액세스할 수 있는 경우 \\\computername\Program Files\myfolder\\구문을 사용하여 네트워크 공유를 참조할 수 있습니다. 그렇지 않으면 \\\computername\c$\Program Files\myfolder\\구문을 사용해야 합니다. 두 번째 구문을 사용하려면 원본 및 대상 네트워크 공유에 대한 쓰기 액세스가 필요합니다.  
  
## <a name="transfer-of-databases-between-versions-of-sql-server"></a>SQL Server 버전 간 데이터베이스 전송  
 데이터베이스 전송 태스크는 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전의 인스턴스 간에 데이터베이스를 전송할 수 있습니다.  
  
## <a name="events"></a>이벤트  
 데이터베이스 전송 태스크는 오류 메시지 전송의 진행 상황은 보고하지 않으며 0% 및 100% 완료만 보고합니다.  
  
## <a name="execution-value"></a>실행 값  
 다른 전송 태스크와 달리 데이터베이스 전송 태스크는 한 개의 데이터베이스만 전송할 수 있으므로 태스크의 **ExecutionValue** 속성에 정의된 실행 값은 1을 반환합니다.  
  
 데이터베이스 전송 태스크의 **ExecValueVariable** 속성에 사용자 정의 변수를 할당하면 패키지 내의 다른 개체에서 오류 메시지 전송에 대한 정보를 사용할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md) 및 [패키지에서 변수 사용](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)을 참조하세요.  
  
## <a name="log-entries"></a>로그 항목  
 데이터베이스 전송 태스크는 다음 사용자 지정 로그 항목을 포함합니다.  
  
-   SourceSQLServer    이 로그 항목은 원본 서버의 이름을 나열합니다.  
  
-   DestSQLServer    이 로그 항목은 대상 서버의 이름을 나열합니다.  
  
-   SourceDB    이 로그 항목은 전송된 데이터베이스의 이름을 나열합니다.  
  
 또한 대상 데이터베이스를 덮어쓰는 경우 **OnInformation** 이벤트에 대한 로그 항목이 기록됩니다.  
  
## <a name="security-and-permissions"></a>보안 및 사용 권한  
 오프라인 모드를 사용해 데이터베이스를 전송하려면 패키지를 실행하는 사용자가 sysadmin 서버 역할의 멤버여야 합니다.  
  
 온라인 모드를 사용해 데이터베이스를 전송하려면 패키지를 실행하는 사용자가 sysadmin 서버 역할의 멤버이거나 선택한 데이터베이스의 데이터베이스 소유자(dbo)여야 합니다.  
  
## <a name="configuration-of-the-transfer-database-task"></a>데이터베이스 전송 태스크 구성  
 데이터베이스 전송이 실패하는 경우 태스크가 원본 데이터베이스에 다시 연결할지 여부를 지정할 수 있습니다.  
  
 동일한 이름의 대상 데이터베이스를 덮어쓰고 대상 데이터베이스를 대체할 수 있도록 데이터베이스 전송 태스크를 구성할 수 있습니다.  
  
 전송 과정의 일부로 원본 데이터베이스의 이름을 바꿀 수 있습니다. 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 이미 같은 이름의 데이터베이스가 있는 경우 원본 데이터베이스의 이름을 변경하여 데이터베이스를 전송할 수 있습니다. 그러나 같은 이름의 데이터베이스 파일이 대상에 있는 경우에는 태스크가 실패하므로 데이터베이스 파일의 이름은 반드시 달라야 합니다.  
  
 데이터베이스를 복사할 경우 데이터베이스는 대상 서버에 있는 **model** 데이터베이스의 크기보다 작을 수 없습니다. 복사할 데이터베이스의 크기를 늘리거나 **model**의 크기를 줄일 수 있습니다.  
  
 데이터베이스 전송 태스크는 런타임에 한 개 또는 두 개의 SMO 연결 관리자를 사용해 원본 서버 및 대상 서버에 연결합니다. 동일한 서버에 데이터베이스 복사본을 만드는 경우 하나의 SMO 연결 관리자만 필요합니다. SMO 연결 관리자는 데이터베이스 전송 태스크와 별도로 구성된 후 데이터베이스 전송 태스크에서 참조됩니다. SMO 연결 관리자는 태스크가 서버에 액세스할 때 사용할 서버 및 인증 모드를 지정합니다. 자세한 내용은 [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md)을 참조하세요.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [식 페이지](../../integration-services/expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-transfer-database-task"></a>데이터베이스 전송 태스크의 프로그래밍 방식 구성  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferDatabaseTask.TransferDatabaseTask>  
  
## <a name="transfer-database-task-editor-general-page"></a>데이터베이스 전송 태스크 편집기(일반 페이지)
  **데이터베이스 전송 태스크 편집기** 대화 상자의 **일반** 페이지를 사용하여 데이터베이스 전송 태스크를 명명 및 설명할 수 있습니다. 데이터베이스 전송 태스크에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 두 인스턴스 간에 복사 또는 이동합니다. 동일한 서버 내에서 데이터베이스를 복사하는 데도 전송 태스크를 사용할 수 있습니다.   
  
### <a name="options"></a>옵션  
 **이름**  
 데이터베이스 전송 태스크에 사용할 고유 이름을 입력합니다. 이 이름은 태스크 아이콘에서 레이블로 사용됩니다.  
  
> [!NOTE]  
>  태스크 이름은 패키지 내에서 고유해야 합니다.  
  
 **Description**  
 데이터베이스 전송 태스크에 대한 설명을 입력합니다.  
  
## <a name="transfer-database-task-editor-databases-page"></a>데이터베이스 전송 태스크 편집기(데이터베이스 페이지)
  **데이터베이스 전송 태스크 편집기** 대화 상자의 **데이터베이스** 페이지를 사용하여 데이터베이스 전송 태스크와 관련된 원본 및 대상 데이터베이스의 속성을 지정할 수 있습니다. 데이터베이스 전송 태스크에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 두 인스턴스 간에 복사 또는 이동합니다. 동일한 서버 내에서 데이터베이스를 복사하는 데도 전송 태스크를 사용할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **SourceConnection**  
 목록에서 SMO 연결 관리자를 선택 하거나 클릭  **\<새 연결... >** 원본 서버에 새 연결을 만듭니다.  
  
 **DestinationConnection**  
 목록에서 SMO 연결 관리자를 선택 하거나 클릭  **\<새 연결... >** 대상 서버에 새 연결을 만듭니다.  
  
 **DestinationDatabaseName**  
 대상 서버에 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 이름을 지정합니다.  
  
 이 필드를 원본 데이터베이스 이름으로 자동으로 채우려면 먼저 **SourceConnection** 및 **SourceDatabaseName** 을 지정합니다.  
  
 대상 서버에 있는 데이터베이스의 이름을 바꾸려면 이 필드에 새 이름을 입력합니다.  
  
 **DestinationDatabaseFiles**  
 대상 서버에 있는 데이터베이스 파일의 이름 및 위치를 지정합니다.  
  
 이 필드를 원본 데이터베이스 파일 이름 및 위치로 자동으로 채우려면 먼저 **SourceConnection**, **SourceDatabaseName**및 **SourceDatabaseFiles** 를 지정합니다.  
  
 데이터베이스 파일의 이름을 바꾸거나 대상 서버에 새 위치를 지정하려면 이 필드를 원본 데이터베이스 정보로 채운 다음 찾아보기 단추를 클릭합니다. **대상 데이터베이스 파일** 대화 상자에서 **대상 파일**, **대상 폴더**또는 **네트워크 파일 공유**를 편집합니다.  
  
> [!NOTE]  
>  찾아보기 단추를 사용하여 데이터베이스 파일을 찾으면 해당 파일 위치가 로컬 드라이브 표기법을 사용하여 입력됩니다(예: c:\\). 이는 컴퓨터 이름 및 공유 이름과 함께 네트워크 공유 표기법으로 바꾸어야 합니다. 기본 관리 공유를 사용하는 경우 $ 표기법을 사용하고 공유에 대한 관리 액세스가 있어야 합니다.  
  
 **DestinationOverwrite**  
 대상 서버에 있는 데이터베이스를 덮어쓸지 여부를 지정합니다.  
  
 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**True**|대상 서버 데이터베이스를 덮어씁니다.|  
|**False**|대상 서버 데이터베이스를 덮어쓰지 않습니다.|  
  
> [!CAUTION]  
>  **DestinationOverwrite** 에 대해 **True**를 지정하면 대상 서버 데이터베이스의 데이터를 덮어쓰며 이로 인해 데이터가 손실될 수 있습니다. 이를 방지하려면 데이터베이스 전송 태스크를 실행하기 전에 대상 서버 데이터베이스를 다른 위치에 백업합니다.  
  
 **동작**  
 데이터베이스를 대상 서버로 복사하려면 **Copy** , 이동하려면 **Move** 를 지정합니다.  
  
 **메서드**  
 원본 서버의 데이터베이스가 온라인 모드에 있을 때 태스크를 실행할지, 아니면 오프라인 모드에 있을 때 실행할지를 지정합니다.  
  
 오프라인 모드를 사용하여 데이터베이스를 전송하려면 패키지를 실행하는 사용자가 **sysadmin** 고정 서버 역할의 멤버여야 합니다.  
  
 온라인 모드를 사용하여 데이터베이스를 전송하려면 패키지를 실행하는 사용자가 **sysadmin** 고정 서버 역할의 멤버이거나 선택한 데이터베이스의 데이터베이스 소유자(**dbo**)여야 합니다.  
  
 **SourceDatabaseName**  
 복사 또는 이동할 데이터베이스의 이름을 선택합니다.  
  
 **SourceDatabaseFiles**  
 데이터베이스 파일을 선택하려면 찾아보기 단추를 클릭합니다.  
  
 **ReattachSourceDatabase**  
 오류 발생 시 원본 데이터베이스를 다시 연결할지 여부를 지정합니다.  
  
 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**True**|원본 데이터베이스를 다시 연결합니다.|  
|**False**|원본 데이터베이스를 다시 연결하지 않습니다.|  

## <a name="source-database-files"></a>원본 데이터베이스 파일
  **원본 데이터베이스 파일** 대화 상자를 사용하여 원본 서버의 데이터베이스 파일 이름 및 위치를 보거나 데이터베이스 전송 태스크에 대한 네트워크 파일 공유 위치를 지정할 수 있습니다.   
  
 이 대화 상자를 원본 서버의 데이터베이스 파일 이름 및 위치로 채우려면 먼저 **데이터베이스 전송 태스크 편집기** 대화 상자의 **데이터베이스** 페이지에서 **SourceConnection** 및 **SourceDatabaseName** 을 지정합니다.  
  
### <a name="options"></a>옵션  
 **원본 파일**  
 전송할 원본 서버의 데이터베이스 파일 이름입니다. **원본 파일** 은 읽기 전용입니다.  
  
 **원본 폴더**  
 전송할 데이터베이스 파일이 있는 원본 서버의 폴더입니다. **원본 폴더** 는 읽기 전용입니다.  
  
 **네트워크 파일 공유**  
 데이터베이스 파일을 전송할 원본 서버의 네트워크 공유 폴더입니다. 오프라인 모드에서 데이터베이스를 전송할 때는 **데이터베이스 전송 태스크 편집기** 대화 상자의 **데이터베이스** 페이지에서 **Method** 에 대해 **DatabaseOffline** 을 지정하여 **네트워크 파일 공유** 를 사용합니다.  
  
 네트워크 파일 공유 위치를 입력하거나 찾아보기 단추 **(...)** 를 클릭하여 네트워크 파일 공유 위치를 찾습니다.  
  
 오프라인 모드에서 데이터베이스를 전송할 때는 데이터베이스 파일이 대상 서버에 전송되기 전에 원본 서버의 **네트워크 파일 공유** 위치에 복사됩니다.  

## <a name="destination-database-files"></a>대상 데이터베이스 파일
  **대상 데이터베이스 파일** 대화 상자를 사용하여 대상 서버의 데이터베이스 파일 이름 및 위치를 확인 또는 변경하거나 데이터베이스 전송 태스크에 대한 네트워크 파일 위치를 지정할 수 있습니다.  
  
 이 대화 상자를 원본 서버의 데이터베이스 파일 이름 및 위치로 자동으로 채우려면 먼저 **데이터베이스 전송 태스크 편집기**대화 상자의 **데이터베이스**페이지에서 **SourceConnection** , **SourceDatabaseName** 및 **SourceDatabaseFiles** 를 지정합니다.  
  
### <a name="options"></a>옵션  
 **대상 파일**  
 전송된 대상 서버의 데이터베이스 파일 이름입니다.  
  
 파일 이름을 입력하거나 파일 이름을 클릭하여 편집합니다.  
  
 **대상 폴더**  
 데이터베이스 파일을 전송할 대상 서버의 폴더입니다.  
  
 폴더 경로를 입력하거나, 폴더 경로를 클릭하여 편집하거나, 찾아보기를 클릭하여 대상 서버의 데이터베이스 파일을 전송할 폴더를 찾습니다.  
  
 **네트워크 파일 공유**  
 데이터베이스 파일을 전송할 대상 서버의 네트워크 공유 폴더입니다. 오프라인 모드에서 데이터베이스를 전송할 때는 **데이터베이스 전송 태스크 편집기** 대화 상자의 **데이터베이스** 페이지에서 **Method** 에 대해 **DatabaseOffline** 을 지정하여 **네트워크 파일 공유** 를 사용합니다.  
  
 네트워크 파일 공유 위치를 입력하거나 찾아보기를 클릭하여 네트워크 파일 공유 위치를 찾습니다.  
  
 오프라인 모드에서 데이터베이스를 전송할 때는 데이터베이스 파일이 **대상 폴더** 위치에 전송되기 전에 **네트워크 파일 공유** 위치에 복사됩니다.  

