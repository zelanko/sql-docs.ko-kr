---
title: SSIS 카탈로그 | Microsoft Docs
ms.custom: ''
ms.date: 11/12/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.iscreatecatalog.f1
- sql13.ssis.ssms.iscatalogprop.general.f1
- sql13.ssis.dbupgradewizard.f1
ms.assetid: 24bd987e-164a-48fd-b4f2-cbe16a3cd95e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1e240a53d86d66fdf81b53cae1ba55d41820befd
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79287727"
---
# <a name="ssis-catalog"></a>SSIS 카탈로그

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **SSISDB** 카탈로그는 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] 서버에 배포한 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)](SSIS) 프로젝트를 사용할 수 있는 중앙 위치입니다. 예를 들어 프로젝트 및 패키지 매개 변수를 설정하고, 패키지의 런타임 값을 지정하기 위한 환경을 구성하고, 패키지를 실행하거나 문제를 해결하고, [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] 서버 작업을 관리할 수 있습니다.  
 
> [!NOTE]
> 이 문서에서는 일반적인 SSIS 카탈로그 및 온-프레미스에서 실행되는 SSIS 카탈로그를 설명합니다. Azure SQL Database에서 SSIS 카탈로그를 만들고 Azure에서 SSIS 패키지를 배포 및 실행할 수도 있습니다. 자세한 내용은 [SQL Server Integration Services 워크로드를 클라우드로 리프트 앤 시프트](../lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)를 참조하세요.
>
> Linux에서 SSIS 패키지를 실행할 수 있더라도 SSIS 카탈로그는 Linux에서 지원되지 않습니다. 자세한 내용은 [Linux에서 SSIS를 사용하여 데이터 추출, 변환 및 로드](../../linux/sql-server-linux-migrate-ssis.md)를 참조하세요.
 
 **SSISDB** 카탈로그에 저장되는 개체에는 프로젝트, 패키지, 매개 변수, 환경 및 작업 기록이 있습니다.  
  
 **SSISDB** 데이터베이스에서 뷰를 쿼리하여 **SSISDB** 카탈로그에 저장된 개체, 설정 및 작업 데이터를 검사할 수 있습니다. **SSISDB** 데이터베이스에서 저장 프로시저를 호출하거나 **SSISDB** 카탈로그의 UI를 사용하여 개체를 관리할 수 있습니다. 대부분의 경우 UI를 사용하거나 저장 프로시저를 호출하여 동일한 태스크를 수행할 수 있습니다.  
  
 **SSISDB** 데이터베이스를 유지 관리하려면 사용자 데이터베이스 관리를 위한 표준 엔터프라이즈 정책을 적용하는 것이 좋습니다. 유지 관리 계획 만들기에 대해서는 [Maintenance Plans](../../relational-databases/maintenance-plans/maintenance-plans.md)을 참조하십시오.  
  
 **SSISDB** 카탈로그 및 **SSISDB** 데이터베이스는 Windows PowerShell을 지원합니다. Windows PowerShell과 SQL Server를 함께 사용하는 방법은 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)을 참조하십시오. Windows PowerShell을 사용하여 프로젝트 배포와 같은 태스크를 수행하는 방법의 예는 blogs.msdn.com에서 [SQL Server 2012의 SSIS 및 PowerShell](https://go.microsoft.com/fwlink/?LinkId=242539)블로그 항목을 참조하십시오.  
  
 작업 데이터를 보는 방법에 대한 자세한 내용은 [실행 중인 패키지 및 기타 작업 모니터링](../../integration-services/performance/monitor-running-packages-and-other-operations.md)을 참조하세요.  
  
 **데이터베이스 엔진에 연결한 다음 개체 탐색기에서** Integration Services 카탈로그 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 노드를 확장하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 **SSISDB** 카탈로그에 액세스합니다. **에서** SSISDB [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 데이터베이스에 액세스하려면 개체 탐색기에서 데이터베이스 노드를 확장하면 됩니다.  
  
> [!NOTE]
> **SSISDB** 데이터베이스 이름은 바꿀 수 없습니다.  
  
> [!NOTE]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSISDB **데이터베이스가 연결된** 인스턴스가 중지되었거나 응답하지 않으면 ISServerExec.exe 프로세스가 종료됩니다. 메시지는 Windows 이벤트 로그에 기록됩니다.  
>   
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스가 클러스터 장애 조치(Failover)의 일부로 장애 조치(Failover)되는 경우에는 실행 중인 패키지가 다시 시작되지 않습니다. 검사점을 사용하여 패키지를 다시 시작할 수 있습니다. 자세한 내용은 [검사점을 사용하여 패키지 다시 시작](../../integration-services/packages/restart-packages-by-using-checkpoints.md)을 참조하세요.  
  
## <a name="features-and-capabilities"></a>특징과 기능  
  
-   [카탈로그 개체 식별자](../../integration-services/catalog/ssis-catalog.md#CatalogObjectIdentifiers)  
  
-   [카탈로그 구성](../../integration-services/catalog/ssis-catalog.md#Configuration)  
  
-   [권한](../../integration-services/catalog/ssis-catalog.md#Permissions)  
  
-   [폴더](../../integration-services/catalog/ssis-catalog.md#Folders)  
  
-   [프로젝트 및 패키지](../../integration-services/catalog/ssis-catalog.md#ProjectsAndPackages)  
  
-   [매개 변수](../../integration-services/catalog/ssis-catalog.md#Parameters)  
  
-   [서버 환경, 서버 변수 및 서버 환경 참조](../../integration-services/catalog/ssis-catalog.md#ServerEnvironments)  
  
-   [실행 및 유효성 검사](../../integration-services/catalog/ssis-catalog.md#Executions)  

##  <a name="CatalogObjectIdentifiers"></a> 카탈로그 개체 식별자  
 카탈로그에서 새 개체를 만든 경우 해당 개체에 이름을 할당합니다. 개체 이름은 식별자입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 식별자에 사용할 수 있는 문자에 대한 규칙을 정의합니다. 다음 개체의 이름은 식별자 규칙을 따라야 합니다.  
  
-   폴더  
  
-   Project  
  
-   Environment  
  
-   매개 변수  
  
-   환경 변수  
  
###  <a name="Folder"></a> 폴더, 프로젝트, 환경  
 폴더, 프로젝트 또는 환경의 이름을 바꿀 때 고려할 규칙은 다음과 같습니다.  
  
-   ASCII/유니코드 문자 1~31, 따옴표("), 보다 작음(\<), 보다 큼(>), 파이프(|), 백스페이스(\b), null(\0) 및 탭(\t)은 올바른 문자가 아닙니다.  
  
-   이름은 선행 또는 후행 공백을 포함할 수 없습니다.  
  
-   \@를 첫 글자로 사용할 수 없습니다. 하지만 후속 글자에는 \@를 사용할 수 있습니다.  
  
-   이름의 길이는 1자에서 128자 사이여야 합니다.  
  
###  <a name="Parameter"></a> 매개 변수  
 매개 변수 이름을 지정할 때 고려할 규칙은 다음과 같습니다.  
  
-   이름의 첫 글자는 Unicode Standard 2.0에서 정의한 문자이거나 밑줄(_)이어야 합니다.  
  
-   후속 글자는 Unicode Standard 2.0에 정의된 문자 또는 숫자이거나 밑줄(_)일 수 있습니다.  
  
###  <a name="EnvironmentVariable"></a> 환경 변수  
 환경 변수 이름을 지정할 때 고려할 규칙은 다음과 같습니다.  
  
-   ASCII/유니코드 문자 1~31, 따옴표("), 보다 작음(\<), 보다 큼(>), 파이프(|), 백스페이스(\b), null(\0) 및 탭(\t)은 올바른 문자가 아닙니다.  
  
-   이름은 선행 또는 후행 공백을 포함할 수 없습니다.  
  
-   \@를 첫 글자로 사용할 수 없습니다. 하지만 후속 글자에는 \@를 사용할 수 있습니다.  
  
-   이름의 길이는 1자에서 128자 사이여야 합니다.  
  
-   이름의 첫 글자는 Unicode Standard 2.0에서 정의한 문자이거나 밑줄(_)이어야 합니다.  
  
-   후속 글자는 Unicode Standard 2.0에 정의된 문자 또는 숫자이거나 밑줄(_)일 수 있습니다.  
  
##  <a name="Configuration"></a> 카탈로그 구성  
 카탈로그 속성을 조정하여 카탈로그가 동작하는 방식을 세밀하게 조정할 수 있습니다. 카탈로그 속성은 중요한 데이터가 암호화되는 방법과 작업 및 프로젝트 버전 관리 데이터가 보존되는 방법을 정의합니다. 카탈로그 속성을 설정하려면 **카탈로그 속성** 대화 상자를 사용하거나 [catalog.configure_catalog&#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md) 저장 프로시저를 호출합니다. 속성을 보려면 대화 상자를 사용하거나 [catalog.catalog_properties&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)를 쿼리합니다. 개체 탐색기에서 **SSISDB**를 마우스 오른쪽 단추로 클릭하여 대화 상자에 액세스할 수 있습니다.  
  
###  <a name="Cleanup"></a> 작업 및 프로젝트 버전 정리  
 카탈로그의 많은 작업에 대한 상태 데이터는 내부 데이터베이스 테이블에 저장됩니다. 예를 들어 카탈로그는 패키지 실행 및 프로젝트 배포 상태를 추적합니다. 작업 데이터의 크기를 유지 관리하기 위해 **의** SSIS 서버 유지 관리 작업 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 오래된 데이터를 제거합니다. 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 가 설치될 때 만들어집니다.  
  
 카탈로그의 같은 폴더에 동일한 이름으로 배포하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 업데이트하거나 다시 배포할 수 있습니다. 기본적으로 프로젝트를 다시 배포할 때마다 **SSISDB** 카탈로그에서 이전 버전의 프로젝트를 보존합니다. 작업 데이터의 크기를 유지 관리하기 위해 **SSIS 서버 유지 관리 작업** 을 사용하여 오래된 버전의 프로젝트를 제거합니다.  
 
**SSIS Server 유지 관리 작업**을 실행하기 위해 SSIS는 SQL Server 로그인 **##MS_SSISServerCleanupJobLogin##** 을 만듭니다. 이 로그인은 SSIS 내부에서만 사용됩니다.
  
 이 **에이전트 작업의 동작 방법은 다음** SSISDB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 카탈로그 속성에 의해 정의됩니다. **카탈로그 속성** 대화 상자를 사용하거나 [catalog.catalog_properties&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) 및 [catalog.configure_catalog&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md)를 사용하여 속성을 보고 수정할 수 있습니다.  
  
 **주기적으로 로그 정리**  
 이 속성이 **True**로 설정된 경우 작업 정리를 위한 작업 단계가 실행됩니다.  
  
 **보존 기간(일)**  
 허용 가능한 작업 데이터의 최대 수명(일)을 정의합니다. 오래된 데이터는 제거됩니다.  
  
 최소값은 1일입니다. 최대값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **int** 데이터의 최대값에 의해서만 제한됩니다. 이 데이터 형식에 대한 자세한 내용은 [int, bigint, smallint 및 tinyint&#40;Transact-SQL&#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)를 참조하세요.  
  
 **주기적으로 이전 버전을 제거**  
 이 속성이 **True**로 설정된 경우 프로젝트 버전 정리를 위한 작업 단계가 실행됩니다.  
  
 **프로젝트당 최대 버전 수**  
 카탈로그에 저장되는 프로젝트 버전 수를 정의합니다. 오래된 버전의 프로젝트는 제거됩니다.  
  
###  <a name="Encryption"></a> 암호화 알고리즘  
 **암호화 알고리즘** 속성은 중요한 매개 변수 값을 암호화하는 데 사용되는 암호화 유형을 지정합니다. 다음 암호화 유형 중에서 선택할 수 있습니다.  
  
-   AES_256(기본값)  
  
-   AES_192  
  
-   AES_128  
  
-   DESX  
  
-   TRIPLE_DES_3KEY  
  
-   TRIPLE_DES  
  
-   DES  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포하는 경우 카탈로그에서 패키지 데이터와 중요한 값을 자동으로 암호화합니다. 카탈로그에서는 검색하는 데이터의 암호도 자동으로 해제합니다. SSISDB 카탈로그에서는 **ServerStorage** 보호 수준을 사용합니다. 자세한 내용은 [Access Control for Sensitive Data in Packages](../../integration-services/security/access-control-for-sensitive-data-in-packages.md)을 참조하세요.  
  
 암호화 알고리즘을 변경하는 작업에는 시간이 많이 소비됩니다. 먼저 서버에서 이전에 지정된 알고리즘을 사용하여 모든 구성 값의 암호를 해독해야 합니다. 그런 다음 새 알고리즘을 사용하여 값을 다시 암호화해야 합니다. 그 동안 서버에서 다른 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 작업을 수행할 수 없습니다. 따라서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 작업을 중단 없이 지속되게 하려면 암호화 알고리즘이 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 대화 상자에서 읽기 전용 값으로 지정되어야 합니다.  
  
 **암호화 알고리즘** 속성 설정을 변경하려면 **SSISDB** 데이터베이스를 단일 사용자 모드로 설정한 다음 catalog.configure_catalog 저장 프로시저를 호출합니다. *property_name* 인수에 ENCRYPTION_ALGORITHM을 사용합니다. 지원되는 속성 값에 대한 자세한 내용은 [catalog.catalog_properties&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)를 참조하세요. 저장 프로시저에 대한 자세한 내용은 [catalog.configure_catalog&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md)를 참조하세요.  
  
 단일 사용자 모드에 대한 자세한 내용은 [단일 사용자 모드로 데이터베이스 설정](../../relational-databases/databases/set-a-database-to-single-user-mode.md)을 참조하세요. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 암호화 및 암호화 알고리즘에 대한 자세한 내용은 [SQL Server 암호화](../../relational-databases/security/encryption/sql-server-encryption.md)섹션의 항목을 참조하세요.  
  
 데이터베이스 마스터 키는 암호화에 사용됩니다. 이 키는 카탈로그를 만들 때 생성됩니다.  
  
 다음 표에는 **카탈로그 속성** 대화 상자에 표시되는 속성 이름과 데이터베이스 뷰의 해당 속성이 나와 있습니다.  
  
|속성 이름(**카탈로그 속성** 대화 상자)|속성 이름(데이터베이스 뷰)|  
|---------------------------------------------------------|-------------------------------------|  
|암호화 알고리즘 이름|ENCRYPTION_ALGORITHM|  
|주기적으로 로그 정리|OPERATION_CLEANUP_ENABLEDâ€‹|  
|보존 기간(일)|RETENTION_WINDOW|  
|주기적으로 이전 버전을 제거|VERSION_CLEANUP_ENABLED|  
|프로젝트당 최대 버전 수|MAX_PROJECT_VERSIONS|  
|서버 차원의 기본 로깅 수준|SERVER_LOGGING_LEVEL|  
  
##  <a name="Permissions"></a> 권한  
 프로젝트, 환경 및 패키지는 보안 개체인 폴더에 포함됩니다. MANAGE_OBJECT_PERMISSIONS 권한을 포함하여 폴더에 대한 사용 권한을 부여할 수 있습니다. MANAGE_OBJECT_PERMISSIONS는 ssis_admin 역할에 대한 사용자 멤버 자격을 부여하지 않고도 사용자에게 폴더 내용에 대한 관리를 위임할 수 있습니다. 프로젝트, 환경 및 작업에 사용 권한을 부여할 수도 있습니다. 작업에는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]초기화, 프로젝트 배포, 실행 만들기 및 시작, 프로젝트 및 패키지 유효성 검사, **SSISDB** 카탈로그 구성 등이 있습니다.  
  
 데이터베이스 역할에 대한 자세한 내용은 [데이터베이스 수준 역할](../../relational-databases/security/authentication-access/database-level-roles.md)을 참조하세요.  
  
 SSISDB 카탈로그는 ddl_cleanup_object_permissions DDL 트리거를 사용하여 SSIS 보안 개체에 대한 사용 권한 정보의 무결성을 보장합니다. 데이터베이스 사용자, 데이터베이스 역할 또는 데이터베이스 애플리케이션 역할과 같은 데이터베이스 보안 주체가 SSISDB 데이터베이스에서 제거되면 트리거가 실행됩니다.  
  
 보안 주체가 다른 보안 주체에 대해 사용 권한을 부여하거나 거부한 경우 해당 보안 주체를 제거하려면 먼저 부여자가 제공한 사용 권한을 취소해야 합니다. 그러지 않으면 시스템에서 보안 주체를 제거하려고 할 때 오류 메시지가 반환됩니다. 트리거는 데이터베이스 보안 주체가 피부여자인 모든 사용 권한 레코드를 제거합니다.  
  
 트리거를 사용하면 데이터베이스 보안 주체가 **SSISDB** 데이터베이스에서 삭제된 후 분리된 사용 권한 레코드가 발생하지 않으므로 가능하면 트리거를 사용하도록 설정하는 것이 좋습니다.  
  
### <a name="managing-permissions"></a>사용 권한 관리  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] UI, 저장 프로시저 및 <xref:Microsoft.SqlServer.Management.IntegrationServices> 네임스페이스를 사용하여 사용 권한을 관리할 수 있습니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] UI를 사용하여 사용 권한을 관리하려면 다음 대화 상자를 사용합니다. 
  
-   폴더를 사용 하 여는 **권한을** 의 페이지는 [Folder Properties Dialog Box](../../integration-services/catalog/folder-properties-dialog-box.md)합니다.  
  
-   프로젝트를 사용 하 여는 **권한을** 페이지에 [Project Properties Dialog Box](../../integration-services/catalog/project-properties-dialog-box.md).  

 Transact-SQL을 사용하여 사용 권한을 관리하려면 [catalog.grant_permission&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database.md), [catalog.deny_permission&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-deny-permission-ssisdb-database.md) 및 [catalog.revoke_permission&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-revoke-permission-ssisdb-database.md)을 참조하세요. 모든 개체의 현재 보안 주체에 대한 유효한 사용 권한을 보려면 [catalog.effective_object_permissions&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-effective-object-permissions-ssisdb-database.md)를 쿼리합니다. 이 항목에서는 여러 유형의 사용 권한에 대해 설명합니다. 사용자에게 명시적으로 할당된 사용 권한을 보려면 [catalog.explicit_object_permissions&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-explicit-object-permissions-ssisdb-database.md)를 쿼리합니다.  
  
##  <a name="Folders"></a> 폴더  
 폴더에는 **SSISDB** 카탈로그의 프로젝트 및 환경이 하나 이상 포함됩니다. [catalog.folders&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-folders-ssisdb-database.md) 뷰를 사용하여 카탈로그의 폴더에 대한 정보에 액세스할 수 있습니다. 다음 저장 프로시저를 사용하여 폴더를 관리할 수 있습니다.  
  
-   [catalog.create_folder&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-create-folder-ssisdb-database.md)  
  
-   [catalog.delete_folder&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-delete-folder-ssisdb-database.md)  
  
-   [catalog.rename_folder&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-rename-folder-ssisdb-database.md)  
  
-   [catalog.set_folder_description&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-set-folder-description-ssisdb-database.md)  
  
##  <a name="ProjectsAndPackages"></a> 프로젝트 및 패키지  
 각 프로젝트에 여러 패키지를 포함할 수 있습니다. 프로젝트와 패키지 모두 매개 변수 및 환경 참조를 포함할 수 있습니다. [Configure Dialog Box](../../integration-services/catalog/configure-dialog-box.md)를 사용하여 매개 변수 및 환경 참조에 액세스할 수 있습니다.  
  
 다음 저장 프로시저를 호출하여 다른 프로젝트 태스크를 수행할 수 있습니다. 
  
-   [catalog.delete_project &#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-delete-project-ssisdb-database.md)  
  
-   [catalog.deploy_project &#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md)  
  
-   [catalog.get_project &#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-get-project-ssisdb-database.md)  
  
-   [catalog.move_project &#40;&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-move-project-ssisdb-database.md)  
  
-   [catalog.restore_project &#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database.md)  
  
 이러한 뷰는 패키지, 프로젝트 및 프로젝트 버전에 대한 자세한 정보를 제공합니다.  
  
-   [catalog.projects &#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-projects-ssisdb-database.md)  
  
-   [catalog.packages &#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-packages-ssisdb-database.md)  
  
-   [catalog.object_versions &#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-object-versions-ssisdb-database.md)  
  
##  <a name="Parameters"></a> 매개 변수  
 매개 변수를 사용하여 패키지 실행 시 패키지 속성에 값을 할당할 수 있습니다. 패키지 또는 프로젝트 매개 변수의 값을 설정하고 값을 지우려면 [catalog.set_object_parameter_value&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database.md) 및 [catalog.clear_object_parameter_value&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database.md)를 호출합니다. 실행 인스턴스에 대한 매개 변수 값을 설정하려면 [catalog.set_execution_parameter_value&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)를 호출합니다. [catalog.get_parameter_values&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md)를 호출하여 기본 매개 변수 값을 검색할 수 있습니다.  
  
 이러한 뷰는 모든 패키지 및 프로젝트에 대한 매개 변수와 실행 인스턴스에 사용되는 매개 변수 값을 표시합니다.  
  
-   [catalog.object_parameters&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-object-parameters-ssisdb-database.md)  
  
-   [catalog.execution_parameter_values&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)  
  
##  <a name="ServerEnvironments"></a> 서버 환경, 서버 변수 및 서버 환경 참조  
 서버 환경에는 서버 변수가 포함되어 있습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에서 패키지를 실행하거나 유효성을 검사할 때 변수 값을 사용할 수 있습니다.  
  
 다음 저장 프로시저를 사용하여 환경 및 변수에 대한 다른 많은 관리 태스크를 수행할 수 있습니다.  
  
-   [catalog.create_environment&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-ssisdb-database.md)  
  
-   [catalog.delete_environment&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-ssisdb-database.md)  
  
-   [catalog.move_environment&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-move-environment-ssisdb-database.md)  
  
-   [catalog.rename_environment&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-rename-environment-ssisdb-database.md)  
  
-   [catalog.set_environment_property&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-property-ssisdb-database.md)  
  
-   [catalog.create_environment_variable&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-variable-ssisdb-database.md)  
  
-   [catalog.delete_environment_variable&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-variable-ssisdb-database.md)  
  
-   [catalog.set_environment_variable_property&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-property-ssisdb-database.md)  
  
-   [catalog.set_environment_variable_value&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-value-ssisdb-database.md)  
  
 [catalog.set_environment_variable_protection&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-protection-ssisdb-database.md) 저장 프로시저를 호출하여 변수에 대한 민감도 비트를 설정할 수 있습니다.  
  
 서버 변수 값을 사용하려면 프로젝트와 서버 환경 간의 참조를 지정합니다. 다음 저장 프로시저를 사용하여 참조를 만들거나 삭제할 수 있습니다. 환경을 프로젝트와 같은 폴더에서 찾을 수 있는지, 아니면 다른 폴더에서 찾을 수 있는지를 나타낼 수도 있습니다.  
  
-   [catalog.create_environment_reference&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-reference-ssisdb-database.md)  
  
-   [catalog.delete_environment_reference&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-reference-ssisdb-database.md)  
  
-   [catalog.set_environment_reference_type&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-reference-type-ssisdb-database.md)  
  
 환경 및 변수에 대한 자세한 정보를 보려면 이러한 뷰를 쿼리하십시오.  
  
-   [catalog.environments&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-environments-ssisdb-database.md)  
  
-   [catalog.environment_variables&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-environment-variables-ssisdb-database.md)  
  
-   [catalog.environment_references&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-environment-references-ssisdb-database.md)  
  
##  <a name="Executions"></a> 실행 및 유효성 검사  
 실행은 패키지 실행의 인스턴스입니다. 실행을 만들고 시작하려면 [catalog.create_execution&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md) 및 [catalog.start_execution&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)을 호출합니다. 실행 또는 패키지/프로젝트 유효성 검사를 중지하려면 [catalog.stop_operation&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database.md)을 호출합니다.  
  
 실행 중인 패키지를 일시 중지하고 덤프 파일을 만들려면 catalog.create_execution_dump 저장 프로시저를 호출합니다. 덤프 파일은 실행 문제를 해결하는 데 도움이 될 수 있는 패키지 실행에 대한 정보를 제공합니다. 덤프 파일을 생성하고 구성하는 방법은 [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)을 참조하십시오.  
  
 실행, 유효성 검사, 작업 중에 기록되는 메시지 및 오류와 관련된 상황별 정보에 대한 자세한 정보를 보려면 이러한 뷰를 쿼리하십시오.  
  
-   [catalog.executions&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md)  
  
-   [catalog.operations&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)  
  
-   [catalog.operation_messages&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md)  
  
-   [catalog.extended_operation_info&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md)  
  
-   [catalog.event_messages](../../integration-services/system-views/catalog-event-messages.md)  
  
-   [catalog.event_message_context](../../integration-services/system-views/catalog-event-message-context.md)  
  
 [catalog.validate_project&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-validate-project-ssisdb-database.md) 및 [catalog.validate_package&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-validate-package-ssisdb-database.md) 저장 프로시저를 호출하여 프로젝트와 패키지의 유효성을 검사할 수 있습니다. [catalog.validations&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-validations-ssisdb-database.md) 뷰는 유효성 검사에서 고려되는 서버 환경 참조, 유효성 검사가 종속성 유효성 검사인지 또는 전체 유효성 검사인지 여부, 패키지를 실행하는 데 32비트 런타임이 사용되는지 또는 64비트 런타임이 사용되는지 여부 등에 대한 자세한 정보를 제공합니다.  

## <a name="create-the-ssis-catalog"></a>SSIS 카탈로그 만들기
  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 패키지를 디자인하고 테스트한 후에는 이 패키지가 포함된 프로젝트를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포할 수 있습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 프로젝트를 배포하려면 서버에 **SSISDB** 카탈로그가 있어야 합니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 설치 프로그램에서 카탈로그를 자동으로 만들지 않으므로 다음 지침에 따라 카탈로그를 수동으로 만들어야 합니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 SSISDB 카탈로그를 만들 수 있습니다. Windows PowerShell을 사용하여 프로그래밍 방식으로 카탈로그를 만들 수도 있습니다.  
  
### <a name="to-create-the-ssisdb-catalog-in-sql-server-management-studio"></a>SQL Server Management Studio에서 SSISDB 카탈로그를 만들려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 엽니다.  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 엔진에 연결합니다.  
  
3.  개체 탐색기에서 서버 노드를 확장하고 **Integration Services 카탈로그** 노드를 마우스 오른쪽 단추로 클릭한 다음 **카탈로그 만들기**를 클릭합니다.  
  
4.  **CLR 통합 사용**을 클릭합니다.  
  
     카탈로그에 CLR 저장 프로시저가 사용됩니다.  
  
5.  **SQL Server 시작 시 Integration Services 저장 프로시저 자동 실행** 을 클릭하여 [서버 인스턴스를 다시 시작할 때마다](../../integration-services/system-stored-procedures/catalog-startup.md) catalog.startup [!INCLUDE[ssIS](../../includes/ssis-md.md)] 저장 프로시저를 실행하도록 지정합니다.  
  
     저장 프로시저에서는 SSISDB 카탈로그에 대한 작업의 상태를 유지 관리합니다. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 서버 인스턴스가 다운될 때 실행 중이었던 패키지의 상태를 수정합니다.  
  
6.  암호를 입력하고 **확인**을 클릭합니다.  
  
     암호는 카탈로그 데이터를 암호화하는 데 사용되는 데이터베이스 마스터 키를 보호합니다. 암호를 안전한 위치에 저장하십시오. 데이터베이스 마스터 키도 백업하는 것이 좋습니다. 자세한 내용은 [Back Up a Database Master Key](../../relational-databases/security/encryption/back-up-a-database-master-key.md)을 참조하세요.  
  
### <a name="to-create-the-ssisdb-catalog-programmatically"></a>SSISDB 카탈로그를 프로그래밍 방식으로 만들려면  
  
1.  다음 PowerShell 스크립트를 실행합니다.  
  
    ```  
    # Load the IntegrationServices Assembly  
    [Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Management.IntegrationServices")  
  
    # Store the IntegrationServices Assembly namespace to avoid typing it every time  
    $ISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"  
  
    Write-Host "Connecting to server ..."  
  
    # Create a connection to the server  
    $sqlConnectionString = "Data Source=localhost;Initial Catalog=master;Integrated Security=SSPI;"  
    $sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString  
  
    # Create the Integration Services object  
    $integrationServices = New-Object $ISNamespace".IntegrationServices" $sqlConnection  
  
    # Provision a new SSIS Catalog  
    $catalog = New-Object $ISNamespace".Catalog" ($integrationServices, "SSISDB", "P@assword1")  
    $catalog.Create()  
  
    ```  
  
     Windows PowerShell 및 <xref:Microsoft.SqlServer.Management.IntegrationServices> 네임스페이스를 사용하는 방법의 예를 더 보려면 blogs.msdn.com에서 [SQL Server 2012의 SSIS 및 PowerShell](https://go.microsoft.com/fwlink/?LinkId=242539) 블로그 항목을 참조하세요. 네임스페이스 및 코드 예제에 대한 개요는 blogs.msdn.com에서 [SSIS 카탈로그 관리 개체 모델에 대한 이해](https://go.microsoft.com/fwlink/?LinkId=254267)블로그 항목을 참조하십시오.  

## <a name="catalog-properties-dialog-box"></a>카탈로그 속성 대화 상자
  카탈로그 속성 대화 상자를 사용하여 SSISDB 카탈로그를 구성할 수 있습니다. 카탈로그 속성은 중요한 데이터가 암호화되는 방법, 작업 및 프로젝트 버전 관리 데이터가 보존되는 방법 및 유효성 검사 작업의 제한 시간을 정의합니다. SSISDB 카탈로그는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트, 패키지, 매개 변수 및 환경에 대한 중앙 스토리지 및 관리 지점 역할을 합니다.  
  
 또한 `catalog.catalog_properties` 보기에서 카탈로그 속성을 보고 `catalog.configure_catalog` 저장 프로시저를 사용하여 속성을 설정할 수 있습니다. 자세한 내용은 [catalog.catalog_properties&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) 및 [catalog.configure_catalog&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md)를 참조하세요.  
  
 **수행 작업**  
  
-   [카탈로그 속성 대화 상자 열기](#open_dialog)  
  
-   [옵션 구성](#options)  
  
###  <a name="open_dialog"></a> 카탈로그 속성 대화 상자 열기  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]열기  
  
2.  Microsoft SQL Server 데이터베이스 엔진에 연결합니다.  
  
3.  개체 탐색기에서 **Integration Services** 노드를 확장하고 **SSISDB**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
###  <a name="options"></a> 옵션 구성  
  
#### <a name="options"></a>옵션  
 다음 표에서는 대화 상자의 특정 속성과 `catalog.catalog_properties` 보기의 해당 속성에 대해 설명합니다.  
  
|속성 이름(카탈로그 속성 대화 상자)|속성 이름(catalog.catalog_properties 보기)|Description|  
|-----------------------------------------------------|------------------------------------------------------|-----------------|  
|암호화 알고리즘 이름|ENCRYPTION_ALGORITHM|카탈로그의 중요한 매개 변수 값을 암호화하는 데 사용되는 암호화 유형을 지정합니다. 가능한 값은 다음과 같습니다.<br /><br /> DES<br /><br /> TRIPLE_DES<br /><br /> TRIPLE_DES_3KEY<br /><br /> DESPX<br /><br /> AES_128<br /><br /> AES_192<br /><br /> AES_256(기본값)|  
|프로젝트당 최대 버전 수|MAX_PROJECT_VERSIONS|카탈로그에 저장되는 프로젝트 버전 수를 지정합니다. 최대값을 초과하는 오래된 버전의 프로젝트는 프로젝트 버전 정리 작업이 실행될 때 제거됩니다.|  
|주기적으로 로그 정리|OPERATION_CLEANUP_ENABLED|SQL Server 에이전트 작업인 작업 정리가 실행되도록 지정하려면 이 속성을 True로 설정하고, 그렇지 않으면 이 속성을 False로 설정합니다.|  
|보존 기간(일)|RETENTION_WINDOW|허용 가능한 작업 데이터의 최대 수명(일)을 지정합니다. 지정된 일수보다 오래된 데이터는 SQL 에이전트 작업인 작업 정리를 통해 제거됩니다.|  

## <a name="back-up-restore-and-move-the-ssis-catalog"></a>SSIS 카탈로그 백업, 복원 및 이동
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 에는 SSISDB 데이터베이스가 포함되어 있습니다. SSISDB 데이터베이스에서 뷰를 쿼리하여 **SSISDB** 카탈로그에 저장된 개체, 설정 및 작업 데이터를 검사할 수 있습니다. 이 항목에서는 데이터베이스 백업 및 복원에 대한 지침을 제공합니다.  
  
 **SSISDB** 카탈로그는 사용자가 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포한 패키지를 저장합니다. 카탈로그에 대한 자세한 내용은 [SSIS 카탈로그](../../integration-services/catalog/ssis-catalog.md)를 참조하세요.  
  
###  <a name="backup"></a> SSIS 데이터베이스를 백업하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 열고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결합니다.  
  
2.  BACKUP MASTER KEY Transact-SQL 문을 사용하여 SSISDB 데이터베이스에 대한 마스터 키를 백업합니다. 이 키는 사용자가 지정한 파일에 저장됩니다. 암호를 사용하여 파일의 마스터 키를 암호화합니다.  
  
     문에 대한 자세한 내용은 [BACKUP MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/backup-master-key-transact-sql.md)를 참조하세요.  
  
     다음 예에서는 마스터 키를 `c:\temp directory\RCTestInstKey` 파일로 내보냅니다. 마스터 키를 암호화하는 데에는 `LS2Setup!` 암호가 사용되었습니다.  
  
    ```  
    backup master key to file = 'c:\temp\RCTestInstKey'  
           encryption by password = 'LS2Setup!'  
  
    ```  
  
3.  **에서** 데이터베이스 백업 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]대화 상자를 사용하여 SSISDB 데이터베이스를 백업합니다. 자세한 내용은 [방법: 데이터베이스 백업(SQL Server Management Studio)](https://go.microsoft.com/fwlink/?LinkId=231812)을 참조하세요.  
  
4.  다음을 수행하여 ##MS_SSISServerCleanupJobLogin##에 대한 CREATE LOGIN 스크립트를 생성합니다. 자세한 내용은 [CREATE LOGIN&#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)을 참조하세요.  
  
    1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 **보안** 노드를 확장한 후 **로그인** 노드를 확장합니다.  
  
    2.  **##MS_SSISServerCleanupJobLogin##** 을 마우스 오른쪽 단추로 클릭한 후 **로그인 스크립팅** > **CREATE** > **새 쿼리 편집기 창**을 클릭합니다.  
  
5.  SSISDB 카탈로그가 만들어지지 않은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 SSISDB 데이터베이스를 복원할 경우 다음을 수행하여 sp_ssis_startup에 대한 CREATE PROCEDURE 스크립트를 생성합니다. 자세한 내용은 [CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)를 참조하세요.  
  
    1.  개체 탐색기에서 **데이터베이스** 노드를 확장한 후 **master** > **프로그래밍 기능** > **저장 프로시저** 노드를 확장합니다.  
  
    2.  **dbo.sp_ssis_startup**을 마우스 오른쪽 단추로 클릭한 후 **저장 프로시저 스크립팅** > **CREATE** > **새 쿼리 편집기 창**을 클릭합니다.  
  
6.  SQL Server 에이전트가 시작되었는지 확인합니다.  
  
7.  SSISDB 카탈로그가 만들어지지 않은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 SSISDB 데이터베이스를 복원할 경우 다음을 수행하여 SSIS 서버 유지 관리 작업에 대한 스크립트를 생성합니다. 이 스크립트는 SSISDB 카탈로그가 생성될 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에 자동으로 만들어집니다. 이 작업은 보존 기간이 지난 작업 로그를 정리하고 오래된 프로젝트 버전을 제거하는 데 도움을 줍니다.  
  
    1.  개체 탐색기에서 **SQL Server 에이전트** 노드를 확장한 후 **작업** 노드를 확장합니다.  
  
    2.  SSIS 서버 유지 관리 작업을 마우스 오른쪽 단추로 클릭한 후 **작업 스크립팅** > **CREATE** > **새 쿼리 편집기 창**을 클릭합니다.  
  
### <a name="to-restore-the-ssis-database"></a>SSIS 데이터베이스를 복원하려면  
  
1.  SSISDB 카탈로그가 만들어지지 않은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 SSISDB 데이터베이스를 복원할 경우 `sp_configure` 저장 프로시저를 실행하여 CLR(공용 언어 런타임)을 사용하도록 설정합니다. 자세한 내용은 [sp_configure&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 및 [clr enabled 옵션](https://go.microsoft.com/fwlink/?LinkId=231855)을 참조하세요.  
  
    ```  
    use master   
           sp_configure 'clr enabled', 1  
           reconfigure  
  
    ```  
  
2.  SSISDB 카탈로그가 만들어지지 않은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 SSISDB 데이터베이스를 복원할 경우 비대칭 키를 만들고 비대칭 키로부터 로그인한 후 해당 로그인에 UNSAFE 권한을 부여합니다.  
  
    ```  
    Create Asymmetric key MS_SQLEnableSystemAssemblyLoadingKey  
           FROM Executable File = 'C:\Program Files\Microsoft SQL Server\110\DTS\Binn\Microsoft.SqlServer.IntegrationServices.Server.dll'  
  
    ```  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] CLR 저장 프로시저를 사용하려면 해당 로그인에 UNSAFE 권한을 부여해야 합니다. UNSAFE 코드 권한에 대한 자세한 내용은 [Creating an Assembly](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)를 참조하십시오.  
  
    ```  
    Create Login MS_SQLEnableSystemAssemblyLoadingUser  
           FROM Asymmetric key MS_SQLEnableSystemAssemblyLoadingKey   
  
           Grant unsafe Assembly to MS_SQLEnableSystemAssemblyLoadingUser  
  
    ```  
  
3.  **에서** 데이터베이스 복원 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]대화 상자를 사용하여 백업에서 SSISDB 데이터베이스를 복원합니다. 자세한 내용은 아래 항목을 참조하세요.  
  
    -   [데이터베이스 복원&#40;일반 페이지&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)  
  
    -   [데이터베이스 복원&#40;파일 페이지&#41;](../../relational-databases/backup-restore/restore-database-files-page.md)  
  
    -   [데이터베이스 복원&#40;옵션 페이지&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)  
  
4.  [SSIS 데이터베이스를 백업하려면](#backup) 에서 ##MS_SSISServerCleanupJobLogin##, sp_ssis_startup 및 SSIS 서버 유지 관리 작업에 대해 만든 스크립트를 실행합니다. SQL Server 에이전트가 시작되었는지 확인합니다.  
  
5.  다음 문을 실행하여 sp_ssis_startup 프로시저가 자동 실행되도록 설정합니다. 자세한 내용은 [sp_procoption&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-procoption-transact-sql.md)을 참조하세요.  
  
    ```  
    EXEC sp_procoption N'sp_ssis_startup','startup','on'  
    ```  
  
6.  **에서** 로그인 속성 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]대화 상자를 사용하여 SSISDB 사용자 ##MS_SSISServerCleanupJobUser##(SSISDB 데이터베이스)를 ##MS_SSISServerCleanupJobLogin##에 매핑합니다.  
  
7.  다음 방법 중 하나를 사용하여 마스터 키를 복원합니다. 암호화에 대한 자세한 내용은 [Encryption Hierarchy](../../relational-databases/security/encryption/encryption-hierarchy.md)을 참조하십시오.  
  
    -   **메서드 1**  
  
         이미 데이터베이스 마스터 키에 대한 백업을 수행했고 마스터 키를 암호화하기 위해 사용된 암호가 있는 경우 이 방법을 사용합니다.  
  
        ```  
               Restore master key from file = 'c:\temp\RCTestInstKey'  
               Decryption by password = 'LS2Setup!' -- 'Password used to encrypt the master key during SSISDB backup'  
               Encryption by password = 'LS3Setup!' -- 'New Password'  
               Force  
  
        ```  
  
        > [!NOTE]  
        >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정에 백업 키 파일에 대한 읽기 권한이 있는지 확인합니다.  
  
        > [!NOTE]  
        >  데이터베이스 마스터 키가 아직 서비스 마스터 키로 암호화되지 않은 경우 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에 다음과 같은 경고 메시지가 표시됩니다. 경고 메시지를 무시합니다.  
        >   
        >  **현재 마스터 키를 해독할 수 없습니다. FORCE 옵션이 지정되어 있어 오류가 무시되었습니다.**  
        >   
        >  FORCE 인수는 현재 데이터베이스 마스터 키가 열려 있지 않더라도 복원 프로세스가 계속되도록 지정합니다. SSISDB 카탈로그의 경우 사용자가 데이터베이스를 복원 중인 인스턴스에서 데이터베이스 마스터 키가 아직 열려 있지 않으므로 이 메시지가 표시됩니다.  
  
    -   **방법 2**  
  
         SSISDB를 만들기 위해 사용된 원래 암호를 갖고 있는 경우 이 방법을 사용합니다.  
  
        ```  
        open master key decryption by password = 'LS1Setup!' --'Password used when creating SSISDB'  
               Alter Master Key Add encryption by Service Master Key  
        ```  
  
8.  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] catalog.check_schema_version [을 실행하여 SSISDB 카탈로그 스키마와](../../integration-services/system-stored-procedures/catalog-check-schema-version.md)바이너리 파일(ISServerExec 및 SQLCLR 어셈블리)이 호환되는지 여부를 결정합니다.  
  
9. SSISDB 데이터베이스가 성공적으로 복원되었는지 확인하려면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포된 패키지를 실행하는 등 SSISDB 카탈로그에 대해 작업을 수행합니다. 자세한 내용은 [Integration Services(SSIS) 패키지 실행](../../integration-services/packages/run-integration-services-ssis-packages.md)을 참조하세요.  
  
### <a name="to-move-the-ssis-database"></a>SSIS 데이터베이스를 이동하려면  
  
-   사용자 데이터베이스 이동 지침을 따릅니다. 자세한 내용은 [Move User Databases](../../relational-databases/databases/move-user-databases.md)을 참조하세요.  
  
     SSISDB 데이터베이스의 마스터 키를 백업하고 백업 파일을 보호하십시오. 자세한 내용은 [SSIS 데이터베이스를 백업하려면](#backup)을 참조하세요.  
  
     Integration Services(SSIS) 관련 개체가 SSISDB 카탈로그가 아직 만들어지지 않은 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 만들어졌는지 확인합니다.  

## <a name="upgrade-the-ssis-catalog-ssisdb"></a>SSIS 카탈로그(SSISDB) 업그레이드
  데이터베이스가 SQL Server 인스턴스의 최신 버전보다 오래된 상태이면 SSISDB 업그레이드 마법사를 사용하여 SSIS 카탈로그 데이터베이스인 SSISDB를 업그레이드합니다. 다음 조건 중 하나에 해당하는 경우 데이터베이스가 오래되었을 수 있습니다.  
  
-   이전 버전의 SQL Server에서 데이터베이스를 복원한 경우  
  
-   SQL Server 인스턴스를 업그레이드하기 전에 Always On 가용성 그룹에서 데이터베이스를 제거하지 않은 경우. 이 조건에서는 데이터베이스가 자동으로 업그레이드되지 않습니다. 자세한 내용은 [Upgrading SSISDB in an availability group](#Upgrade)를 참조하십시오.  
  
 마법사는 로컬 서버 인스턴스의 데이터베이스만 업그레이드할 수 있습니다.  
  
### <a name="upgrade-the-ssis-catalog-ssisdb-by-running-the-ssisdb-upgrade-wizard"></a>SSISDB 업그레이드 마법사를 실행하여 SSIS 카탈로그(SSISDB) 업그레이드  
  
1.  SSIS 카탈로그 데이터베이스(SSISDB)를 백업합니다.  
  
2.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 로컬 서버와 **Integration Services 카탈로그**를 차례로 확장합니다.  
  
3.  **SSISDB**를 마우스 오른쪽 단추로 클릭하고 **데이터베이스 업그레이드** 를 선택하여 SSISDB 업그레이드 마법사를 시작합니다. 또는 로컬 서버의 관리자 권한으로 `C:\Program Files\Microsoft SQL Server\140\DTS\Binn\ISDBUpgradeWizard.exe`를 실행하여 SSISDB 업그레이드 마법사를 시작합니다.
  
     ![SSISDB 업그레이드 마법사 시작](../../integration-services/service/media/ssisdb-upgrade-wizard-1.png)

4.  **인스턴스 선택** 페이지에서 로컬 서버의 SQL Server 인스턴스를 선택합니다.  
  
    > [!IMPORTANT]  
    >  마법사는 로컬 서버 인스턴스의 데이터베이스만 업그레이드할 수 있습니다.  
  
     마법사를 실행하기 전에 SSISDB 데이터베이스를 백업했음을 나타내는 확인란을 선택합니다.  
  
     ![SSISDB 업그레이드 마법사에서 서버 선택](../../integration-services/service/media/ssisdb-upgrade-wizard-2.png "SSISDB 업그레이드 마법사에서 서버 선택")  
  
5.  **업그레이드** 를 선택하여 SSIS 카탈로그 데이터베이스를 업그레이드합니다.  
  
6.  **결과** 페이지에서 결과를 검토합니다.  
  
     ![SSISDB 업그레이드 마법사에서 결과 검토](../../integration-services/service/media/ssisdb-upgrade-wizard-3.png "SSISDB 업그레이드 마법사에서 결과 검토")  

## <a name="always-on-for-ssis-catalog-ssisdb"></a>SSIS 카탈로그에 대한 Always On(SSISDB)
  Always On 가용성 그룹 기능은 데이터베이스 미러링에 대한 엔터프라이즈 수준의 대안을 제공하는 고가용성 및 재해 복구 솔루션입니다. 가용성 그룹은 함께 장애 조치(Failover)되는 사용자 데이터베이스(가용성 데이터베이스라고 함)의 불연속 집합에 대한 장애 조치(Failover) 환경을 지원합니다. 자세한 내용은 [Always On 가용성 그룹](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)을 참조하세요.  
  
 SSIS 카탈로그(SSISDB) 및 해당 콘텐츠(프로젝트, 패키지, 실행 로그 등)에 대한 고가용성을 제공하기 위해 Always On 가용성 그룹에 SSISDB 데이터베이스(다른 사용자 데이터베이스와 동일하게)를 추가할 수 있습니다. 장애 조치(Failover)가 발생하면 보조 노드 중 하나가 자동으로 새 주 노드가 됩니다.  
 
 > [!IMPORTANT]
 > 장애 조치(failover)가 수행될 경우 실행 중이던 패키지가 다시 시작되지 않습니다. 
 
 **섹션 내용**  
  
1.  [필수 구성 요소](#prereq)  
  
2.  [Always On에 대한 SSIS 지원 구성](#Firsttime)  
  
3.  [가용성 그룹에서 SSISDB 업그레이드](#Upgrade)  
  
###  <a name="prereq"></a> 필수 조건  
SSISDB 데이터베이스에 대한 Always On 지원을 활성화하기 전에 다음 필수 구성 요소를 수행합니다.  
  
1.  Windows 장애 조치(Failover) 클러스터를 설정합니다. 지침은 [Windows Server 2012용 장애 조치(Failover) 클러스터 기능 및 도구 설치](https://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) 블로그 게시물을 참조하세요. 모든 클러스터 노드에 기능 및 도구를 설치합니다.  
  
2.  클러스터의 각 노드에 Integration Services 기능이 포함된 SQL Server 2016(SSIS)을 설치합니다.  
  
3.  각 SQL Server 인스턴스에 대해 Always On 가용성 그룹을 사용하도록 설정합니다. 자세한 내용은 [Always On 가용성 그룹 활성화](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md) 를 참조하세요.  
  
###  <a name="Firsttime"></a> Always On에 대한 SSIS 지원 구성  
  
-   [1단계: Integration Services 카탈로그 만들기](#Step1)  
  
-   [2단계: Always On 가용성 그룹에 SSISDB 추가](#Step2)  
  
-   [3단계: Always On에 대한 SSIS 지원 활성화](#Step3)  
  
> [!IMPORTANT]  
> -   가용성 그룹의 **주 노드** 에서 이러한 단계를 수행해야 합니다.
> -   Always On 가용성 그룹에 SSISDB를 추가한 ‘후’ **Always On에 대한 SSIS 지원**을 사용하도록 설정해야 합니다.   

> [!NOTE]
> 이 절차에 대한 자세한 내용은 데이터 플랫폼 MVP Marcos Freccia의 추가 스크린 샷이 포함된 다음 연습을 참조하세요. [SQL Server 2016용 AG에 SSISDB 추가](https://marcosfreccia.com/2017/04/28/adding-ssisdb-to-ag-for-sql-server-2016/).

####  <a name="Step1"></a> 1단계: Integration Services 카탈로그 만들기  
  
1.  **SQL Server Management Studio** 를 시작하고 SSISDB에 대한 Always On 고가용성 그룹의 **주 노드** 로 설정하려는 클러스터의 SQL Server 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 서버 노드를 확장하고 **Integration Services 카탈로그** 노드를 마우스 오른쪽 단추로 클릭한 다음 **카탈로그 만들기**를 클릭합니다.  
  
3.  **CLR 통합 사용**을 클릭합니다. 카탈로그에 CLR 저장 프로시저가 사용됩니다.  
  
4.  **SQL Server 시작 시 Integration Services 저장 프로시저 자동 실행** 을 클릭하여 SSIS 서버 인스턴스를 다시 시작할 때마다 [catalog.startup](../system-stored-procedures/catalog-startup.md) 저장 프로시저를 실행하도록 지정합니다. 저장 프로시저에서는 SSISDB 카탈로그에 대한 작업의 상태를 유지 관리합니다. SSIS 서버 인스턴스가 다운될 때 실행 중이었던 패키지의 상태를 수정합니다.  
  
5.  **암호**를 입력하고 **확인**을 클릭합니다. 암호는 카탈로그 데이터를 암호화하는 데 사용되는 데이터베이스 마스터 키를 보호합니다. 암호를 안전한 위치에 저장하십시오. 데이터베이스 마스터 키도 백업하는 것이 좋습니다. 자세한 내용은 [Back Up a Database Master Key](../../relational-databases/security/encryption/back-up-a-database-master-key.md)을 참조하세요.  
  
####  <a name="Step2"></a> 2단계: Always On 가용성 그룹에 SSISDB 추가  
Always On 가용성 그룹에 SSISDB 데이터베이스를 추가하는 것은 가용성 그룹에 다른 사용자 데이터베이스를 추가하는 것과 거의 동일합니다. [가용성 그룹 마법사 사용](../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)을 참조하세요.  
  
**새 가용성 그룹** 마법사의 **데이터베이스 선택** 페이지에서 SSIS 카탈로그를 만드는 동안 지정한 암호를 제공합니다.

![새 가용성 그룹](../../integration-services/service/media/ssis-newavailabilitygroup.png "데이터베이스 선택")  
  
####  <a name="Step3"></a> 3단계: Always On에 대한 SSIS 지원 활성화  
 통합 서비스 카탈로그를 만든 후 **통합 서비스 카탈로그** 노드를 마우스 오른쪽 단추로 클릭하고 **Always On 지원 활성화**를 클릭합니다. 다음 **Always On에 대한 지원 활성화** 대화 상자를 참조해야 합니다. 이 메뉴 항목이 비활성화된 경우 모든 필수 구성 요소를 설치했는지 확인하고 **새로 고침**을 클릭합니다.  
  
 ![Always On에 대한 지원 활성화](../../integration-services/service/media/ssis-enablesupportforalwayson.png)  
  
> [!WARNING]  
>  Always On에 대한 SSIS 지원을 활성화할 때까지 SSISDB 데이터베이스의 자동 장애 조치(Failover)는 지원되지 않습니다.  
  
 Always On 가용성 그룹에서 새로 추가된 보조 복제본이 테이블에 표시됩니다. 목록에서 각 복제본에 대한 **연결...** 단추를 클릭하고 인증 자격 증명을 입력하여 복제본에 연결합니다. 사용자 계정은 Always On에 대한 SSIS 지원을 활성화하도록 각 복제본에서 sysadmin 그룹의 구성원이어야 합니다. 각 복제본에 성공적으로 연결한 후 **확인** 을 클릭하여 Always On에 대한 SSIS 지원을 활성화합니다.  
 
다른 필수 조건을 완료한 후 상황에 맞는 메뉴의 **Always On 지원 활성화** 옵션이 비활성화된 것으로 나타나는 경우 다음을 시도해 봅니다.
1.  **새로 고침** 옵션을 클릭하여 상황에 맞는 메뉴를 새로 고칩니다.
2.  주 노드에 연결되는지 확인합니다. 주 노드에서 Always On 지원을 사용하도록 설정해야 합니다.
3.  SQL Server 버전이 13.0 이상인지 확인합니다. SSIS는 SQL Server 2016 이상 버전에 대해서만 Always On을 지원합니다.

###  <a name="Upgrade"></a> 가용성 그룹에서 SSISDB 업그레이드  
 이전 버전에서 SQL Server를 업그레이드하고 SSISDB가 Always On 가용성 그룹에 있는 경우 업그레이드는 "Always On 가용성 그룹의 SSISDB 검사" 규칙에 따라 차단될 수 있습니다. 이 차단은 업그레이드는 단일 사용자 모드에서 실행되는 반면 가용성 데이터베이스는 다중 사용자 데이터베이스여야 하기 때문에 발생합니다. 따라서 업그레이드 또는 패치되는 동안 SSISDB를 포함하는 모든 가용성 데이터베이스는 오프라인으로 전환되고 업그레이드 또는 패치되지 않습니다. 업그레이드를 계속하려면 먼저 가용성 그룹에서 SSISDB를 제거한 다음 각 노드를 업그레이드 또는 패치하고 가용성 그룹에 SSISDB를 다시 추가합니다.  
  
 “Always On 가용성 그룹의 SSISDB 검사” 규칙에 따라 차단되는 경우 SQL Server를 업그레이드하려면 이러한 단계를 따릅니다.  
  
1.  가용성 그룹에서 SSISDB 데이터베이스를 제거합니다. 자세한 내용은 [가용성 그룹에서 보조 데이터베이스 제거&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md) 및 [가용성 그룹에서 주 데이터베이스 제거&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md)를 참조하세요.  
  
2.  업그레이드 마법사에서 **다시 실행**을 클릭합니다. “Always On 가용성 그룹의 SSISDB 검사” 규칙을 통과합니다.  
  
3.  **다음** 을 클릭하여 업그레이드를 계속합니다.  
  
4.  모든 노드를 업그레이드한 후 Always On 가용성 그룹에 SSISDB 데이터베이스를 다시 추가합니다. 자세한 내용은 [가용성 그룹에 데이터베이스 추가&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/availability-group-add-a-database.md)를 참조하세요.  
  
 SQL Server를 업그레이드할 때 차단되지 않고 SSISDB가 Always On 가용성 그룹에 있는 경우 SQL Server 데이터베이스 엔진을 업그레이드한 후 SSISDB를 개별적으로 업그레이드해야 합니다. 다음 절차에 설명된 대로 SSIS 업그레이드 마법사를 사용하여 SSISDB를 업그레이드합니다.  
  
1.  SSISDB가 가용성 그룹의 유일한 데이터베이스인 경우 가용성 그룹에서 SSISDB 데이터베이스를 이동하거나 가용성 그룹을 삭제합니다. 이 작업을 수행하려면 가용성 그룹의 **주 노드**에서 **SQL Server Management Studio**를 시작합니다.  
  
2.  모든 **복제본 노드**에서 SSISDB 데이터베이스를 제거합니다.  
  
3.  **주 노드**에서 SSISDB 데이터베이스를 업그레이드합니다. SQL Server Management Studio의**개체 탐색기** 에서 **Integration Services 카탈로그**를 확장하고 **SSISDB**를 마우스 오른쪽 단추로 클릭한 다음 **데이터베이스 업그레이드**를 선택합니다. 데이터베이스를 업그레이드하려면 **SSISDB 업그레이드 마법사** 의 지침을 따릅니다. **주 노드**에서 **SSIDB 업그레이드 마법사**를 로컬로 시작합니다.  
  
4.  [2단계: Always On 가용성 그룹에 SSISDB 추가](#Step2)의 지침에 따라 가용성 그룹에 SSISDB를 다시 추가합니다.  
  
5.  [3단계: Always On에 대한 SSIS 지원 활성화](#Step3)의 지침을 따릅니다.  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   blogs.msdn.com의 블로그 항목 - [SQL Server 2012의 SSIS 및 PowerShell](https://go.microsoft.com/fwlink/?LinkId=242539)  
  
-   blogs.msdn.com의 블로그 항목 - [SSIS 카탈로그 액세스 제어 팁](https://go.microsoft.com/fwlink/?LinkId=246669)  
  
-   blogs.msdn.com의 블로그 항목 - [SSIS 카탈로그 관리 개체 모델에 대한 이해](https://go.microsoft.com/fwlink/?LinkId=254267)  
