---
title: 백업, 복원 및 SSIS 카탈로그를 이동 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: bf806aef-8556-48ab-aed5-e95de9a2204e
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2c2873a6864e3ac5d55f180bfc2555d8cb471620
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53354473"
---
# <a name="backup-restore-and-move-the-ssis-catalog"></a>SSIS 카탈로그 백업, 복원 및 이동
  [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] 에는 SSISDB 데이터베이스가 포함되어 있습니다. SSISDB 데이터베이스에서 뷰를 쿼리하여 **SSISDB** 카탈로그에 저장된 개체, 설정 및 작업 데이터를 검사할 수 있습니다. 이 항목에서는 데이터베이스 백업 및 복원에 대한 지침을 제공합니다.  
  
 **SSISDB** 카탈로그는 사용자가 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버에 배포한 패키지를 저장합니다. 카탈로그에 대한 자세한 내용은 [SSIS 카탈로그](catalog/ssis-catalog.md)를 참조하세요.  
  
##  <a name="backup"></a> SSIS 데이터베이스를 백업하려면  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 를 열고 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에 연결합니다.  
  
2.  BACKUP MASTER KEY Transact-SQL 문을 사용하여 SSISDB 데이터베이스에 대한 마스터 키를 백업합니다. 이 키는 사용자가 지정한 파일에 저장됩니다. 암호를 사용하여 파일의 마스터 키를 암호화합니다.  
  
     문에 대한 자세한 내용은 [BACKUP MASTER KEY&#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-master-key-transact-sql)를 참조하세요.  
  
     다음 예에서는 마스터 키를 `c:\temp directory\RCTestInstKey` 파일로 내보냅니다. 마스터 키를 암호화하는 데에는 `LS2Setup!` 암호가 사용되었습니다.  
  
    ```  
    backup master key to file = 'c:\temp\RCTestInstKey'  
           encryption by password = 'LS2Setup!'  
  
    ```  
  
3.  **에서** 데이터베이스 백업 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]대화 상자를 사용하여 SSISDB 데이터베이스를 백업합니다. 자세한 내용은 참조 하세요. [방법: 데이터베이스 (SQL Server Management Studio) 백업](https://go.microsoft.com/fwlink/?LinkId=231812)합니다.  
  
4.  다음을 수행하여 ##MS_SSISServerCleanupJobLogin##에 대한 CREATE LOGIN 스크립트를 생성합니다. 자세한 내용은 [CREATE LOGIN&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)을 참조하세요.  
  
    1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 **보안** 노드를 확장한 후 **로그인** 노드를 확장합니다.  
  
    2.  **##MS_SSISServerCleanupJobLogin##** 을 마우스 오른쪽 단추로 클릭한 후 **로그인 스크립팅** > **CREATE** > **새 쿼리 편집기 창**을 클릭합니다.  
  
5.  SSISDB 카탈로그가 만들어지지 않은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스로 SSISDB 데이터베이스를 복원할 경우 다음을 수행하여 sp_ssis_startup에 대한 CREATE PROCEDURE 스크립트를 생성합니다. 자세한 내용은 [CREATE PROCEDURE&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)를 참조하세요.  
  
    1.  개체 탐색기에서 **데이터베이스** 노드를 확장한 후 **master** > **프로그래밍 기능** > **저장 프로시저** 노드를 확장합니다.  
  
    2.  **dbo.sp_ssis_startup**을 마우스 오른쪽 단추로 클릭한 후 **저장 프로시저 스크립팅** > **CREATE** > **새 쿼리 편집기 창**을 클릭합니다.  
  
6.  SQL Server 에이전트가 시작되었는지 확인합니다.  
  
7.  SSISDB 카탈로그가 만들어지지 않은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스로 SSISDB 데이터베이스를 복원할 경우 다음을 수행하여 SSIS 서버 유지 관리 작업에 대한 스크립트를 생성합니다. 이 스크립트는 SSISDB 카탈로그가 생성될 때 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트에 자동으로 만들어집니다. 이 작업은 보존 기간이 지난 작업 로그를 정리하고 오래된 프로젝트 버전을 제거하는 데 도움을 줍니다.  
  
    1.  개체 탐색기에서 **SQL Server 에이전트** 노드를 확장한 후 **작업** 노드를 확장합니다.  
  
    2.  SSIS 서버 유지 관리 작업을 마우스 오른쪽 단추로 클릭한 후 **작업 스크립팅** > **CREATE** > **새 쿼리 편집기 창**을 클릭합니다.  
  
### <a name="to-restore-the-ssis-database"></a>SSIS 데이터베이스를 복원하려면  
  
1.  SSISDB 카탈로그가 만들어지지 않은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 SSISDB 데이터베이스를 복원할 경우 sp_configure 저장 프로시저를 실행하여 CLR(공용 언어 런타임)을 사용하도록 설정합니다. 자세한 내용은 [sp_configure&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 및 [clr enabled 옵션](https://go.microsoft.com/fwlink/?LinkId=231855)을 참조하세요.  
  
    ```  
    use master   
           sp_configure 'clr enabled', 1  
           reconfigure  
  
    ```  
  
2.  SSISDB 카탈로그가 만들어지지 않은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스로 SSISDB 데이터베이스를 복원할 경우 비대칭 키를 만들고 비대칭 키로부터 로그인한 후 해당 로그인에 UNSAFE 권한을 부여합니다.  
  
    ```  
    Create Asymmetric key MS_SQLEnableSystemAssemblyLoadingKey  
           FROM Executable File = 'C:\Program Files\Microsoft SQL Server\110\DTS\Binn\Microsoft.SqlServer.IntegrationServices.Server.dll'  
  
    ```  
  
     [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] CLR 저장 프로시저를 사용하려면 해당 로그인에 UNSAFE 권한을 부여해야 합니다. UNSAFE 코드 권한에 대한 자세한 내용은 [Creating an Assembly](../relational-databases/clr-integration/assemblies/creating-an-assembly.md)를 참조하십시오.  
  
    ```  
    Create Login MS_SQLEnableSystemAssemblyLoadingUser  
           FROM Asymmetric key MS_SQLEnableSystemAssemblyLoadingKey   
  
           Grant unsafe Assembly to MS_SQLEnableSystemAssemblyLoadingUser  
  
    ```  
  
3.  **에서** 데이터베이스 복원 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]대화 상자를 사용하여 백업에서 SSISDB 데이터베이스를 복원합니다. 자세한 내용은 다음 항목을 참조하십시오.  
  
    -   [데이터베이스 복원&#40;일반 페이지&#41;](general-page-of-integration-services-designers-options.md)  
  
    -   [데이터베이스 복원&#40;파일 페이지&#41;](../relational-databases/backup-restore/restore-database-files-page.md)  
  
    -   [데이터베이스 복원&#40;옵션 페이지&#41;](../relational-databases/backup-restore/restore-database-options-page.md)  
  
4.  [SSIS 데이터베이스를 백업하려면](#backup) 에서 ##MS_SSISServerCleanupJobLogin##, sp_ssis_startup 및 SSIS 서버 유지 관리 작업에 대해 만든 스크립트를 실행합니다. SQL Server 에이전트가 시작되었는지 확인합니다.  
  
5.  다음 문을 실행하여 sp_ssis_startup 프로시저가 자동 실행되도록 설정합니다. 자세한 내용은 [sp_procoption&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-procoption-transact-sql)을 참조하세요.  
  
    ```  
    EXEC sp_procoption N'sp_ssis_startup','startup','on'  
    ```  
  
6.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 **로그인 속성** 대화 상자를 사용하여 SSISDB 사용자 ##MS_SSISServerCleanupJobUser##(SSISDB 데이터베이스)를 ##MS_SSISServerCleanupJobLogin##에 매핑합니다.  
  
7.  다음 방법 중 하나를 사용하여 마스터 키를 복원합니다. 암호화에 대한 자세한 내용은 [Encryption Hierarchy](../relational-databases/security/encryption/encryption-hierarchy.md)을 참조하십시오.  
  
    -   **메서드 1**  
  
         이미 데이터베이스 마스터 키에 대한 백업을 수행했고 마스터 키를 암호화하기 위해 사용된 암호가 있는 경우 이 방법을 사용합니다.  
  
        ```  
               Restore master key from file = 'c:\temp\RCTestInstKey'  
               Decryption by password = 'LS2Setup!' -- 'Password used to encrypt the master key during SSISDB backup'  
               Encryption by password = 'LS3Setup!' -- 'New Password'  
               Force  
  
        ```  
  
        > [!NOTE]  
        >  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서비스 계정에 백업 키 파일에 대한 읽기 권한이 있는지 확인합니다.  
  
        > [!NOTE]  
        >  데이터베이스 마스터 키가 아직 서비스 마스터 키로 암호화되지 않은 경우 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 에 다음과 같은 경고 메시지가 표시됩니다. 경고 메시지를 무시합니다.  
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
  
8.  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] catalog.check_schema_version [을 실행하여 SSISDB 카탈로그 스키마와](/sql/integration-services/system-stored-procedures/catalog-check-schema-version)바이너리 파일(ISServerExec 및 SQLCLR 어셈블리)이 호환되는지 여부를 결정합니다.  
  
9. SSISDB 데이터베이스가 성공적으로 복원되었는지 확인하려면 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버에 배포된 패키지를 실행하는 등 SSISDB 카탈로그에 대해 작업을 수행합니다. 자세한 내용은 [SQL Server Management Studio를 사용하여 SSIS 서버에서 패키지 실행](run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)을 참조하세요.  
  
### <a name="to-move-the-ssis-database"></a>SSIS 데이터베이스를 이동하려면  
  
-   사용자 데이터베이스 이동 지침을 따릅니다. 자세한 내용은 [Move User Databases](../relational-databases/databases/move-user-databases.md)을 참조하세요.  
  
     SSISDB 데이터베이스의 마스터 키를 백업하고 백업 파일을 보호하십시오. 자세한 내용은 [SSIS 데이터베이스를 백업하려면](#backup)을 참조하세요.  
  
     Integration Services(SSIS) 관련 개체가 SSISDB 카탈로그가 아직 만들어지지 않은 새 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 만들어졌는지 확인합니다.  
  
  
