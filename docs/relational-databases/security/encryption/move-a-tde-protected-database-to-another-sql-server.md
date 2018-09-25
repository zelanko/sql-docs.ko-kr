---
title: 다른 SQL Server로 TDE 보호 데이터베이스 이동 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Transparent Data Encryption, moving
- TDE, moving a database
ms.assetid: fb420903-df54-4016-bab6-49e6dfbdedc7
caps.latest.revision: 18
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: 8512a02e65df08ba99e48af6ece110ab7c893b71
ms.sourcegitcommit: 3762dd447ca4bb449eda8476e72f393db0851b38
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/18/2018
ms.locfileid: "46013788"
---
# <a name="move-a-tde-protected-database-to-another-sql-server"></a>다른 SQL Server로 TDE 보호 데이터베이스 이동
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 TDE(투명한 데이터 암호화)를 사용하여 데이터베이스를 보호하고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 이 데이터베이스를 [!INCLUDE[tsql](../../../includes/tsql-md.md)]의 다른 인스턴스로 이동하기 위한 단계를 설명합니다. TDE(투명한 데이터 암호화)를 통해 데이터 및 로그 파일의 실시간 I/O 암호화 및 암호 해독을 수행합니다. 이 암호화에서는 DEK(데이터베이스 암호화 키)를 사용하며 이 키는 복구하는 동안 사용할 수 있도록 데이터베이스 부트 레코드에 저장됩니다. DEK는 서버의 **master** 데이터베이스에 저장된 인증서 또는 EKM 모듈로 보호되는 비대칭 키를 사용하여 보호되는 대칭 키입니다.  
   
##  <a name="Restrictions"></a> 제한 사항  
  
-   TDE로 보호되는 데이터베이스를 이동하려면 DEK를 여는 데 사용되는 인증서 또는 비대칭 키도 이동해야 합니다. 인증서 또는 비대칭 키는 **에서 데이터베이스 파일에 액세스할 수 있도록 대상 서버의** master [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 설치되어야 합니다. 자세한 내용은 [TDE&#40;투명한 데이터 암호화&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md)를 참조하세요.  
  
-   인증서를 복구하려면 인증서 파일 및 개인 키 파일의 사본을 보관해야 합니다. 개인 키의 암호는 데이터베이스 마스터 키 암호와 동일할 필요가 없습니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 기본적으로 여기서 생성된 파일을 **C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA** 에 저장합니다. 파일 이름 및 위치는 다를 수 있습니다.  
  
##  <a name="Permissions"></a> Permissions  
  
-   데이터베이스 마스터 키를 만들려면 **master** 데이터베이스에 대한 **CONTROL DATABASE** 권한이 필요합니다.  
  
-   DEK를 보호하는 인증서를 만들려면 **master** 데이터베이스에 대한 **CREATE CERTIFICATE** 권한이 필요합니다.  
  
-   암호화된 데이터베이스에 대한 **CONTROL DATABASE** 권한과 데이터베이스 암호화 키를 암호화하는 데 사용되는 인증서 또는 비대칭 키에 대한 **VIEW DEFINITION** 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> 투명한 데이터 암호화로 보호되는 데이터베이스를 만들려면  

다음 절차에서는 SQL Server Management Studio를 사용하고 Transact-SQL을 사용하여 TDE로 보호되는 데이터베이스를 만들어야 함을 보여줍니다.
  
###  <a name="SSMSCreate"></a> SQL Server Management Studio 사용  
  
1.  **master** 데이터베이스에서 데이터베이스 마스터 키 및 인증서를 만듭니다. 자세한 내용은 아래에서 **Transact-SQL 사용** 을 참조하세요.  
  
2.  **master** 데이터베이스에서 서버 인증서의 백업을 만듭니다. 자세한 내용은 아래에서 **Transact-SQL 사용** 을 참조하세요.  
  
3.  개체 탐색기에서 **데이터베이스** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **새 데이터베이스**를 선택합니다.  
  
4.  **새 데이터베이스** 대화 상자의 **데이터베이스 이름** 상자에 새 데이터베이스의 이름을 입력합니다.  
  
5.  **소유자** 상자에 새 데이터베이스의 소유자 이름을 입력합니다. 또는 줄임표 **(…)** 를 클릭하여 **데이터베이스 소유자 선택** 대화 상자를 엽니다. 새 데이터베이스를 만드는 방법은 [Create a Database](../../../relational-databases/databases/create-a-database.md)를 참조하세요.  
  
6.  개체 탐색기에서 더하기 기호를 클릭하여 **데이터베이스** 폴더를 확장합니다.  
  
7.  만든 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 가리킨 다음 **데이터베이스 암호화 관리**를 선택합니다.  
  
     **데이터베이스 암호화 관리** 대화 상자에는 다음과 같은 옵션이 제공됩니다.  
  
     **암호화 알고리즘**  
     데이터베이스 암호화에 사용할 알고리즘을 표시하거나 설정합니다. 기본 알고리즘은**AES128** 입니다. 이 필드는 비워 둘 수 없습니다. 암호화 알고리즘에 대한 자세한 내용은 [Choose an Encryption Algorithm](../../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)을 참조하세요.  
  
     **서버 인증서 사용**  
     인증서로 암호화의 보안을 유지하도록 설정합니다. 목록에서 하나를 선택합니다. 서버 인증서에 대한 **VIEW DEFINITION** 권한이 없으면 이 목록은 비어 있습니다. 암호화의 인증서 방법을 선택한 경우에는 이 값을 비워 둘 수 없습니다. 인증서에 대한 자세한 내용은 [SQL Server Certificates and Asymmetric Keys](../../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)를 참조하세요.  
  
     **서버 비대칭 키 사용**  
     비대칭 키로 암호화의 보안을 유지하도록 설정합니다. 사용 가능한 비대칭 키만 표시됩니다. EKM 모듈에서 보호하는 비대칭 키만 TDE를 사용하여 데이터베이스를 암호화할 수 있습니다.  
  
     **데이터베이스 암호화 설정**  
     데이터베이스의 TDE를 설정(선택) 또는 해제(선택 취소)로 변경합니다.  
  
8.  완료되었으면 **확인**을 클릭합니다.  
  
###  <a name="TsqlCreate"></a> Transact-SQL 사용  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```sql  
    -- Create a database master key and a certificate in the master database.  
    USE master ;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '*rt@40(FL&dasl1';  
    GO  
    CREATE CERTIFICATE TestSQLServerCert   
    WITH SUBJECT = 'Certificate to protect TDE key'  
    GO  
    -- Create a backup of the server certificate in the master database.  
    -- The following code stores the backup of the certificate and the private key file in the default data location for this instance of SQL Server   
    -- (C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA).  
  
    BACKUP CERTIFICATE TestSQLServerCert   
    TO FILE = 'TestSQLServerCert'  
    WITH PRIVATE KEY   
    (  
        FILE = 'SQLPrivateKeyFile',  
        ENCRYPTION BY PASSWORD = '*rt@40(FL&dasl1'  
    );  
    GO  
    -- Create a database to be protected by TDE.  
    CREATE DATABASE CustRecords ;  
    GO  
    -- Switch to the new database.  
    -- Create a database encryption key, that is protected by the server certificate in the master database.   
    -- Alter the new database to encrypt the database using TDE.  
    USE CustRecords;  
    GO  
    CREATE DATABASE ENCRYPTION KEY  
    WITH ALGORITHM = AES_128  
    ENCRYPTION BY SERVER CERTIFICATE TestSQLServerCert;  
    GO  
    ALTER DATABASE CustRecords  
    SET ENCRYPTION ON;  
    GO  
    ```  
  
 참조 항목:  
  
-   [CREATE MASTER KEY&#40;Transact-SQL&#41;](../../../t-sql/statements/create-master-key-transact-sql.md)  
  
-   [CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../../t-sql/statements/create-certificate-transact-sql.md)  
  
-   [BACKUP CERTIFICATE&#40;Transact-SQL&#41;](../../../t-sql/statements/backup-certificate-transact-sql.md)  
  
-   [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
-   [CREATE DATABASE ENCRYPTION KEY&#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-encryption-key-transact-sql.md)  
  
-   [ALTER DATABASE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md)  
  
##  <a name="TsqlProcedure"></a> 투명한 데이터 암호화로 보호되는 데이터베이스를 이동하려면 

다음 절차에서는 SQL Server Management Studio를 사용하고 Transact-SQL을 사용하여 TDE로 보호되는 데이터베이스를 이동해야 함을 보여줍니다.
  
###  <a name="SSMSMove"></a> SQL Server Management Studio 사용  
  
1.  개체 탐색기에서 위에서 암호화한 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크** 를 가리킨 후 **분리...** 를 선택합니다.  
  
     **데이터베이스 분리** 대화 상자에는 다음과 같은 옵션이 제공됩니다.  
  
     **분리할 데이터베이스**  
     분리할 데이터베이스를 나열합니다.  
  
     **Database Name**  
     분리할 데이터베이스 이름을 표시합니다.  
  
     **연결 삭제**  
     지정한 데이터베이스에 대한 연결을 끊습니다.  
  
    > [!NOTE]  
    >  활성 연결이 있는 데이터베이스는 분리할 수 없습니다.  
  
     **통계 업데이트**  
     기본적으로 분리 작업은 데이터베이스를 분리할 때 오래된 최적화 통계를 유지합니다. 기존의 최적화 통계를 업데이트하려면 이 확인란을 클릭합니다.  
  
     **전체 텍스트 카탈로그 유지**  
     기본적으로 분리 작업은 데이터베이스와 연결된 모든 전체 텍스트 카탈로그를 유지합니다. 전체 텍스트 카탈로그를 제거하려면 **전체 텍스트 카탈로그 유지** 확인란의 선택을 취소합니다. 이 옵션은 데이터베이스를 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 업그레이드하는 경우에만 표시됩니다.  
  
     **상태**  
     **준비** 또는 **준비 안 됨**상태 중 하나를 표시합니다.  
  
     **메시지**  
     다음과 같이 **메시지** 열에 데이터베이스에 대한 정보가 표시될 수도 있습니다.  
  
    -   데이터베이스가 복제와 관련된 경우 **상태** 는 **준비 안 됨** 이고 **메시지** 열에는 **데이터베이스 복제 완료**가 표시됩니다.  
  
    -   데이터베이스에 하나 이상의 활성 연결이 있는 경우 **상태**는 **준비 안 됨**이고 **메시지** 열에는 *<number_of_active_connections>***활성 연결**(예: **1개의 활성 연결**)이 표시됩니다. 데이터베이스를 분리하려면 먼저 **연결 삭제**를 선택하여 모든 활성 연결을 끊어야 합니다.  
  
     메시지에 대한 자세한 내용을 보려면 하이퍼링크로 연결된 텍스트를 클릭하여 작업 모니터를 엽니다.  
  
2.  **확인**을 클릭합니다.  
  
3.  Windows 탐색기를 사용하여 데이터베이스 파일을 원본 서버에서 대상 서버의 동일한 위치로 이동 또는 복사합니다.  
  
4.  Window 탐색기를 사용하여 서버 인증서 및 개인 키 파일의 백업을 원본 서버에서 대상 서버의 동일한 위치로 이동 또는 복사합니다.  
  
5.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 대상 인스턴스에서 데이터베이스 마스터 키를 만듭니다. 자세한 내용은 아래에서 **Transact-SQL 사용** 을 참조하세요.  
  
6.  원본 서버 인증서 백업 파일을 사용하여 서버 인증서를 다시 만듭니다. 자세한 내용은 아래에서 **Transact-SQL 사용** 을 참조하세요.  
  
7.  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 **데이터베이스** 폴더를 마우스 오른쪽 단추로 클릭하고 **연결...** 을 선택합니다.  
  
8.  **데이터베이스 연결** 대화 상자의 **연결할 데이터베이스**아래에서 **추가**를 클릭합니다.  
  
9. **데이터베이스 파일 찾기 –***server_name* 대화 상자에서 새 서버에 연결할 데이터베이스 파일을 선택하고 **확인**을 클릭합니다.  
  
     **데이터베이스 연결** 대화 상자에는 다음과 같은 옵션이 제공됩니다.  
  
     **연결할 데이터베이스**  
     선택한 데이터베이스에 대한 정보를 표시합니다.  
  
     \<열 머리글 없음>  
     연결 작업의 상태를 나타내는 아이콘을 표시합니다. 가능한 아이콘은 아래의 **상태** 에 대한 설명에 설명되어 있습니다.  
  
     **MDF 파일 위치**  
     선택한 MDF 파일의 경로와 파일 이름을 표시합니다.  
  
     **Database Name**  
     데이터베이스 이름을 표시합니다.  
  
     **다른 이름으로 연결**  
     필요에 따라 연결할 데이터베이스의 이름을 다른 이름으로 지정합니다.  
  
     **소유자**  
     필요에 따라 다른 소유자를 선택할 수 있도록 가능한 데이터베이스 소유자의 드롭다운 목록을 제공합니다.  
  
     **상태**  
     다음 표에 설명된 내용과 같이 데이터베이스의 상태를 표시합니다.  
  
    |아이콘|상태 텍스트|설명|  
    |----------|-----------------|-----------------|  
    |(아이콘 없음)|(텍스트 없음)|연결 작업이 시작되지 않았거나 이 개체에 대해 보류 중입니다. 대화 상자가 열려 있는 경우에 표시되는 기본 설정입니다.|  
    |녹색, 오른쪽 방향 삼각형|진행 중|연결 작업이 시작되었지만 아직 완료되지 않았습니다.|  
    |녹색 확인 표시|성공|개체가 성공적으로 연결되었습니다.|  
    |흰색 십자 표시가 있는 빨강 원|Error|연결 작업을 수행하는 동안 오류가 발생하여 완료하지 못했습니다.|  
    |오른쪽과 왼쪽에 두 개의 검정 사분면이 있고 위쪽과 아래쪽에 두 개의 흰색 사분면이 있는 원|중지됨|사용자가 작업을 중지하여 연결 작업이 완료되지 않았습니다.|  
    |시계 반대 방향을 가리키는 곡선 모양의 화살표가 있는 원|롤백됨|연결 작업이 성공적으로 완료되었지만 다른 개체를 연결하는 동안 발생한 오류로 인해 롤백되었습니다.|  
  
     **메시지**  
     빈 메시지 또는 "파일을 찾을 수 없습니다"라는 하이퍼링크를 표시합니다.  
  
     **추가**  
     필요한 기본 데이터베이스 파일을 찾습니다. 사용자가 .mdf 파일을 선택하면 **연결할 데이터베이스** 표의 각 필드에 적절한 정보가 자동으로 입력됩니다.  
  
     **제거**  
     선택한 파일을 **연결할 데이터베이스** 표에서 제거합니다.  
  
     **"** *<database_name>* **" 데이터베이스 정보**  
     연결할 파일의 이름을 표시합니다. 파일의 경로 이름을 확인하거나 변경하려면 **찾아보기** 단추(**…**)를 클릭합니다.  
  
    > [!NOTE]  
    >  파일이 없으면 **메시지** 열에 "찾을 수 없음"이 표시됩니다. 로그 파일을 찾을 수 없는 경우 다른 디렉터리에 있거나 삭제된 것입니다. 올바른 위치를 가리키도록 **데이터베이스 정보** 표의 파일 경로를 업데이트하거나 표에서 로그 파일을 제거해야 합니다. .ndf 데이터 파일을 찾을 수 없는 경우 올바른 위치를 가리키도록 표에서 해당 파일의 경로를 업데이트해야 합니다.  
  
     **원래 파일 이름**  
     데이터베이스에 속한 연결된 파일의 이름을 표시합니다.  
  
     **파일 유형**  
     파일의 형식( **데이터** 또는 **로그**)을 나타냅니다.  
  
     **현재 파일 경로**  
     선택한 데이터베이스 파일의 경로를 표시합니다. 이 경로는 직접 편집할 수 있습니다.  
  
     **메시지**  
     빈 메시지 또는 "**파일을 찾을 수 없습니다**"라는 하이퍼링크를 표시합니다.  
  
###  <a name="TsqlMove"></a> Transact-SQL 사용  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```sql  
    -- Detach the TDE protected database from the source server.   
    USE master ;  
    GO  
    EXEC master.dbo.sp_detach_db @dbname = N'CustRecords';  
    GO  
    -- Move or copy the database files from the source server to the same location on the destination server.   
    -- Move or copy the backup of the server certificate and the private key file from the source server to the same location on the destination server.   
    -- Create a database master key on the destination instance of SQL Server.   
    USE master;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '*rt@40(FL&dasl1';  
    GO  
    -- Recreate the server certificate by using the original server certificate backup file.   
    -- The password must be the same as the password that was used when the backup was created.  
  
    CREATE CERTIFICATE TestSQLServerCert   
    FROM FILE = 'TestSQLServerCert'  
    WITH PRIVATE KEY   
    (  
        FILE = 'SQLPrivateKeyFile',  
        DECRYPTION BY PASSWORD = '*rt@40(FL&dasl1'  
    );  
    GO  
    -- Attach the database that is being moved.   
    -- The path of the database files must be the location where you have stored the database files.  
    CREATE DATABASE [CustRecords] ON   
    ( FILENAME = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\CustRecords.mdf' ),  
    ( FILENAME = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\CustRecords_log.LDF' )  
    FOR ATTACH ;  
    GO  
    ```  
  
 참조 항목:  
  
-   [sp_detach_db&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)  
  
-   [CREATE MASTER KEY&#40;Transact-SQL&#41;](../../../t-sql/statements/create-master-key-transact-sql.md)  
  
-   [CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../../t-sql/statements/create-certificate-transact-sql.md)  
  
-   [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [Azure SQL Database를 사용한 투명한 데이터 암호화](../../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md)  
  
  
