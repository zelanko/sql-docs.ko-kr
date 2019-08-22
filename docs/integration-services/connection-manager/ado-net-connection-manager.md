---
title: ADO.NET 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.adonetconnection.f1
helpviewer_keywords:
- connection managers [Integration Services], ADO.NET
- ADO.NET connection manager [Integration Services]
- connections [Integration Services], ADO.NET
ms.assetid: fc5daa2f-0159-4bda-9402-c87f1035a96f
author: janinezhang
ms.author: janinez
ms.openlocfilehash: b3856f1f651db485aa9e54758c2d2a92ebf2ea0a
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028779"
---
# <a name="adonet-connection-manager"></a>ADO.NET 연결 관리자

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 사용하면 패키지에서 .NET 공급자를 사용하여 데이터 원본에 액세스할 수 있습니다. 이 연결 관리자는 일반적으로 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 같은 데이터 원본에 액세스하는 데 사용되며, C#과 같은 언어를 사용하여 관리 코드로 작성된 사용자 지정 태스크의 OLE DB 및 XML로 제공되는 데이터 원본에 액세스하는 데에도 사용됩니다.  
  
 패키지에 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 추가하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 런타임에 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결로 확인되는 연결 관리자를 만들고, 연결 관리자 속성을 설정하며, 연결 관리자를 패키지의 **Connections** 컬렉션에 추가합니다.  
  
 연결 관리자의 **ConnectionManagerType** 속성이 **ADO.NET**로 설정됩니다. **ConnectionManagerType** 의 값은 연결 관리자에서 사용되는 .NET 공급자 이름이 포함되도록 한정됩니다.  
  
## <a name="adonet-connection-manager-troubleshooting"></a>ADO.NET 연결 관리자 문제 해결  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자가 외부 데이터 공급자에 대해 수행하는 호출을 로깅할 수 있습니다. 이 로깅 기능을 사용하여 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자가 수행하는 외부 데이터 원본에 대한 연결 문제를 해결할 수 있습니다. [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자가 외부 데이터 공급자에 대해 수행하는 호출을 로깅하려면 패키지 로깅을 설정하고 패키지 수준에서 **Diagnostic** 이벤트를 선택합니다. 자세한 내용은 [패키지 실행 문제 해결 도구](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)를 참조하세요.  
  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자에서 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 날짜 데이터 형식의 데이터를 읽으면 다음 표에 표시된 결과가 생성됩니다.  
  
|SQL Server 데이터 형식|결과|  
|--------------------------|------------|  
|**time**, **datetimeoffset**|매개 변수가 있는 SQL 명령이 패키지에 사용되지 않을 경우 패키지가 실패합니다. 매개 변수가 있는 SQL 명령을 사용하려면 패키지에서 SQL 실행 태스크를 사용하십시오. 자세한 내용은 [SQL 실행 태스크](../../integration-services/control-flow/execute-sql-task.md) 및 [SQL 실행 태스크의 매개 변수 및 반환 코드](https://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663)를 참조하세요.|  
|**datetime2**|[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자가 밀리초 값을 자릅니다.|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 및 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식에 매핑하는 방법에 대한 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md) 및 [Integration Services 데이터 형식](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
## <a name="adonet-connection-manager-configuration"></a>ADO.NET 연결 관리자 구성  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자는 다음과 같은 방법으로 구성할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
-   선택된 .NET 공급자에 대한 요구 사항을 만족하도록 구성된 특정 연결 문자열을 제공합니다.  
  
-   공급자에 따라 연결할 데이터 원본의 이름을 포함시킵니다.  
  
-   선택된 공급자에 적합한 보안 자격 증명을 제공합니다.  
  
-   연결 관리자에서 만든 연결이 런타임에 유지될지 여부를 나타냅니다.  
  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자의 여러 구성 옵션은 연결 관리자에서 사용되는 .NET 공급자에 따라 달라집니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [ADO.NET 연결 관리자 구성](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)로 설정됩니다.  
  
## <a name="configure-adonet-connection-manager"></a>ADO.NET 연결 관리자 구성
  **ADO.NET 연결 관리자 구성** 대화 상자를 사용하여 SqlClient 공급자와 같은 .NET Framework 데이터 공급자를 사용하여 액세스할 수 있는 데이터 원본에 연결을 추가할 수 있습니다. 연결 관리자는 기존 연결을 사용하거나 새 연결을 만들 수 있습니다.  
  
 ADO.NET 연결 관리자에 대한 자세한 내용은 [ADO.NET Connection Manager](../../integration-services/connection-manager/ado-net-connection-manager.md)를 참조하십시오.  
  
### <a name="options"></a>옵션  
 **데이터 연결**  
 목록에서 기존 ADO.NET 데이터 연결을 선택합니다.  
  
 **데이터 연결 속성**  
 선택한 ADO.NET 데이터 연결의 속성과 값을 봅니다.  
  
 **새로 만들기**  
 **연결 관리자** 대화 상자를 사용하여 ADO.NET 데이터 연결을 만듭니다.  
  
 **Delete**  
 연결을 선택한 다음 **삭제** 단추를 사용하여 삭제합니다.  
  
### <a name="managed-identities-for-azure-resources-authentication"></a>Azure 리소스 인증을 위한 관리 ID
[Azure Data Factory의 Azure-SSIS 통합 런타임](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime)에 대해 SSIS 패키지를 실행하는 경우 Azure SQL Database(또는 Managed Instance) 인증을 위해 데이터 팩터리와 연결된 [관리 ID](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-database#managed-identity)를 사용할 수 있습니다. 지정된 팩터리는 이 ID를 사용하여 데이터베이스에 액세스하고 해당 데이터베이스에 대해 데이터를 복사할 수 있습니다.

> [!NOTE]
>  Azure AD 인증(관리 ID 인증 포함)을 사용하여 Azure SQL Database(또는 Managed Instance)에 연결하는 경우 패키지 실행 실패 또는 예기치 않은 동작 변경을 야기할 수 있는 알려진 이슈가 발생합니다. 자세한 내용은 [Azure AD 기능 및 제한](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication#azure-ad-features-and-limitations)을 참조하세요.

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

1. SQL 사용자 및 다른 사용자에 대해 일반적으로 수행하는 것처럼 **Azure AD에 필요한 사용 권한을 부여**합니다. 해당 역할에 대해서는 [데이터베이스 수준 역할](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles)을 참조하세요. 예를 들어 다음 코드를 실행합니다.

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

1. **데이터 팩터리 관리 ID에 필요한 사용 권한을 부여합니다**. 해당 역할에 대해서는 [데이터베이스 수준 역할](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles)을 참조하세요. 데이터를 복사할 데이터베이스에 대해 다음 T-SQL을 실행합니다.

    ```sql
    CREATE USER [{the managed identity name}] FOR LOGIN [{the managed identity name}] WITH DEFAULT_SCHEMA = dbo
    ALTER ROLE [role name] ADD MEMBER [{the managed identity name}]
    ```

끝으로, ADO.NET 연결 관리자에 대해 **관리 ID 인증을 구성**합니다. 이 작업을 수행하는 두 가지 옵션이 있습니다.
    
1. 디자인 타임에 구성합니다. SSIS 디자이너에서 ADO.NET 연결 관리자를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭하여 **속성 창**을 엽니다. 속성 **ConnectUsingManagedIdentity**를 **True**로 업데이트합니다.
    > [!NOTE]
    >  현재 연결 관리자 속성 **ConnectUsingManagedIdentity**는 SSIS Designer 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server에서 SSIS 패키지를 실행하는 경우 적용되지 않습니다(관리 ID 인증이 작동하지 않음).
    
1. 런타임에 구성합니다. [SSMS(SQL Server Management Studio)](https://docs.microsoft.com/sql/integration-services/ssis-quickstart-run-ssms) 또는 [Azure Data Factory SSIS 패키지 작업 실행](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity)을 통해 패키지를 실행하는 경우 ADO.NET 연결 관리자를 찾아 해당 속성 **ConnectUsingManagedIdentity**를 **True**로 설정합니다.
    > [!NOTE]
    >  Azure-SSIS 통합 런타임에서 ADO.NET 연결 관리자에 미리 구성된 모든 다른 인증 방법(예: 통합 인증, 암호)은 관리 ID 인증을 사용하여 데이터베이스 연결을 설정하는 데 사용되는 경우 **재정의**됩니다.

> [!NOTE]
>  기존 패키지에서 관리 ID 인증을 구성하려면 새 연결 관리자 속성 **ConnectUsingManagedIdentity**가 SSIS 프로젝트의 모든 ADO.NET 연결 관리자에 자동으로 추가되도록 적어도 [최신 SSIS 디자이너](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)를 한 번 이상 사용하여 SSIS 프로젝트를 다시 빌드하고 해당 SSIS 프로젝트를 Azure-SSIS 통합 런타임에 다시 배포하는 것이 좋습니다. 또 다른 방법은 런타임에 속성 경로 **\Package.Connections[{연결 관리자의 이름}].Properties[ConnectUsingManagedIdentity]** 에 속성 재정의를 직접 사용하는 것입니다.

## <a name="see-also"></a>참고 항목  
 [Integration Services&#40;SSIS&#41; 연결](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
