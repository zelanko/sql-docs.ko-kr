---
description: RESTORE 문 - VERIFYONLY(Transact-SQL)
title: RESTORE VERIFYONLY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- VERIFYONLY
- RESTORE VERIFYONLY
- VERIFYONLY_TSQL
- RESTORE_VERIFYONLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RESTORE VERIFYONLY statement
- backups [SQL Server], verifying
- verifying backups
- checking backups
ms.assetid: cba3b6a0-b48e-4c94-812b-5b3cbb408bd6
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||>=sql-server-linux-2017
ms.openlocfilehash: 00926a8ee1244112d1fb5a01273e90d22a5753a7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463973"
---
# <a name="restore-statements---verifyonly-transact-sql"></a>RESTORE 문 - VERIFYONLY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md )]

  백업을 확인하되 복원하지는 않으며, 백업 세트가 완성되었는지와 전체 백업을 읽을 수 있는지를 확인합니다. 그러나 RESTORE VERIFYONLY는 백업 볼륨에 포함된 데이터의 구조를 확인하지는 않습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 RESTORE VERIFYONLY를 개선하여 데이터에 대한 추가 검사를 수행하는 방법으로 오류 발견율을 높였습니다. 가능한 한 실제에 가깝도록 데이터를 복원하는 것이 목표입니다. 자세한 내용은 주의 섹션을 참조하십시오.  

 백업이 유효한 경우 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 성공 메시지를 반환합니다.  
  
> [!NOTE]  
>  인수에 대한 자세한 설명은 [RESTORE 인수&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
RESTORE VERIFYONLY  
FROM <backup_device> [ ,...n ]  
[ WITH    
 {  
   LOADHISTORY   
  
--Restore Operation Option  
 | MOVE 'logical_file_name_in_backup' TO 'operating_system_file_name'   
          [ ,...n ]   
  
--Backup Set Options  
 | FILE = { backup_set_file_number | @backup_set_file_number }   
 | PASSWORD = { password | @password_variable }   
  
--Media Set Options  
 | MEDIANAME = { media_name | @media_name_variable }   
 | MEDIAPASSWORD = { mediapassword | @mediapassword_variable }  
  
--Error Management Options  
 | { CHECKSUM | NO_CHECKSUM }   
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }  
  
--Monitoring Options  
 | STATS [ = percentage ]   
  
--Tape Options  
 | { REWIND | NOREWIND }   
 | { UNLOAD | NOUNLOAD }    
 } [ ,...n ]  
]  
[;]  
  
<backup_device> ::=  
{   
   { logical_backup_device_name |  
      @logical_backup_device_name_var }  
   | { DISK | TAPE | URL } = { 'physical_backup_device_name' |  
       @physical_backup_device_name_var }   
}  
  
```  
 > [!NOTE] 
> URL은 Microsoft Azure Blob Storage의 위치 및 파일 이름을 지정하는 데 사용되는 형식이며 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2부터 지원됩니다. Microsoft Azure Blob Storage는 서비스이지만, 모든 세 디바이스에 대해 일관되고 원활한 복원 환경을 가능하게 하는 디스크와 테이프와 구현이 유사합니다.
 
## <a name="arguments"></a>인수  
 RESTORE VERIFYONLY 인수에 대한 설명은 [RESTORE 인수&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)를 참조하세요.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 Microsoft Tape Format으로 해석할 수 있도록 미디어 세트 또는 백업 세트는 최소한의 올바른 정보를 포함해야 합니다. 그렇지 않을 경우 RESTORE VERIFYONLY가 중지되고 백업 형식이 잘못되었다는 메시지가 나타납니다.  
  
 RESTORE VERIFYONLY는 다음 사항을 확인합니다.  
  
-   백업 세트가 완료되었고 모든 볼륨이 읽기가 가능한지 확인합니다.  
  
-   데이터 기록 방식과 유사하게 페이지 ID 등 데이터베이스 페이지의 일부 헤더 필드를 확인합니다.  
  
-   체크섬을 확인합니다(미디어에 있을 경우).  
  
-   대상 디바이스에 충분한 공간이 있는지 확인합니다.  
  
> [!NOTE]  
>  RESTORE VERIFYONLY는 데이터베이스 스냅샷에서는 작동하지 않습니다. 되돌리기 작업을 수행하기 전에 데이터베이스 스냅샷을 확인하려면 DBCC CHECKDB를 실행합니다.  
  
> [!NOTE]  
>  스냅샷 백업을 사용하여 RESTORE VERIFYONLY는 백업 파일에 지정된 위치에 스냅샷의 존재 여부를 확인합니다. 스냅샷 백업은 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]의 새로운 기능입니다. 스냅샷 백업에 대한 자세한 내용은 [Azure의 데이터베이스 파일에 대한 파일-스냅샷 백업](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)을 참조하세요.  
  
## <a name="security"></a>보안  
 필요한 경우 백업 작업에서 미디어 세트, 백업 세트 또는 이 둘 모두에 대해 암호를 지정할 수 있습니다. 미디어 세트나 백업 세트에 암호가 정의되어 있는 경우 RESTORE 문에서 정확한 암호를 지정해야 합니다. 이러한 암호를 지정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 도구를 사용하여 무단으로 복원 작업을 수행하거나 미디어에 백업 세트를 무단으로 추가하는 작업을 방지할 수 있습니다. 하지만 암호를 사용해도 BACKUP 문의 FORMAT 옵션을 사용하여 미디어를 덮어쓰는 작업은 수행됩니다.  
  
> [!IMPORTANT]  
>  이 암호에 의한 보호 수준은 낮습니다. 권한 유무에 관계없이 사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 도구를 사용하여 잘못된 복원을 수행하는 것을 방지합니다. 다른 수단을 사용한 백업 데이터 읽기나 암호 바꾸기를 방지하지는 않습니다. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]백업을 보호하는 최선의 구현 방법은 백업 테이프를 안전한 장소에 보관하거나 적합한 ACL(액세스 제어 목록)로 보호되는 디스크 파일에 백업하는 것입니다. ACL은 백업이 만들어지는 디렉터리 루트에 설정해야 합니다.  
  
### <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터는 백업 세트나 백업 디바이스에 대한 정보를 얻으려면 CREATE DATABASE 권한이 필요합니다. 자세한 내용은 [GRANT 데이터베이스 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)을 참조하세요.  
 
## <a name="examples"></a>예제  
 다음 예제에서는 디스크에서 백업을 확인합니다.
  
```sql  
RESTORE VERIFYONLY FROM DISK = 'D:\AdventureWorks.bak';
GO
```  
  
## <a name="see-also"></a>참고 항목  
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE REWINDONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [백업 기록 및 헤더 정보&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  
