---
title: SSIS 카탈로그 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 24bd987e-164a-48fd-b4f2-cbe16a3cd95e
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 5a4d66ee27fbd3482ab51f27753355a585c58def
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080266"
---
# <a name="ssis-catalog"></a>SSIS 카탈로그
  `SSISDB` 카탈로그 작업을 위한 중앙 위치가 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에 배포한 (SSIS) 프로젝트는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버입니다. 예를 들어 프로젝트 및 패키지 매개 변수를 설정하고, 패키지의 런타임 값을 지정하기 위한 환경을 구성하고, 패키지를 실행하거나 문제를 해결하고, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버 작업을 관리할 수 있습니다.  
  
 에 저장 된 개체는 `SSISDB` 카탈로그 프로젝트, 패키지, 매개 변수, 환경 및 작업 기록이 포함 합니다.  
  
 개체, 설정 및 작업 데이터에 저장 되어 있는 경우를 조사 하는 `SSISDB` 에서 뷰를 쿼리하여 카탈로그는 `SSISDB` 데이터베이스입니다. 저장된 프로시저를 호출 하 여 개체를 관리할 수는 `SSISDB` 데이터베이스 또는의 UI를 사용 하 여는 `SSISDB` 카탈로그입니다. 대부분의 경우 UI를 사용하거나 저장 프로시저를 호출하여 동일한 태스크를 수행할 수 있습니다.  
  
 `SSISDB` 데이터베이스를 유지 관리하려면 사용자 데이터베이스 관리를 위한 표준 엔터프라이즈 정책을 적용하는 것이 좋습니다. 유지 관리 계획 만들기에 대해서는 [Maintenance Plans](../../relational-databases/maintenance-plans/maintenance-plans.md)을 참조하십시오.  
  
 `SSISDB` 카탈로그 및 `SSISDB` 데이터베이스 Windows PowerShell을 지원 합니다. Windows PowerShell과 SQL Server를 함께 사용하는 방법은 [SQL Server PowerShell](../../powershell/sql-server-powershell.md)을 참조하십시오. Windows PowerShell을 사용하여 프로젝트 배포와 같은 태스크를 수행하는 방법의 예는 blogs.msdn.com에서 [SQL Server 2012의 SSIS 및 PowerShell](http://go.microsoft.com/fwlink/?LinkId=242539)블로그 항목을 참조하십시오.  
  
 작업 데이터를 보는 방법에 대 한 자세한 내용은 참조 [패키지 실행 및 기타 작업에 대 한 모니터링](../performance/monitor-running-packages-and-other-operations.md)합니다.  
  
 액세스는 `SSISDB` 카탈로그에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에 연결 하 여는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다음을 확장 하 고 데이터베이스 엔진의 **Integration Services 카탈로그** 개체 탐색기에서 노드. 액세스는 `SSISDB` 여기에 데이터베이스 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 개체 탐색기에서 데이터베이스 노드를 확장 합니다.  
  
> [!NOTE]  
>  이름을 바꿀 수 없습니다는 `SSISDB` 데이터베이스입니다.  
  
> [!NOTE]  
>  경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 `SSISDB` 데이터베이스에 연결 된, 중지 또는 ISServerExec.exe 응답 하지 않으면 프로세스가 종료 합니다. 메시지는 Windows 이벤트 로그에 기록됩니다.  
>   
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스가 클러스터 장애 조치(Failover)의 일부로 장애 조치(Failover)되는 경우에는 실행 중인 패키지가 다시 시작되지 않습니다. 검사점을 사용하여 패키지를 다시 시작할 수 있습니다. 자세한 내용은 [검사점을 사용하여 패키지 다시 시작](../packages/restart-packages-by-using-checkpoints.md)을 참조하세요.  
  
## <a name="catalog-object-identifiers"></a>카탈로그 개체 식별자  
 카탈로그에서 새 개체를 만든 경우 해당 개체에 이름을 할당합니다. 개체 이름은 식별자입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 식별자에 사용할 수 있는 문자에 대한 규칙을 정의합니다. 다음 개체의 이름은 식별자 규칙을 따라야 합니다.  
  
-   Folder  
  
-   프로젝트  
  
-   환경  
  
-   매개 변수  
  
-   환경 변수  
  
### <a name="folder-project-environment"></a>폴더, 프로젝트, 환경  
 폴더, 프로젝트 또는 환경의 이름을 바꿀 때 고려할 규칙은 다음과 같습니다.  
  
-   ASCII/유니코드 문자 1~31, 따옴표("), 보다 작음(\<), 보다 큼(>), 파이프(|), 백스페이스(\b), null(\0) 및 탭(\t)은 올바른 문자가 아닙니다.  
  
-   이름은 선행 또는 후행 공백을 포함할 수 없습니다.  
  
-   @를 첫 글자로 사용할 수 없습니다. 하지만 후속 글자에는 @를 사용할 수 있습니다.  
  
-   이름의 길이는 1자에서 128자 사이여야 합니다.  
  
### <a name="parameter"></a>매개 변수  
 매개 변수 이름을 지정할 때 고려할 규칙은 다음과 같습니다.  
  
-   이름의 첫 글자는 Unicode Standard 2.0에서 정의한 문자이거나 밑줄(_)이어야 합니다.  
  
-   후속 글자는 Unicode Standard 2.0에 정의된 문자 또는 숫자이거나 밑줄(_)일 수 있습니다.  
  
### <a name="environment-variable"></a>환경 변수  
 환경 변수 이름을 지정할 때 고려할 규칙은 다음과 같습니다.  
  
-   ASCII/유니코드 문자 1~31, 따옴표("), 보다 작음(\<), 보다 큼(>), 파이프(|), 백스페이스(\b), null(\0) 및 탭(\t)은 올바른 문자가 아닙니다.  
  
-   이름은 선행 또는 후행 공백을 포함할 수 없습니다.  
  
-   @를 첫 글자로 사용할 수 없습니다. 하지만 후속 글자에는 @를 사용할 수 있습니다.  
  
-   이름의 길이는 1자에서 128자 사이여야 합니다.  
  
-   이름의 첫 글자는 Unicode Standard 2.0에서 정의한 문자이거나 밑줄(_)이어야 합니다.  
  
-   후속 글자는 Unicode Standard 2.0에 정의된 문자 또는 숫자이거나 밑줄(_)일 수 있습니다.  
  
## <a name="catalog-configuration"></a>카탈로그 구성  
 카탈로그 속성을 조정하여 카탈로그가 동작하는 방식을 세밀하게 조정할 수 있습니다. 카탈로그 속성은 중요한 데이터가 암호화되는 방법과 작업 및 프로젝트 버전 관리 데이터가 보존되는 방법을 정의합니다. 카탈로그 속성을 설정하려면 **카탈로그 속성** 대화 상자를 사용하거나 [catalog.configure_catalog&#40;SSISDB Database&#41;](/sql/integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database) 저장 프로시저를 호출합니다. 속성을 보려면 대화 상자를 사용하거나 [catalog.catalog_properties&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-catalog-properties-ssisdb-database)를 쿼리합니다. 개체 탐색기에서 `SSISDB`를 마우스 오른쪽 단추로 클릭하여 대화 상자에 액세스할 수 있습니다.  
  
### <a name="operations-and-project-version-cleanup"></a>작업 및 프로젝트 버전 정리  
 카탈로그의 많은 작업에 대한 상태 데이터는 내부 데이터베이스 테이블에 저장됩니다. 예를 들어 카탈로그는 패키지 실행 및 프로젝트 배포 상태를 추적합니다. 작업 데이터의 크기를 유지 관리하기 위해 **의** SSIS 서버 유지 관리 작업 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 오래된 데이터를 제거합니다. 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 가 설치될 때 만들어집니다.  
  
 카탈로그의 같은 폴더에 동일한 이름으로 배포하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 업데이트하거나 다시 배포할 수 있습니다. 기본적으로 다시 배포할 때마다 프로젝트는 `SSISDB` 카탈로그 이전 버전의 프로젝트를 보존 합니다. 작업 데이터의 크기를 유지 관리하기 위해 **SSIS 서버 유지 관리 작업** 을 사용하여 오래된 버전의 프로젝트를 제거합니다.  
  
 다음 `SSISDB` 카탈로그 속성 정의 방법을이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업의 동작입니다. **카탈로그 속성** 대화 상자를 사용하거나 [catalog.catalog_properties&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-catalog-properties-ssisdb-database) 및 [catalog.configure_catalog&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database)를 사용하여 속성을 보고 수정할 수 있습니다.  
  
 **주기적으로 로그 정리**  
 이 속성은로 설정 하는 경우 작업 정리를 위한 작업 단계가 실행 `True`합니다.  
  
 **보존 기간(일)**  
 허용 가능한 작업 데이터의 최대 수명(일)을 정의합니다. 오래된 데이터는 제거됩니다.  
  
 최소값은 1일입니다. 최 댓 값의 최대값에 의해서만 제한 됩니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `int` 데이터입니다. 이 데이터 형식에 대한 자세한 내용은 [int, bigint, smallint 및 tinyint&#40;Transact-SQL&#41;](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql)를 참조하세요.  
  
 **주기적으로 이전 버전을 제거**  
 이 속성 설정 된 경우 프로젝트 버전 정리를 위한 작업 단계가 실행 `True`합니다.  
  
 **프로젝트당 최대 버전 수**  
 카탈로그에 저장되는 프로젝트 버전 수를 정의합니다. 오래된 버전의 프로젝트는 제거됩니다.  
  
### <a name="encryption-algorithm"></a>암호화 알고리즘  
 **암호화 알고리즘** 속성은 중요한 매개 변수 값을 암호화하는 데 사용되는 암호화 유형을 지정합니다. 다음 암호화 유형 중에서 선택할 수 있습니다.  
  
-   AES_256(기본값)  
  
-   AES_192  
  
-   AES_128  
  
-   DESX  
  
-   TRIPLE_DES_3KEY  
  
-   TRIPLE_DES  
  
-   DES  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]서버에 배포하는 경우 카탈로그에서 패키지 데이터와 중요한 값을 자동으로 암호화합니다. 카탈로그에서는 검색하는 데이터의 암호도 자동으로 해제합니다. SSISDB 카탈로그에서는 `ServerStorage` 보호 수준입니다. 자세한 내용은 [Access Control for Sensitive Data in Packages](../security/access-control-for-sensitive-data-in-packages.md)을 참조하세요.  
  
 암호화 알고리즘을 변경하는 작업에는 시간이 많이 소비됩니다. 먼저 서버에서 이전에 지정된 알고리즘을 사용하여 모든 구성 값의 암호를 해독해야 합니다. 그런 다음 새 알고리즘을 사용하여 값을 다시 암호화해야 합니다. 그 동안 서버에서 다른 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 작업을 수행할 수 없습니다. 따라서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 작업을 중단 없이 지속되게 하려면 암호화 알고리즘이 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 대화 상자에서 읽기 전용 값으로 지정되어야 합니다.  
  
 변경 하는 **암호화 알고리즘** 속성 설정이 설정는 `SSISDB` 단일 사용자 모드로 데이터베이스에 있으며 다음 catalog.configure_catalog 저장 프로시저를 호출 합니다. *property_name* 인수에 ENCRYPTION_ALGORITHM을 사용합니다. 지원되는 속성 값에 대한 자세한 내용은 [catalog.catalog_properties&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-catalog-properties-ssisdb-database)를 참조하세요. 저장 프로시저에 대한 자세한 내용은 [catalog.configure_catalog&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database)를 참조하세요.  
  
 단일 사용자 모드에 대한 자세한 내용은 [단일 사용자 모드로 데이터베이스 설정](../../relational-databases/databases/set-a-database-to-single-user-mode.md)을 참조하세요. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 암호화 및 암호화 알고리즘에 대한 자세한 내용은 [SQL Server 암호화](../../relational-databases/security/encryption/sql-server-encryption.md)섹션의 항목을 참조하세요.  
  
 데이터베이스 마스터 키는 암호화에 사용됩니다. 이 키는 카탈로그를 만들 때 생성됩니다. 자세한 내용은 [SSIS 카탈로그 만들기](ssis-catalog.md)를 참조하세요.  
  
 다음 표에는 **카탈로그 속성** 대화 상자에 표시되는 속성 이름과 데이터베이스 뷰의 해당 속성이 나와 있습니다.  
  
|속성 이름(**카탈로그 속성** 대화 상자)|속성 이름(데이터베이스 뷰)|  
|---------------------------------------------------------|-------------------------------------|  
|암호화 알고리즘 이름|ENCRYPTION_ALGORITHM|  
|주기적으로 로그 정리|OPERATION_CLEANUP_ENABLED|  
|보존 기간(일)|RETENTION_WINDOW|  
|주기적으로 이전 버전을 제거|VERSION_CLEANUP_ENABLED|  
|프로젝트당 최대 버전 수|MAX_PROJECT_VERSIONS|  
|서버 차원의 기본 로깅 수준|SERVER_LOGGING_LEVEL|  
  
## <a name="permissions"></a>사용 권한  
 프로젝트, 환경 및 패키지는 보안 개체인 폴더에 포함됩니다. MANAGE_OBJECT_PERMISSIONS 권한을 포함하여 폴더에 대한 사용 권한을 부여할 수 있습니다. MANAGE_OBJECT_PERMISSIONS는 ssis_admin 역할에 대한 사용자 멤버 자격을 부여하지 않고도 사용자에게 폴더 내용에 대한 관리를 위임할 수 있습니다. 프로젝트, 환경 및 작업에 사용 권한을 부여할 수도 있습니다. 작업에는 초기화 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], 배포 프로젝트, 만들기 및 실행을 시작, 프로젝트 및 패키지 유효성 검사 및 구성의 `SSISDB` 카탈로그입니다.  
  
 데이터베이스 역할에 대한 자세한 내용은 [데이터베이스 수준 역할](../../relational-databases/security/authentication-access/database-level-roles.md)을 참조하세요.  
  
 SSISDB 카탈로그는 ddl_cleanup_object_permissions DDL 트리거를 사용하여 SSIS 보안 개체에 대한 사용 권한 정보의 무결성을 보장합니다. 데이터베이스 사용자, 데이터베이스 역할 또는 데이터베이스 응용 프로그램 역할과 같은 데이터베이스 보안 주체가 SSISDB 데이터베이스에서 제거되면 트리거가 실행됩니다.  
  
 보안 주체가 다른 보안 주체에 대해 사용 권한을 부여하거나 거부한 경우 해당 보안 주체를 제거하려면 먼저 부여자가 제공한 사용 권한을 취소해야 합니다. 그러지 않으면 시스템에서 보안 주체를 제거하려고 할 때 오류 메시지가 반환됩니다. 트리거는 데이터베이스 보안 주체가 피부여자인 모든 사용 권한 레코드를 제거합니다.  
  
 데이터베이스 보안 주체에서 삭제 된 후 분리 된 사용 권한 레코드가 발생 하지 않는 것이 있기 때문에 트리거가 비활성화 되지 않습니다 것이 좋습니다.는 `SSISDB` 데이터베이스입니다.  
  
### <a name="managing-permissions"></a>사용 권한 관리  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] UI, 저장 프로시저 및 <xref:Microsoft.SqlServer.Management.IntegrationServices> 네임스페이스를 사용하여 사용 권한을 관리할 수 있습니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] UI를 사용하여 사용 권한을 관리하려면 다음 대화 상자를 사용합니다.  
  
-   폴더를 사용 하 여는 **권한을** 의 페이지는 [Folder Properties Dialog Box](folder-properties-dialog-box.md)합니다.  
  
-   프로젝트를 사용 하 여는 **권한을** 페이지에 [Project Properties Dialog Box](project-properties-dialog-box.md).  
  
 TRANSACT-SQL을 사용하여 사용 권한을 관리하려면 [catalog.grant_permission&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database), [catalog.deny_permission&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-deny-permission-ssisdb-database) 및 [catalog.revoke_permission&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-revoke-permission-ssisdb-database)을 참조하세요. 모든 개체의 현재 보안 주체에 대한 유효한 사용 권한을 보려면 [catalog.effective_object_permissions&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-effective-object-permissions-ssisdb-database)를 쿼리합니다. 이 항목에서는 여러 유형의 사용 권한에 대해 설명합니다. 사용자에게 명시적으로 할당된 사용 권한을 보려면 [catalog.explicit_object_permissions&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-explicit-object-permissions-ssisdb-database)를 쿼리합니다.  
  
## <a name="folders"></a>폴더  
 프로젝트 및 환경에 하나 이상의 폴더에 포함 된 `SSISDB` 카탈로그입니다. [catalog.folders&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-folders-ssisdb-database) 뷰를 사용하여 카탈로그의 폴더에 대한 정보에 액세스할 수 있습니다. 다음 저장 프로시저를 사용하여 폴더를 관리할 수 있습니다.  
  
-   [catalog.create_folder&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-create-folder-ssisdb-database)  
  
-   [catalog.delete_folder&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-folder-ssisdb-database)  
  
-   [catalog.rename_folder&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-rename-folder-ssisdb-database)  
  
-   [catalog.set_folder_description&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-set-folder-description-ssisdb-database)  
  
## <a name="projects-and-packages"></a>프로젝트 및 패키지  
 각 프로젝트에 여러 패키지를 포함할 수 있습니다. 프로젝트와 패키지 모두 매개 변수 및 환경 참조를 포함할 수 있습니다. [Configure Dialog Box](configure-dialog-box.md)를 사용하여 매개 변수 및 환경 참조에 액세스할 수 있습니다.  
  
 다음 저장 프로시저를 호출하여 다른 프로젝트 태스크를 수행할 수 있습니다.  
  
-   [catalog.delete_project &#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-project-ssisdb-database)  
  
-   [catalog.deploy_project &#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database)  
  
-   [catalog.get_project &#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-get-project-ssisdb-database)  
  
-   [catalog.move_project &#40;&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-move-project-ssisdb-database)  
  
-   [catalog.restore_project &#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database)  
  
 이러한 뷰는 패키지, 프로젝트 및 프로젝트 버전에 대한 자세한 정보를 제공합니다.  
  
-   [catalog.projects &#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-projects-ssisdb-database)  
  
-   [catalog.packages &#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-packages-ssisdb-database)  
  
-   [catalog.object_versions &#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-object-versions-ssisdb-database)  
  
## <a name="parameters"></a>매개 변수  
 매개 변수를 사용하여 패키지 실행 시 패키지 속성에 값을 할당할 수 있습니다. 패키지 또는 프로젝트 매개 변수의 값을 설정하고 값을 지우려면 [catalog.set_object_parameter_value&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database) 및 [catalog.clear_object_parameter_value&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database)를 호출합니다. 실행 인스턴스에 대한 매개 변수 값을 설정하려면 [catalog.set_execution_parameter_value&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database)를 호출합니다. [catalog.get_parameter_values&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database)를 호출하여 기본 매개 변수 값을 검색할 수 있습니다.  
  
 이러한 뷰는 모든 패키지 및 프로젝트에 대한 매개 변수와 실행 인스턴스에 사용되는 매개 변수 값을 표시합니다.  
  
-   [catalog.object_parameters&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database)  
  
-   [catalog.execution_parameter_values&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-execution-parameter-values-ssisdb-database)  
  
## <a name="server-environments-server-variables-and-server-environment-references"></a>서버 환경, 서버 변수 및 서버 환경 참조  
 서버 환경에는 서버 변수가 포함되어 있습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에서 패키지를 실행하거나 유효성을 검사할 때 변수 값을 사용할 수 있습니다.  
  
 다음 저장 프로시저를 사용하여 환경 및 변수에 대한 다른 많은 관리 태스크를 수행할 수 있습니다.  
  
-   [catalog.create_environment&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-create-environment-ssisdb-database)  
  
-   [catalog.delete_environment&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-environment-ssisdb-database)  
  
-   [catalog.move_environment&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-move-environment-ssisdb-database)  
  
-   [catalog.rename_environment&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-rename-environment-ssisdb-database)  
  
-   [catalog.set_environment_property&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-set-environment-property-ssisdb-database)  
  
-   [catalog.create_environment_variable&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-create-environment-variable-ssisdb-database)  
  
-   [catalog.delete_environment_variable&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-environment-variable-ssisdb-database)  
  
-   [catalog.set_environment_variable_property&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-set-environment-variable-property-ssisdb-database)  
  
-   [catalog.set_environment_variable_value&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-set-environment-variable-value-ssisdb-database)  
  
 [catalog.set_environment_variable_protection&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-set-environment-variable-protection-ssisdb-database) 저장 프로시저를 호출하여 변수에 대한 민감도 비트를 설정할 수 있습니다.  
  
 서버 변수 값을 사용하려면 프로젝트와 서버 환경 간의 참조를 지정합니다. 다음 저장 프로시저를 사용하여 참조를 만들거나 삭제할 수 있습니다. 환경을 프로젝트와 같은 폴더에서 찾을 수 있는지, 아니면 다른 폴더에서 찾을 수 있는지를 나타낼 수도 있습니다.  
  
-   [catalog.create_environment_reference&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-create-environment-reference-ssisdb-database)  
  
-   [catalog.delete_environment_reference&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-environment-reference-ssisdb-database)  
  
-   [catalog.set_environment_reference_type&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-set-environment-reference-type-ssisdb-database)  
  
 환경 및 변수에 대한 자세한 정보를 보려면 이러한 뷰를 쿼리하십시오.  
  
-   [catalog.environments&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-environments-ssisdb-database)  
  
-   [catalog.environment_variables&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-environment-variables-ssisdb-database)  
  
-   [catalog.environment_references&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-environment-references-ssisdb-database)  
  
## <a name="executions-and-validations"></a>실행 및 유효성 검사  
 실행은 패키지 실행의 인스턴스입니다. 실행을 만들고 시작하려면 [catalog.create_execution&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database) 및 [catalog.start_execution&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database)을 호출합니다. 실행 또는 패키지/프로젝트 유효성 검사를 중지하려면 [catalog.stop_operation&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database)을 호출합니다.  
  
 실행 중인 패키지를 일시 중지하고 덤프 파일을 만들려면 catalog.create_execution_dump 저장 프로시저를 호출합니다. 덤프 파일은 실행 문제를 해결하는 데 도움이 될 수 있는 패키지 실행에 대한 정보를 제공합니다. 덤프 파일을 생성하고 구성하는 방법은 [Generating Dump Files for Package Execution](../troubleshooting/generating-dump-files-for-package-execution.md)을 참조하십시오.  
  
 실행, 유효성 검사, 작업 중에 기록되는 메시지 및 오류와 관련된 상황별 정보에 대한 자세한 정보를 보려면 이러한 뷰를 쿼리하십시오.  
  
-   [catalog.executions&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-executions-ssisdb-database)  
  
-   [catalog.operations&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-operations-ssisdb-database)  
  
-   [catalog.operation_messages&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-operation-messages-ssisdb-database)  
  
-   [catalog.extended_operation_info&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-extended-operation-info-ssisdb-database)  
  
-   [catalog.event_messages](/sql/integration-services/system-views/catalog-event-messages)  
  
-   [catalog.event_message_context](/sql/integration-services/system-views/catalog-event-message-context)  
  
 [catalog.validate_project&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-validate-project-ssisdb-database) 및 [catalog.validate_package&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-validate-package-ssisdb-database) 저장 프로시저를 호출하여 프로젝트와 패키지의 유효성을 검사할 수 있습니다. [catalog.validations&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-validations-ssisdb-database) 뷰는 유효성 검사에서 고려되는 서버 환경 참조, 유효성 검사가 종속성 유효성 검사인지 또는 전체 유효성 검사인지 여부, 패키지를 실행하는 데 32비트 런타임이 사용되는지 또는 64비트 런타임이 사용되는지 여부 등에 대한 자세한 정보를 제공합니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [SSIS 카탈로그 만들기](ssis-catalog.md)  
  
-   [SSIS 카탈로그 백업, 복원 및 이동](../backup-restore-and-move-the-ssis-catalog.md)  
  
## <a name="related-content"></a>관련 내용  
  
-   blogs.msdn.com의 블로그 항목 - [SQL Server 2012의 SSIS 및 PowerShell](http://go.microsoft.com/fwlink/?LinkId=242539)  
  
-   blogs.msdn.com의 블로그 항목 - [SSIS 카탈로그 액세스 제어 팁](http://go.microsoft.com/fwlink/?LinkId=246669)  
  
-   blogs.msdn.com의 블로그 항목 - [SSIS 카탈로그 관리 개체 모델에 대한 이해](http://go.microsoft.com/fwlink/?LinkId=254267)  
  
  
