---
title: OLE DB 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.oledbconnection.f1
helpviewer_keywords:
- OLE DB connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], OLE DB
- connections [Integration Services], OLE DB
ms.assetid: 91e3622e-4b1a-439a-80c7-a00b90d66979
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c455e449ff59296848c7e3f15d07aaee80d415c7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66221152"
---
# <a name="ole-db-connection-manager"></a>OLE DB 연결 관리자

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  OLE DB 연결 관리자를 사용하면 패키지에서 OLE DB Provider를 사용하여 데이터 원본에 연결할 수 있습니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결되는 OLE DB 연결 관리자에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 사용할 수 있습니다.    
    
> [!NOTE]
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 11.0 OLEDB 공급자는 다중 서브넷 장애 조치(Failover) 클러스터링에 대한 새 연결 문자열 키워드(MultiSubnetFailover=True)를 지원하지 않습니다. 자세한 내용은 [SQL Server 릴리스 정보](https://go.microsoft.com/fwlink/?LinkId=247824) 및 www.mattmasson.com의 블로그 게시물, [Always On 다중 서브넷 장애 조치(Failover) 및 SSIS](https://www.mattmasson.com/2012/03/alwayson-multi-subnet-failover-and-ssis/)를 참조하세요.    
> 
> [!NOTE]
>  데이터 원본이 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007인 경우 이 데이터 원본에는 이전 버전의 Excel 또는 Access와 다른 데이터 공급자가 필요합니다. 자세한 내용은 [Excel 통합 문서에 연결](../../integration-services/connection-manager/connect-to-an-excel-workbook.md) 및 [Access 데이터베이스에 연결](../../integration-services/connection-manager/connect-to-an-access-database.md)을 참조하세요.    
    
 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 태스크와 데이터 흐름 구성 요소에서는 OLE DB 연결 관리자가 사용됩니다. 예를 들어 OLE DB 원본과 OLE DB 대상에서는 이 연결 관리자를 사용하여 데이터를 추출 및 로드하고, SQL 실행 태스크에서는 이 연결 관리자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결하고 쿼리를 실행합니다.    
    
 OLE DB 연결 관리자는 또한 C++와 같은 언어를 사용하는 비관리 코드로 작성된 사용자 지정 태스크의 OLE DB 데이터 원본에 액세스하는 데에도 사용됩니다.    
    
 패키지에 OLE DB 연결 관리자를 추가하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 런타임에 OLE DB 연결로 확인되는 연결 관리자를 만들고, 연결 관리자 속성을 설정하고, 연결 관리자를 패키지의 **Connections** 컬렉션에 추가합니다.    
    
 연결 관리자의 **ConnectionManagerType** 속성이 **OLEDB**로 설정됩니다.    
    
 다음과 같은 방법으로 OLE DB 연결 관리자를 구성할 수 있습니다.    
    
-   선택된 공급자에 대한 요구 사항을 만족하도록 구성된 특정 연결 문자열을 제공합니다.    
    
-   공급자에 따라 연결할 데이터 원본의 이름을 포함시킵니다.    
    
-   선택된 공급자에 적합한 보안 자격 증명을 제공합니다.    
    
-   연결 관리자에서 만든 연결이 런타임에 유지될지 여부를 나타냅니다.    
    
## <a name="logging"></a>로깅    
 OLE DB 연결 관리자가 외부 데이터 공급자에 대해 수행하는 호출을 로깅할 수 있습니다. 이 로깅 기능을 사용하여 OLE DB 연결 관리자가 수행하는 외부 데이터 원본에 대한 연결 문제를 해결할 수 있습니다. OLE DB 연결 관리자가 외부 데이터 공급자에 대해 수행하는 호출을 로깅하려면 패키지 로깅을 설정하고 패키지 수준에서 **Diagnostic** 이벤트를 선택합니다. 자세한 내용은 [패키지 실행 문제 해결 도구](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)를 참조하세요.    
    
## <a name="configuration-of-the-oledb-connection-manager"></a>OLEDB 연결 관리자 구성    
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 [OLE DB 연결 관리자 구성](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)을 참조하세요. 프로그래밍 방식으로 연결 관리자를 구성하는 방법은 개발자 가이드에서 **T:Microsoft.SqlServer.Dts.Runtime.ConnectionManager** 클래스에 대한 설명서를 참조하십시오.    
    
## <a name="related-content"></a>관련 내용    
    
-   social.technet.microsoft.com의 Wiki 문서 - [Oracle 커넥터가 있는 SSIS](https://go.microsoft.com/fwlink/?LinkId=220670)    
    
-   carlprothman.net의 기술 문서 [OLE DB 공급자에 대한 연결 문자열](https://go.microsoft.com/fwlink/?LinkId=220744)    
    
## <a name="configure-ole-db-connection-manager"></a>OLE DB 연결 관리자 구성
  **OLE DB 연결 관리자 구성** 대화 상자를 사용하면 새 연결을 만들거나 기존 연결을 복사하여 데이터 원본에 대한 연결을 추가할 수 있습니다.  
  
> [!NOTE]  
>  데이터 원본이 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007인 경우 이 데이터 원본에는 이전 버전의 Excel과 다른 연결 관리자가 필요합니다. 자세한 내용은 [Excel 통합 문서에 연결](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)을 참조하세요.  
>   
>  데이터 원본이 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007인 경우 이 데이터 원본에는 이전 버전의 Access와 다른 OLE DB 공급자가 필요합니다. 자세한 내용은 [Access 데이터베이스에 연결](../../integration-services/connection-manager/connect-to-an-access-database.md)을 참조하세요.  
  
 OLE DB 연결 관리자에 대한 자세한 내용은 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)를 참조하십시오.  
  
### <a name="options"></a>옵션  
 **데이터 연결**  
 목록에서 기존 OLE DB 데이터 연결을 선택합니다.  
  
 **데이터 연결 속성**  
 선택한 OLE DB 데이터 연결의 속성과 값을 표시합니다.  
  
 **새로 만들기**  
 **연결 관리자** 대화 상자를 사용하여 OLE DB 데이터 연결을 만듭니다.  
  
 **Delete**  
 데이터 연결을 선택한 다음 **삭제** 단추를 사용하여 삭제합니다.  
  
### <a name="managed-identities-for-azure-resources-authentication"></a>Azure 리소스 인증을 위한 관리 ID
[Azure Data Factory의 Azure-SSIS 통합 런타임](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime)에 대해 SSIS 패키지를 실행하는 경우 Azure SQL Database(또는 Managed Instance) 인증을 위해 데이터 팩터리와 연결된 [관리 ID](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-database#managed-identity)를 사용할 수 있습니다. 지정된 팩터리는 이 ID를 사용하여 데이터베이스에 액세스하고 해당 데이터베이스에 대해 데이터를 복사할 수 있습니다.

Azure SQL Database에 대해 관리 ID 인증을 사용하려면 아래 단계를 수행하여 데이터베이스를 구성합니다.

1. **Azure AD에 그룹을 만듭니다.** 관리 ID를 그룹의 멤버로 만듭니다.
    
   1. [Azure Portal에서 데이터 팩터리 관리 ID를 찾습니다](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity). 데이터 팩터리의 **속성**으로 이동합니다. **관리 ID 개체 ID**를 복사합니다.
    
   1. [Azure AD PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2) 모듈을 설치합니다. `Connect-AzureAD` 명령을 사용하여 로그인합니다. 다음 명령을 실행하여 그룹을 만들고 관리 ID를 멤버로 추가합니다.
      ```powershell
      $Group = New-AzureADGroup -DisplayName "<your group name>" -MailEnabled $false -SecurityEnabled $true -MailNickName "NotSet"
      Add-AzureAdGroupMember -ObjectId $Group.ObjectId -RefObjectId "<your data factory managed identity object ID>"
      ```
    
1. 아직 수행하지 않은 경우 Azure Portal에서 Azure SQL Server에 대해 **[Azure Active Directory 관리자를 프로비저닝](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-azure-sql-database-server)** 합니다. Azure AD 관리자는 Azure AD 사용자 또는 Azure AD 그룹이 될 수 있습니다. 관리 ID를 가진 그룹에 관리자 역할을 부여하는 경우 3단계 및 4단계를 건너뛰세요. 관리자는 데이터베이스에 대한 전체 액세스 권한을 가집니다.

1. Azure AD 그룹에 대해 **[포함된 데이터베이스 사용자를 만듭니다](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#create-contained-database-users-in-your-database-mapped-to-azure-ad-identities)** . ALTER ANY USER 이상의 사용 권한을 가진 Azure AD ID를 통해 SSMS와 같은 도구를 사용하여 데이터를 복사하려는 데이터베이스에 연결합니다. 다음 T-SQL을 실행합니다. 
    
    ```sql
    CREATE USER [your AAD group name] FROM EXTERNAL PROVIDER;
    ```

1. SQL 사용자 및 다른 사용자에 대해 일반적으로 수행하는 것처럼 **Azure AD에 필요한 사용 권한을 부여**합니다. 예를 들어 다음 코드를 실행합니다.

    ```sql
    ALTER ROLE [role name] ADD MEMBER [your AAD group name];
    ```

Azure SQL Database Managed Instance에 대해 관리 ID 인증을 사용하려면 아래 단계를 수행하여 데이터베이스를 구성합니다.
    
1. 아직 수행하지 않은 경우 Azure Portal에서 관리형 인스턴스에 대해 **[Azure Active Directory 관리자를 프로비저닝](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-managed-instance)** 합니다. Azure AD 관리자는 Azure AD 사용자 또는 Azure AD 그룹이 될 수 있습니다. 관리 ID를 가진 그룹에 관리자 역할을 부여하는 경우 2단계~5단계를 건너뛰세요. 관리자는 데이터베이스에 대한 전체 액세스 권한을 가집니다.

1. **[Azure Portal에서 데이터 팩터리 관리 ID를 찾습니다](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity)** . 데이터 팩터리의 **속성**으로 이동합니다. **관리 ID 애플리케이션 ID**(**관리 ID 개체 ID**가 아닌)를 복사합니다.

1. **데이터 팩터리 관리 ID를 이진 형식으로 변환합니다**. SQL/Active Directory 관리자 계정을 통해 SSMS와 같은 도구를 사용하여 관리형 인스턴스의 **마스터** 데이터베이스에 연결합니다. **마스터** 데이터베이스에 대해 다음 T-SQL을 실행하여 관리 ID 애플리케이션 ID를 이진 형식으로 가져옵니다.
    
    ```sql
    DECLARE @applicationId uniqueidentifier = '{your managed identity application ID}'
    select CAST(@applicationId AS varbinary)
    ```

1. Azure SQL Database Managed Instance에서 **데이터 팩터리 관리 ID를 사용자로 추가**합니다. **마스터** 데이터베이스에 대해 다음 T-SQL을 실행합니다.
    
    ```sql
    CREATE LOGIN [{a name for the managed identity}] FROM EXTERNAL PROVIDER with SID = {your managed identity application ID as binary}, TYPE = E
    ```

1. **데이터 팩터리 관리 ID에 필요한 사용 권한을 부여합니다**. 데이터를 복사할 데이터베이스에 대해 다음 T-SQL을 실행합니다.

    ```sql
    CREATE USER [{the managed identity name}] FOR LOGIN [{the managed identity name}] WITH DEFAULT_SCHEMA = dbo
    ALTER ROLE db_owner ADD MEMBER [{the managed identity name}]
    ```

그런 다음, OLE DB 연결 관리자를 위해 **OLE DB 공급자**를 구성합니다. 이 작업을 수행하는 두 가지 옵션이 있습니다.
    
1. 디자인 타임에 구성합니다. SSIS 디자이너에서 OLE DB 연결 관리자를 두 번 클릭하여 **연결 관리자** 창을 엽니다. **공급자** 드롭다운 목록에서 [**Microsoft OLE DB Driver for SQL Server**](https://go.microsoft.com/fwlink/?linkid=871294)를 선택합니다.
    > [!NOTE]
    >  드롭다운 목록의 다른 공급자는 관리 ID 인증을 지원하지 않을 수 있습니다.
    
1. 런타임에 구성합니다. [SSMS(SQL Server Management Studio)](https://docs.microsoft.com/sql/integration-services/ssis-quickstart-run-ssms) 또는 [Azure Data Factory SSIS 패키지 실행 작업](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity)을 통해 OLE DB 연결 관리자에 대한 **ConnectionString**를 찾고 연결 속성 **공급자**를 **MSOLEDBSQL**(즉, Microsoft OLE DB Driver for SQL Server)로 설정합니다.
    ```vb
    Data Source=serverName;Initial Catalog=databaseName;Provider=MSOLEDBSQL;...
    ```

끝으로, OLE DB 연결 관리자에 대해 **관리 ID 인증을 구성**합니다. 이 작업을 수행하는 두 가지 옵션이 있습니다.
    
1. 디자인 타임에 구성합니다. SSIS 디자이너에서 OLE DB 연결 관리자를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭하여 **속성 창**을 엽니다. 속성 **ConnectUsingManagedIdentity**를 **True**로 업데이트합니다.
    > [!NOTE]
    >  현재 연결 관리자 속성 **ConnectUsingManagedIdentity**는 SSIS Designer 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server에서 SSIS 패키지를 실행하는 경우 적용되지 않습니다(관리 ID 인증이 작동하지 않음).

1. 런타임에 구성합니다. SSMS 또는 SQL 패키지 실행 작업을 통해 패키지를 실행하는 경우 OLE DB 연결 관리자를 찾아 해당 속성 **ConnectUsingManagedIdentity**를 **True**로 설정합니다.
    > [!NOTE]
    >  Azure-SSIS 통합 런타임에서 OLE DB 연결 관리자에 미리 구성된 모든 다른 인증 방법(예: 통합 보안, 암호)은 관리 ID 인증을 사용하여 데이터베이스 연결을 설정하는 데 사용되는 경우 **재정의**됩니다.

> [!NOTE]
>  기존 패키지에서 관리 ID 인증을 구성하려면 새 연결 관리자 속성 **ConnectUsingManagedIdentity**가 SSIS 프로젝트의 모든 OLE DB 연결 관리자에 자동으로 추가되도록 적어도 [최신 SSIS 디자이너](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)를 한 번 이상 사용하여 SSIS 프로젝트를 다시 빌드하고 해당 SSIS 프로젝트를 Azure-SSIS 통합 런타임에 다시 배포해야 합니다.

## <a name="see-also"></a>참고 항목    
 [OLE DB 원본](../../integration-services/data-flow/ole-db-source.md)     
 [OLE DB 대상](../../integration-services/data-flow/ole-db-destination.md)     
 [SQL 실행 태스크](../../integration-services/control-flow/execute-sql-task.md)     
 [Integration Services&#40;SSIS&#41; 연결](../../integration-services/connection-manager/integration-services-ssis-connections.md)    
    
  
