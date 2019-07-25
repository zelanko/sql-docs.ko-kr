---
title: 백업 디바이스(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 08/12/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- tape backup devices, about tape backup devices
- backup devices [SQL Server]
- disk backup devices [SQL Server]
- database backups [SQL Server], backup devices
- logical devices [SQL Server]
- backup devices [SQL Server], about backup devices
- backing up [SQL Server], backup devices
- removable media [SQL Server]
- network shares [SQL Server]
- backups [SQL Server], backup devices
- tape backup devices
- physical devices [SQL Server]
- backing up databases [SQL Server], backup devices
- devices [SQL Server]
ms.assetid: 35a8e100-3ff2-4844-a5da-dd088c43cba4
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5a44b8b9c4ae4c70ec41a7c699572ecf4adcc224
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103769"
---
# <a name="backup-devices-sql-server"></a>백업 디바이스(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 백업 작업 중에 백업되는 데이터인 *백업*은 물리적 백업 디바이스에 기록됩니다. 이 물리적 백업 디바이스는 미디어 세트의 첫 번째 백업을 디바이스에 기록할 때 초기화됩니다. 하나 이상의 백업 디바이스 세트에서의 백업이 미디어 세트 하나를 구성합니다.  
   
##  <a name="TermsAndDefinitions"></a> 용어 및 정의  
 백업 디스크  
 백업 파일이 하나 이상 포함된 하드 디스크나 다른 디스크 스토리지 미디어입니다. 백업 파일은 일반적인 운영 체제 파일입니다.  
  
 미디어 세트(media set)  
 고정된 유형과 개수의 백업 디바이스를 사용하는 백업 미디어, 테이프 또는 디스크 파일을 정렬하여 모아 놓은 것입니다. 미디어 세트에 대한 자세한 내용은 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)를 참조하세요.  
  
 물리적 백업 디바이스  
 운영 체제에서 제공하는 테이프 드라이브나 디스크 파일입니다. 백업은 1개에서 64개까지의 백업 디바이스에 기록될 수 있습니다. 백업에 여러 개의 백업 디바이스가 필요한 경우 모든 디바이스 유형은 디스크 또는 테이프 중 하나로 일치해야 합니다.  
  
 디스크나 테이프뿐 아니라 Windows Azure Blob 스토리지 서비스에도 SQL Server 백업을 작성할 수 있습니다.  
 
  
##  <a name="DiskBackups"></a> 디스크 백업 디바이스 사용  
  
 백업 작업에서 미디어 세트에 백업을 추가하는 동안 디스크 파일이 꽉 차면 백업 작업이 실패합니다. 백업 파일의 최대 크기는 디스크 디바이스에서 사용 가능한 디스크 공간에 의해 결정되므로 백업 디스크 디바이스에 적합한 크기는 백업 크기에 따라 달라집니다.  
  
 디스크 백업 디바이스는 ATA 드라이브와 같은 간단한 디스크 디바이스일 수 있습니다. 또는 드라이브의 전체 디스크를 빈 디스크로 투명하게 교체할 수 있는 핫 스왑 가능 디스크 드라이브를 사용할 수 있습니다. 백업 디스크는 서버의 로컬 디스크나 공유 네트워크 리소스인 원격 디스크일 수 있습니다. 원격 디스크를 사용하는 방법은 이 항목의 뒷부분에 나오는 [네트워크 공유의 파일로 백업](#NetworkShare)을 참조하십시오.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리 도구는 디스크 파일에 타임스탬프 이름을 자동으로 생성하기 때문에 디스크 백업 디바이스를 유연하게 처리할 수 있습니다.  
  
> **중요!** 데이터베이스 데이터 및 로그 디스크가 아닌 다른 디스크를 백업 디스크로 사용하는 것이 좋습니다. 이렇게 하면 데이터 또는 로그 디스크가 실패할 경우 백업에 액세스할 수 있습니다. 
>
>데이터베이스 파일과 백업 파일이 동일한 디바이스에 있는 경우 해당 디바이스에 오류가 발생하면 데이터베이스와 백업을 모두 사용할 수 없게 됩니다. 또한 데이터베이스 파일과 백업 파일을 별개의 디바이스에 두면 데이터베이스의 프로덕션 사용과 백업 작성에 대한 I/O 성능이 모두 최적화됩니다.
  
##  <a name="BackupFileUsingPhysicalName"></a> 실제 이름을 사용하여 백업 파일 지정(Transact-SQL)  
 물리적 디바이스 이름을 사용하여 백업 파일을 지정하기 위한 기본 [BACKUP](../../t-sql/statements/backup-transact-sql.md) 구문은 다음과 같습니다.  
  
 BACKUP DATABASE *database_name*  
  
 TO DISK **=** { **'** _physical_backup_device_name_ **'**  |  **@** _physical_backup_device_name_var_ }  
  
 예를 들어  
  
```sql  
BACKUP DATABASE AdventureWorks2012   
   TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak';  
GO  
```  
  
 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 문에서 물리적 디스크 디바이스를 지정하기 위한 기본 구문은 다음과 같습니다.  
  
 RESTORE { DATABASE | LOG } *database_name*  
  
 FROM DISK **=** { **'** _physical_backup_device_name_ **'**  |  **@** _physical_backup_device_name_var_ }  
  
 예:  
  
```sql  
RESTORE DATABASE AdventureWorks2012   
   FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak';   
```  
  
  
##  <a name="BackupFileDiskPath"></a> 디스크 백업 파일 경로 지정 
 백업 파일을 지정할 경우 전체 경로 및 파일 이름을 입력해야 합니다. 파일에 백업할 때 파일 이름이나 상대 경로만 지정하면 백업 파일이 기본 백업 디렉터리에 저장됩니다. 기본 백업 디렉터리는 C:\Program Files\Microsoft SQL Server\MSSQL.*n*\MSSQL\Backup입니다. 여기서 *n* 은 서버 인스턴스의 번호입니다. 따라서 기본 서버 인스턴스의 경우 기본 백업 디렉터리는 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup입니다.  
  
 특히 스크립트에서 모호성을 피하기 위해 모든 DISK 절에 백업 디렉터리의 경로를 명시적으로 지정하는 것이 좋습니다. 그러나 쿼리 편집기를 사용할 경우 이는 그다지 중요하지 않습니다. 쿼리 편집기를 사용할 경우 백업 파일이 확실히 기본 백업 디렉터리에 있으면 DISK 절에서 경로를 생략할 수 있습니다. 예를 들어 다음 `BACKUP` 문은 기본 백업 디렉터리에 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 백업합니다.  
  
```sql  
BACKUP DATABASE AdventureWorks2012   
   TO DISK = 'AdventureWorks2012.bak';  
GO  
```  
  
> **참고:** 기본 위치는 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL.n\MSSQLServer** 아래의 **BackupDirectory**레지스트리 키에 저장됩니다.  
  
   
###  <a name="NetworkShare"></a> 네트워크 공유 파일에 백업  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 원격 디스크 파일에 액세스하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정에 네트워크 공유에 대한 액세스 권한이 있어야 합니다. 여기에는 백업 작업에서 네트워크 공유에 쓰는 데 필요한 사용 권한과 복원 작업에서 네트워크 공유를 읽는 데 필요한 사용 권한이 포함됩니다. 네트워크 드라이브 및 사용 권한의 가용성은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 실행되고 있는 컨텍스트에 따라 달라집니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 도메인 사용자 계정으로 실행 중일 때 네트워크 드라이브에 백업하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 실행되고 있는 세션에서 공유 드라이브를 네트워크 드라이브로 매핑해야 합니다. 명령줄에서 Sqlservr.exe를 시작하면 로그인 세션에서 매핑한 모든 네트워크 드라이브가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 표시됩니다.  
  
-   Sqlservr.exe를 서비스로 실행하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 로그인 세션과 관계없는 별도의 세션으로 실행됩니다. 일반적인 경우는 아니지만 서비스가 실행되는 세션에 고유하게 매핑된 드라이브가 있을 수 있습니다.  
  
-   도메인 사용자 대신 컴퓨터 계정을 사용하여 네트워크 서비스 계정과 연결할 수 있습니다. 특정 컴퓨터에서 공유 드라이브로 백업할 수 있도록 하려면 해당 컴퓨터 계정에 액세스 권한을 부여합니다. 백업을 작성하는 Sqlservr.exe 프로세스에 액세스 권한이 있으면 BACKUP 명령을 보내는 사용자에게 액세스 권한이 있는지 여부는 상관이 없습니다.  
  
    > **중요!** 네트워크를 통해 데이터를 백업하면 네트워크 오류가 발생하기 쉬우므로 원격 디스크를 사용하는 경우 완료 후에 백업 작업을 확인하는 것이 좋습니다. 자세한 내용은 [RESTORE VERIFYONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)를 참조하세요.  
  
## <a name="specify-a-universal-naming-convention-unc-name"></a>UNC(범용 명명 규칙) 이름 지정  
 백업이나 복원 명령에서 네트워크 공유를 지정하려면 백업 디바이스에 정규화된 UNC(범용 명명 규칙) 파일 이름을 사용해야 합니다. UNC 이름은 **\\\\** _Systemname_ **\\** _ShareName_ **\\** _Path_ **\\** _FileName_.  
  
 예를 들어  
  
```sql  
BACKUP DATABASE AdventureWorks2012   
   TO DISK = '\\BackupSystem\BackupDisk1\AW_backups\AdventureWorksData.Bak';  
GO  
```  
  
 
##  <a name="TapeDevices"></a> 테이프 디바이스 사용  
  
> **참고:** 테이프 백업 디바이스에 대한 지원은 이후 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제거될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요.  
   
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 테이프에 백업하려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 운영 체제에서 지원하는 테이프 드라이브 또는 드라이브를 사용해야 합니다. 또한 지정된 테이프 드라이브에는 드라이브 제조업체가 권장하는 테이프만 사용하는 것이 좋습니다. 테이프 드라이브 설치 방법은 Windows 운영 체제 설명서를 참조하십시오.  
  
 테이프 드라이브를 사용하여 백업할 경우 한 개의 테이프가 가득 차면 계속해서 다른 테이프에 백업합니다. 각 테이프에는 미디어 헤더가 있습니다. 첫 번째로 사용된 미디어를 *초기 테이프*라고 합니다. 각각의 연속되는 테이프는 *연속 테이프* 라고 하며 이전 테이프의 일련 번호보다 높은 미디어 일련 번호가 부여됩니다. 예를 들어 4개의 테이프 디바이스가 연결된 미디어 세트에는 적어도 4개의 초기 테이프가 있으며 데이터베이스가 맞지 않은 경우 4개의 연속적인 테이프가 있습니다. 백업 세트를 추가할 때 마지막 테이프를 연속하여 탑재해야 합니다. 마지막 테이프를 탑재하지 않으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 탑재된 테이프의 끝으로 빨리 감아 검색한 다음 테이프를 교체하도록 요청합니다. 이때 마지막 테이프를 탑재합니다.  
  
 테이프 백업 디바이스는 다음 사항을 제외하고 디스크 디바이스와 같이 사용됩니다.  
  
-   테이프 디바이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스를 실행하는 컴퓨터에 물리적으로 연결되어 있어야 하며 원격 테이프 디바이스로 백업할 수 없습니다.  
  
-   백업 작업 중에 테이프 백업 디바이스가 찼는데 작성할 데이터가 더 남아 있으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 새 테이프를 넣으라는 메시지를 표시하고 새 테이프가 로드된 후에 백업 작업을 계속합니다.  
  
##  <a name="BackupTapeUsingPhysicalName"></a> 실제 이름을 사용하여 백업 테이프 지정(Transact-SQL)  
 테이프 드라이브의 물리적 디바이스 이름을 사용하여 백업 테이프를 지정하기 위한 기본 [BACKUP](../../t-sql/statements/backup-transact-sql.md) 구문은 다음과 같습니다.  
  
 BACKUP { DATABASE | LOG } *database_name*  
  
 TO TAPE **=** { **'** _physical_backup_device_name_ **'**  |  **@** _physical_backup_device_name_var_ }  
  
 예를 들어  
  
```sql  
BACKUP LOG AdventureWorks2012   
   TO TAPE = '\\.\tape0';  
GO  
```  
  
 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 문에서 물리적 테이프 디바이스를 지정하기 위한 기본 구문은 다음과 같습니다.  
  
 RESTORE { DATABASE | LOG } *database_name*  
  
 FROM TAPE **=** { **'** _physical_backup_device_name_ **'**  |  **@** _physical_backup_device_name_var_ }  
  
###  <a name="TapeOptions"></a> 테이프와 관련된 BACKUP 및 RESTORE 옵션(Transact-SQL)  
 테이프를 편리하게 관리할 수 있도록 BACKUP 문은 다음과 같은 테이프 관련 옵션을 제공합니다.  
  
-   { NOUNLOAD | **UNLOAD** }  
  
     백업 또는 복원 작업 후에 테이프 드라이브에서 자동으로 백업 테이프를 언로드할지 여부를 제어할 수 있습니다. UNLOAD/NOUNLOAD는 세션 기간 동안이나 다른 옵션을 지정하여 다시 설정할 때까지 유지되는 세션 설정입니다.  
  
-   { **REWIND** | NOREWIND }  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 백업이나 복원 작업 후에 테이프를 열어 놓을지 또는 테이프가 꽉 찬 후에 테이프를 해제하고 되감을지를 제어할 수 있습니다. 기본 동작은 테이프를 되감는 것입니다(REWIND).  
  
> **참고:** BACKUP 구문 및 인수에 대한 자세한 내용은 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)을 참조하세요. RESTORE 구문 및 인수에 대한 자세한 내용은 각각 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md) 및 [RESTORE 인수&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)를 참조하세요.  
  
###  <a name="OpenTapes"></a> 열려 있는 테이프 관리  
 열려 있는 테이프 디바이스 목록 및 탑재 요청 상태를 보려면 [sys.dm_io_backup_tapes](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md) 동적 관리 뷰를 쿼리합니다. 이 뷰는 다음 BACKUP 또는 RESTORE 작업을 기다리는 동안 일시적으로 유휴 상태에 있는 사용 중인 테이프를 비롯하여 열려 있는 모든 테이프를 표시합니다.  
  
 테이프를 실수로 열어 놓은 경우 테이프를 해제하는 가장 빠른 방법은 RESTORE REWINDONLY FROM TAPE **=** _backup_device_name_ 명령을 사용하는 것입니다. 자세한 내용은 [RESTORE REWINDONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)를 참조하세요.  
  
  
## <a name="using-the-windows-azure-blob-storage-service"></a>Microsoft Azure Blob Storage 서비스 사용  
 Windows Azure Blob Storage Service에 SQL Server 백업을 작성할 수 있습니다.  Microsoft Azure Blob Storage 서비스를 백업에 사용하는 방법은 [Microsoft Azure Blob Storage 서비스로 SQL Server 백업 및 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)을 참조하세요.  
  
##  <a name="LogicalBackupDevice"></a> 논리적 백업 디바이스 사용  
 *논리적 백업 디바이스*는 특정 물리적 백업 디바이스(디스크 파일 또는 테이프 드라이브)를 가리키는 선택적인 사용자 정의 이름입니다. 논리적 백업 디바이스를 사용하면 해당 물리적 백업 디바이스를 참조할 때 간접 참조를 사용할 수 있습니다.  
  
 논리적 백업 디바이스를 정의하려면 물리적 디바이스에 논리적 이름을 할당합니다. 예를 들어 논리적 디바이스인 AdventureWorksBackups가 Z:\SQLServerBackups\AdventureWorks2012.bak 파일이나 \\\\.\tape0 테이프 드라이브를 가리키도록 정의할 수 있습니다. 그런 다음 백업 및 복원 명령에서 DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak' 또는 TAPE = '\\\\.\tape0' 대신 AdventureWorksBackups를 백업 디바이스로 지정할 수 있습니다.  
  
 논리적 디바이스 이름은 서버 인스턴스의 모든 논리적 백업 디바이스에서 고유해야 합니다. 기존의 논리적 디바이스 이름을 보려면 [sys.backup_devices](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md) 카탈로그 뷰를 쿼리합니다. 이 뷰는 각 논리적 백업 디바이스의 이름을 표시하고 해당하는 물리적 백업 디바이스의 유형과 물리적 파일 이름 또는 경로를 설명합니다.  
  
 논리적 백업 디바이스를 정의한 후에는 BACKUP 또는 RESTORE 명령에서 디바이스의 실제 이름 대신 논리적 백업 디바이스를 지정할 수 있습니다. 예를 들어 다음 문은 `AdventureWorks2012` 논리적 백업 디바이스에 `AdventureWorksBackups` 데이터베이스를 백업합니다.  
  
```sql  
BACKUP DATABASE AdventureWorks2012   
   TO AdventureWorksBackups;  
GO  
```  
  
> **참고:** 지정된 BACKUP 또는 RESTORE 문에서 논리적 백업 디바이스 이름과 해당 물리적 백업 디바이스 이름을 바꾸어 사용할 수 있습니다.  
  
 논리적 백업 디바이스는 긴 경로보다 사용이 편리하다는 장점이 있습니다. 동일한 경로 또는 테이프 디바이스에 일련의 백업을 작성하려는 경우 논리적 백업 디바이스를 사용하면 도움이 될 수 있습니다. 논리적 백업 디바이스는 특히 테이프 백업 디바이스를 식별하는 데 유용합니다.  
  
 특정 논리적 백업 디바이스를 사용하도록 백업 스크립트를 작성할 수 있습니다. 이렇게 하면 스크립트를 업데이트하지 않고도 새로운 물리적 백업 디바이스로 전환할 수 있습니다. 전환 과정은 다음과 같습니다.  
  
1.  원래의 논리적 백업 디바이스 삭제  
  
2.  원래의 논리적 디바이스 이름을 사용하지만 다른 물리적 백업 디바이스에 매핑되는 새 논리적 백업 디바이스 정의. 논리적 백업 디바이스는 특히 테이프 백업 디바이스를 식별하는 데 유용합니다.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

##  <a name="MirroredMediaSets"></a> 미러된 백업 미디어 세트  
 백업 미디어 세트를 미러링하면 백업 장치의 오작동에 따른 영향이 줄어듭니다. 데이터 손실을 방지할 수 있는 최후의 수단이 백업이므로 이러한 오작동은 특히 심각합니다. 데이터베이스의 크기가 커지면 백업 디바이스 또는 미디어의 실패로 인해 복원 불가능한 백업을 만들게 될 가능성이 커집니다. 백업 미디어를 미러링하면 물리적 백업 디바이스에 중복을 제공하여 백업의 안정성이 향상됩니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [미러된 백업 미디어 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)백업 및 복원의 기본적인 백업 미디어 관련 용어를 소개합니다.  
  
> **참고:** 미러된 백업 미디어 세트는 [!INCLUDE[ssEnterpriseEd2005](../../includes/ssenterpriseed2005-md.md)] 이상 버전에서만 지원됩니다.  
  
  
##  <a name="Archiving"></a> SQL Server 백업 보관  
 파일 시스템 백업 유틸리티를 사용하여 디스크 백업을 보관하고 오프사이트에 보관 파일을 저장하는 것이 좋습니다. 디스크를 사용할 경우 보관된 백업을 네트워크를 통해 오프사이트 디스크에 쓸 수 있다는 장점이 있습니다. Windows Azure Blob 스토리지 서비스를 오프 사이트 보관 옵션으로 사용할 수 있습니다.  Windows Azure Blob 스토리지 서비스에 디스크 백업을 업로드하거나 백업을 직접 작성할 수 있습니다.  
  
 다른 일반적인 보관 방법은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업을 로컬 백업 디스크에 쓰고 테이프에 보관한 다음 오프사이트에 테이프를 저장하는 것입니다.  

  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **디스크 디바이스를 지정하려면(SQL Server Management Studio)**  
  
-   [디스크 또는 테이프를 백업 대상으로 지정&#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
 **테이프 디바이스를 지정하려면(SQL Server Management Studio)**  
  
-   [디스크 또는 테이프를 백업 대상으로 지정&#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
 **논리적 백업 디바이스를 정의하려면**  
  
-   [sp_addumpdevice&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)  
  
-   [디스크 파일에 대한 논리적 백업 디바이스 정의&#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [테이프 드라이브에 대한 논리적 백업 디바이스 정의&#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.BackupDevice> (SMO)  
  
 **논리적 백업 디바이스를 사용하려면**  
  
-   [디스크 또는 테이프를 백업 대상으로 지정&#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [디바이스에서 백업 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)  
  
-   [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)  
  
-   [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 **백업 디바이스에 대한 정보를 보려면**  
  
-   [백업 기록 및 헤더 정보&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
-   [논리적 백업 디바이스의 속성 및 내용 보기&#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [백업 테이프 또는 파일의 내용 보기&#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
 **논리적 백업 디바이스를 삭제하려면**  
  
-   [sp_dropdevice&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)  
  
-   [백업 디바이스 삭제&#40;SQL Server&#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server, Backup Device 개체](../../relational-databases/performance-monitor/sql-server-backup-device-object.md)   
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [유지 관리 계획](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE LABELONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)   
 [sys.backup_devices&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)   
 [sys.dm_io_backup_tapes&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md)   
 [미러된 백업 미디어 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)  
  
  
