---
title: URL에 대한 SQL Server 백업 - 최상의 방법 및 문제 해결 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: de676bea-cec7-479d-891a-39ac8b85664f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d2d0f3ffdb4c8c026ce12f2f347cbeae0548ede7
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51672782"
---
# <a name="sql-server-backup-to-url-best-practices-and-troubleshooting"></a>URL에 대한 SQL Server 백업 - 최상의 방법 및 문제 해결
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 항목에는 SQL Server를 백업하고 Windows Azure Blob 서비스로 복원하는 최상의 방법 및 문제 해결 팁이 포함되어 있습니다.  
  
 Windows Azure Blob 저장소 서비스를 사용하는 SQL Server 백업 및 복원 작업에 대한 자세한 내용은 다음을 참조하십시오.  
  
-   [Microsoft Azure Blob 저장소 서비스로 SQL Server 백업 및 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
-   [자습서: Microsoft Azure Blob Storage Service로 SQL Server 백업 및 복원](../../relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
## <a name="managing-backups"></a>백업 관리  
 다음은 백업 관리 시 일반적으로 권장되는 사항입니다.  
  
-   blob을 실수로 덮어쓰지 않도록 모든 백업에 고유한 파일 이름을 사용하는 것이 좋습니다.  
  
-   컨테이너를 만들 때 필요한 인증 정보를 제공할 수 있는 사용자 또는 계정만 컨테이너의 blob을 읽거나 쓸 수 있도록 액세스 수준을 **개인**으로 설정하는 것이 좋습니다.  
  
-   Windows Azure Virtual Machine에서 실행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 경우 가상 머신과 같은 지역의 저장소 계정을 사용하여 지역 간의 데이터 전송 비용이 들지 않게 하십시오. 또한 동일한 지역을 사용하면 최적의 백업 및 복원 작업 성능이 보장됩니다.  
  
-   실패한 백업 작업으로 인해 백업 파일이 잘못될 수 있습니다. 실패한 백업을 주기적으로 확인하고 blob 파일을 삭제하는 것이 좋습니다. 자세한 내용은 [Deleting Backup Blob Files with Active Leases](../../relational-databases/backup-restore/deleting-backup-blob-files-with-active-leases.md)를 참조하세요.  
  
-   백업 중 `WITH COMPRESSION` 옵션을 사용하면 저장소 비용과 저장소 트랜잭션 비용이 최소화됩니다. 백업 프로세스를 완료하는 데 걸리는 시간도 줄어듭니다.  

- `MAXTRANSFERSIZE` 및 `BLOCKSIZE` 인수를 [URL에 대한 SQL Server 백업](./sql-server-backup-to-url.md)에서 권장하는 대로 설정합니다.
  
## <a name="handling-large-files"></a>큰 파일 처리  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 작업에서는 여러 스레드를 사용하여 Windows Azure Blob 저장소 서비스로 데이터 전송을 최적화합니다.  그러나 성능은 ISV 대역폭과 데이터베이스 크기 등의 다양한 요소에 따라 달라집니다. 온-프레미스 SQL Server 데이터베이스의 대형 데이터베이스나 파일 그룹을 백업하려는 경우 먼저 몇 가지 처리량 테스트를 수행하는 것이 좋습니다. Azure [저장소에 대한 SLA](https://azure.microsoft.com/support/legal/sla/storage/v1_0/) 에서는 Blob에 대해 고려 가능한 최대 처리 시간을 제공합니다.  
  
-   특히 큰 파일을 백업할 때 [백업 관리](##managing-backups) 섹션에서 권장하는 대로 `WITH COMPRESSION` 옵션을 사용해야 합니다.  
  
## <a name="troubleshooting-backup-to-or-restore-from-url"></a>URL 백업 또는 복원 문제 해결  
 다음은 Windows Azure Blob 스토리지 서비스로 백업하고 복원할 때 발생하는 문제를 해결하는 몇 가지 빠른 방법입니다.  
  
 지원되지 않는 옵션이나 제한 사항으로 인한 오류 발생을 방지하려면 제한 사항 목록과 [Microsoft Azure Blob 저장소 서비스로 SQL Server 백업 및 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) 문서의 BACKUP 및 RESTORE 명령 지원 정보를 검토하세요.  
  
 **인증 오류:**  
  
-   `WITH CREDENTIAL`은 Windows Azure Blob 저장소 서비스로 백업하거나 복원하는 데 필요한 새로운 옵션입니다. 자격 증명과 관련하여 다음과 같은 오류가 발생할 수 있습니다.  
  
     **BACKUP** 또는 **RESTORE** 명령에 지정된 자격 증명이 없습니다. 이 문제를 방지하려면 백업 문에 자격 증명이 없는 경우 자격 증명을 만드는 T-SQL 문을 포함합니다. 다음은 사용 가능한 예입니다.  
  
    ```sql  
    IF NOT EXISTS  
    (SELECT * FROM sys.credentials   
    WHERE credential_identity = 'mycredential')  
    CREATE CREDENTIAL <credential name> WITH IDENTITY = 'mystorageaccount'  
    ,SECRET = '<storage access key> ;  
    ```  
  
-   자격 증명이 있지만 백업 명령을 실행하는 데 사용되는 로그인 계정에 자격 증명 액세스 권한이 없습니다. **Alter any credential** 권한이 있는 ***db_backupoperator*** 역할의 로그인 계정을 사용합니다.  
  
-   저장소 계정 이름과 키 값을 확인합니다. 자격 증명에 저장된 정보와 백업 및 복원 작업에 사용하는 Windows Azure 저장소 계정의 속성 값이 일치해야 합니다.  
  
 **백업 오류:**  
  
-   동일한 blob으로 병렬 백업을 수행하면 **초기화 실패** 오류가 발생하여 백업 중 하나가 실패합니다.  
  
-   다음은 백업 오류 문제 해결에 도움이 되는 오류 로그입니다.  
  
    -   다음 형식으로 추적 플래그 3051을 설정하여 특정 오류 로그 로깅을 활성화합니다.  
  
        `BackupToUrl-\<instname>-\<dbname>-action-\<PID>.log`여기서 `\<action>`은 다음 값 중 하나입니다.  
  
        -   **DB**  
        -   **FILELISTONLY**  
        -   **LABELONLY**  
        -   **HEADERONLY**  
        -   **VERIFYONLY**  
  
    -   Windows 이벤트 로그의 응용 프로그램에서 이름이 `SQLBackupToUrl`인 로그를 검토하여 정보를 찾을 수도 있습니다.  

    -   큰 데이터베이스를 백업하는 경우 COMPRESSION, MAXTRANSFERSIZE, BLOCKSIZE 및 여러 URL 인수를 고려합니다.  [Azure Blob Storage로 VLDB 백업](https://blogs.msdn.microsoft.com/sqlcat/2017/03/10/backing-up-a-vldb-to-azure-blob-storage/)을 참조하세요.
  
        ```
        Msg 3202, Level 16, State 1, Line 1
        Write on "https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_0.bak" failed: 1117(The request could not be performed because of an I/O device error.)
        Msg 3013, Level 16, State 1, Line 1
        BACKUP DATABASE is terminating abnormally.
        ```

        ```sql  
        BACKUP DATABASE TestDb
        TO URL = 'https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_0.bak',
        URL = 'https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_1.bak',
        URL = 'https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_2.bak'
        WITH COMPRESSION, MAXTRANSFERSIZE = 4194304, BLOCKSIZE = 65536;  
        ```  

-   압축된 백업에서 복원할 때 다음과 같은 오류가 표시될 수 있습니다.  
  
    -   `SqlException 3284 occurred. Severity: 16 State: 5  
        Message Filemark on device 'https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_0.bak' is not aligned.           Reissue the Restore statement with the same block size used to create the backupset: '65536' looks like a possible value.`  
  
        이 오류를 해결하려면 **BLOCKSIZE = 65536**을 지정하여 **RESTORE** 문을 다시 실행하세요.  
  
-   Blob에 활성 임대가 있어 백업 중 오류가 발생합니다. 실패한 백업 작업으로 인해 Blob에 활성 임대가 있을 수 있습니다.  
  
     백업 문을 다시 시도하는 경우 다음과 같은 오류가 발생하여 백업 작업이 실패할 수 있습니다.  
  
     `Backup to URL received an exception from the remote endpoint. Exception Message: The remote server returned an error: (412) There is currently a lease on the blob and no lease ID was specified in the request.`  
  
     활성 임대가 있는 백업 blob 파일에 대해 복원 문을 시도할 경우 다음과 같은 오류가 발생하여 복원 작업이 실패합니다.  
  
     `Exception Message: The remote server returned an error: (409) Conflict..`  
  
     이러한 오류가 발생하면 blob 파일을 삭제해야 합니다. 이 시나리오와 이 문제 해결 방법에 대한 자세한 내용은 [Deleting Backup Blob Files with Active Leases](../../relational-databases/backup-restore/deleting-backup-blob-files-with-active-leases.md)를 참조하십시오.  
  
## <a name="proxy-errors"></a>프록시 오류  
 프록시 서버를 사용하여 인터넷에 액세스할 경우 다음과 같은 문제가 발생할 수 있습니다.  
  
 **프록시 서버에 의한 연결 제한:**  
  
 프록시 서버에는 분당 연결 수를 제한하는 설정이 있을 수 있습니다. URL에 대한 백업 프로세스는 다중 스레드 프로세스이므로 이 제한을 초과할 수 있습니다. 이러한 경우 프록시 서버는 연결을 해제합니다. 이 문제를 해결하려면 SQL Server에서 프록시를 사용하지 않도록 프록시 설정을 변경합니다. 다음은 오류 로그에 표시될 수 있는 오류 메시지 유형의 몇 가지 예입니다.  
  
```
Write on "https://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak" failed: Backup to URL received an exception from the remote endpoint. Exception Message: Unable to read data from the transport connection: The connection was closed.
```  
  
```
A nonrecoverable I/O error occurred on file "https://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak:" Error could not be gathered from Remote Endpoint.  
  
Msg 3013, Level 16, State 1, Line 2  
  
BACKUP DATABASE is terminating abnormally.  
```

```
BackupIoRequest::ReportIoError: write failure on backup device https://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak'. Operating system error Backup to URL received an exception from the remote endpoint. Exception Message: Unable to read data from the transport connection: The connection was closed.
```  
  
추적 플래그 3051을 사용하여 자세한 로깅을 설정하는 경우 로그에 다음과 같은 메시지도 표시될 수 있습니다.  
  
`HTTP status code 502, HTTP Status Message Proxy Error (The number of HTTP requests per minute exceeded the configured limit. Contact your ISA Server administrator.) ` 
  
 **기본 프록시 설정이 선택되지 않음:**  
  
경우에 따라 기본 설정은 선택되지 않으면 다음 중 하나와 같은 프록시 인증 오류가 발생합니다.
 
 `A nonrecoverable I/O error occurred on file "https://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak:" Backup to URL received an exception from the remote endpoint. Exception Message: The remote server returned an error: (407)* **Proxy Authentication Required.`  
  
이 문제를 해결하려면 다음 단계를 사용하여 URL에 대한 백업 프로세스에서 기본 프록시 설정을 사용하도록 허용하는 구성 파일을 만듭니다.  
  
1.  다음 xml 콘텐츠를 사용하여 `BackuptoURL.exe.config`라는 구성 파일을 만듭니다.  
  
    ```xml  
    <?xml version ="1.0"?>  
    <configuration>   
                    <system.net>   
                                    <defaultProxy enabled="true" useDefaultCredentials="true">   
                                                    <proxy usesystemdefault="true" />   
                                    </defaultProxy>   
                    </system.net>  
    </configuration>  
    ```  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 Binn 폴더에 구성 파일을 배치합니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 컴퓨터의 C 드라이브에 설치된 경우 구성 파일을 `C:\Program Files\Microsoft SQL Server\MSSQL13.\<InstanceName>\MSSQL\Binn`에 배치합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Microsoft Azure에 저장된 백업에서 복원](../../relational-databases/backup-restore/restoring-from-backups-stored-in-microsoft-azure.md)  
[BACKUP(Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)  
[RESTORE(Transact-SQL)](../../t-sql/statements/restore-statements-transact-sql.md)
  
