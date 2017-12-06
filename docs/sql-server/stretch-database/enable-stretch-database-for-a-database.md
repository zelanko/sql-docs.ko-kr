---
title: "데이터베이스에서 Stretch Database 활성화 | Microsoft 문서"
ms.custom: 
ms.date: 08/05/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: stretch-database
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, enabling database
- enabling database for Stretch Database
ms.assetid: 37854256-8c99-4566-a552-432e3ea7c6da
caps.latest.revision: "70"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ea4a52220729ad7d0fa69ef4e0784fd676aa3f5a
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="enable-stretch-database-for-a-database"></a>Enable Stretch Database for a database
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Stretch Database에 기존 데이터베이스를 구성하려면 SQL Server Management Studio에서 데이터베이스에 대해 **태스크 | 스트레치 | 사용**을 선택하여 **스트레치에 데이터베이스 사용** 마법사를 엽니다. Transact-SQL을 사용하여 데이터베이스에서 스트레치 데이터베이스를 활성화할 수도 있습니다.  
  
 개별 테이블에 대해 **태스크 | 스트레치 | 사용** 선택하고 스트레치 데이터베이스에 데이터베이스를 사용하도록 설정하지 않은 경우에는 마법사가 스트레치 데이터베이스에 데이터베이스를 구성하고 그 과정에서 사용자가 테이블을 선택하도록 합니다. [Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)의 단계 대신 이 항목의 단계를 따릅니다.  
  
 데이터베이스 또는 테이블에서 스트레치 데이터베이스를 활성화하려면 db_owner 사용 권한이 필요합니다. 데이터베이스에서 스트레치 데이터베이스를 활성화하려면 CONTROL DATABASE 사용 권한도 필요합니다.  

 >   [!NOTE]
 > 나중에 Stretch Database를 사용하지 않도록 설정하려는 경우 테이블 또는 데이터베이스에서 Stretch Database를 사용하지 않도록 설정하면 원격 개체가 삭제되지 않습니다. 원격 테이블 또는 원격 데이터베이스를 삭제하려면 Azure 관리 포털을 사용하여 삭제해야 합니다. 원격 개체는 수동으로 삭제할 때까지 Azure 비용이 계속해서 발생합니다. 
 
## <a name="before-you-get-started"></a>시작하기 전에  
  
-   스트레치에서 데이터베이스를 구성하기 전에 스트레치에 적합한 데이터베이스와 테이블을 식별하기 위해 스트레치 데이터베이스 관리자를 실행하는 것이 좋습니다. 스트레치 데이터베이스 관리자는 차단 문제도 식별합니다. 자세한 내용은 [스트레치 데이터베이스 관리자를 실행하여 스트레치 데이터베이스용 데이터베이스 및 테이블 식별](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)을 참조하세요.  
  
-   [스트레치 데이터베이스에 대한 제한 사항](../../sql-server/stretch-database/limitations-for-stretch-database.md)을 검토합니다.  
  
-   스트레치 데이터베이스는 데이터를 Azure로 마이그레이션합니다. 따라서 Azure 계정 및 청구를 위한 구독이 있어야 합니다. Azure 계정을 생성하려면 [여기를 클릭하십시오](http://azure.microsoft.com/en-us/pricing/free-trial/).  
  
-   새 Azure 서버를 만들거나 기존 Azure 서버를 선택하는 데 필요한 연결 및 로그인 정보를 준비합니다.  
  
##  <a name="EnableTSQLServer"></a> 필수 조건: 서버에서 스트레치 데이터베이스 사용  
 데이터베이스 또는 테이블에서 스트레치 데이터베이스를 활성화하기 전에 로컬 서버에서 스트레치 데이터베이스를 먼저 활성화해야 합니다. 이 작업에는 sysadmin 또는 serveradmin 권한이 필요합니다.  
  
-   필요한 관리 권한이 있으면 **스트레치에 데이터베이스 사용** 마법사가 스트레치에 사용할 서버를 구성합니다.  
  
-   필요한 권한이 없는 경우에는 마법사를 실행하기 전에 관리자가 **sp_configure** 를 실행하여 수동으로 옵션을 사용하도록 설정하거나 관리자가 마법사를 실행해야 합니다.  
  
 서버에서 스트레치 데이터베이스를 수동으로 사용하도록 설정하려면 **sp_configure** 를 실행하고 **원격 데이터 보관** 옵션을 설정합니다. 다음 예에서는 값을 1로 설정하여 **remote data archive** 옵션을 활성화합니다.  
  
```sql
EXEC sp_configure 'remote data archive' , '1';  
GO

RECONFIGURE;  
GO  
```  
  
 자세한 내용은 [원격 데이터 보관 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-remote-data-archive-server-configuration-option.md) 및 [sp_configure&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)를 참조하세요.  
  
##  <a name="Wizard"></a> 마법사를 사용하여 데이터베이스에서 Stretch Database 활성화  
 입력해야 하는 정보와 선택해야 하는 항목을 포함하여 스트레치에 데이터베이스 사용 마법사에 대한 자세한 내용은 [스트레치에 데이터베이스 사용 마법사를 실행하여 시작](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md)을 참조하세요.  
  
##  <a name="EnableTSQLDatabase"></a> Transact-SQL을 사용하여 데이터베이스에서 스트레치 데이터베이스 활성화  
 개별 테이블에서 스트레치 데이터베이스를 활성화할 수 있으려면 데이터베이스에서 스트레치 데이터베이스를 먼저 활성화해야 합니다.  
  
 데이터베이스 또는 테이블에서 스트레치 데이터베이스를 활성화하려면 db_owner 사용 권한이 필요합니다. 데이터베이스에서 스트레치 데이터베이스를 활성화하려면 CONTROL DATABASE 사용 권한도 필요합니다.  
  
1.  시작하기 전에 스트레치 데이터베이스가 마이그레이션하는 데이터의 기존 Azure 서버를 선택하거나 새 Azure 서버를 만듭니다.  
  
2.  Azure 서버에서 SQL Server가 원격 서버와 통신이 가능하도록 하는 SQL Server의 IP 주소 범위로 방화벽 규칙을 만듭니다.  

    SSMS(SQL Server Management Studio)의 개체 탐색기에서 Azure 서버에 연결을 시도하여 필요한 값을 쉽게 찾고 방화벽 규칙을 만들 수 있습니다. SSMS를 사용하면 필요한 IP 주소 값이 이미 포함된 다음 대화 상자를 열어 규칙을 만들 수 있습니다.
    
    ![스트레치용 방화벽 규칙](../../sql-server/stretch-database/media/firewall-rule-for-stretch.png)
  
3.  스트레치 데이터베이스용으로 SQL Server 데이터베이스를 구성하려면, 데이터베이스에 데이터베이스 마스터 키가 있어야 합니다. 데이터베이스 마스터 키는 스트레치 데이터베이스가 원격 데이터베이스에 연결하기 위해 사용하는 자격 증명을 보호합니다. 새 데이터베이스 마스터 키를 만드는 예제는 다음과 같습니다.  
  
    ```sql  
    USE <database>; 
    GO  
  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD='<password>'; 
    GO
    ```  
    데이터베이스 마스터 키에 대한 자세한 내용은 [CREATE MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md) 및 [데이터베이스 마스터 키 만들기](../../relational-databases/security/encryption/create-a-database-master-key.md)를 참조하세요.
    
4.  Stretch Database용으로 데이터베이스를 구성하는 경우 온-프레미스 SQL Server와 원격 Azure 서버 간의 통신에 사용할 Stretch Database용 자격 증명을 제공해야 합니다. 두 가지 옵션이 있습니다.  
  
    -   관리자 자격 증명을 제공할 수 있습니다.  
  
        -   마법사를 사용하여 스트레치 데이터베이스를 활성화하면, 그 때 자격 증명을 만들 수 있습니다.  
  
        -   **ALTER DATABASE**를 실행하여 스트레치 데이터베이스를 사용하도록 설정하려는 경우 **ALTER DATABASE** 를 실행하여 스트레치 데이터베이스를 사용하도록 설정하기 전에 수동으로 자격 증명을 만들어야 합니다. 
        
        새 자격 증명을 만드는 예제는 다음과 같습니다.
  
        ```sql  
        CREATE DATABASE SCOPED CREDENTIAL <db_scoped_credential_name>  
            WITH IDENTITY = '<identity>' , SECRET = '<secret>' ;
        GO   
        ```  

         자격 증명에 대한 자세한 내용은 [CREATE DATABASE SCOPED CREDENTIAL&#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)을 참조하세요. 자격 증명을 만들려면 ALTER ANY CREDENTIAL 권한이 필요합니다.  

    -   다음 조건이 모두 참인 경우 원격 Azure 서버와 통신하기 위해 SQL Server용 페더레이션된 서비스 계정을 사용할 수 있습니다.  
  
        -   SQL Server 인스턴스를 실행하는 서비스 계정은 도메인 계정입니다.  
  
        -   이 도메인 계정은 Active Directory가 Azure Active Directory와 페더레이션된 도메인에 속합니다.  
  
        -   원격 Azure 서버는 Azure Active Directory 인증을 지원하도록 구성됩니다.  
  
        -   SQL Server 인스턴스를 실행하는 서비스 계정은 원격 Azure 서버에서 dbmanager 또는 sysadmin 계정으로 구성되어야 합니다.  
  
5.  스트레치 데이터베이스용으로 데이터베이스를 구성하려면 ALTER DATABASE 명령을 실행합니다.  
  
    1.  SERVER 인수에 대해 기존 Azure 서버의 이름을 이름의 `.database.windows.net` 부분을 포함하여 제공합니다(예: `MyStretchDatabaseServer.database.windows.net`).  
  
    2.  CREDENTIAL 인수와 기존 관리자 자격 증명을 제공하거나 FEDERATED_SERVICE_ACCOUNT = ON을 지정합니다. 다음 예에서는 기존 자격 증명을 제공합니다.  
  
    ```sql  
    ALTER DATABASE <database name>  
        SET REMOTE_DATA_ARCHIVE = ON  
            (  
                SERVER = '<server_name>' ,  
                CREDENTIAL = <db_scoped_credential_name>  
            ) ;  
    GO
    ```  
  
## <a name="next-steps"></a>다음 단계  
-   [Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) : 추가 테이블을 사용합니다.  
  
-   데이터 마이그레이션 상태를 보려면 [데이터 마이그레이션 모니터링 및 문제 해결&#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md)을 참조하세요.  
  
-   [데이터 마이그레이션 일시 중지 및 다시 시작&#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)  
  
-   [스트레치 데이터베이스 관리 및 문제 해결](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  
  
-   [스트레치 사용 데이터베이스 백업](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
  
-   [스트레치 사용 데이터베이스 복원](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)  
  
## <a name="see-also"></a>참고 항목  
 [스트레치 데이터베이스 관리자를 실행하여 스트레치 데이터베이스용 데이터베이스 및 테이블 식별](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)   
 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
  
