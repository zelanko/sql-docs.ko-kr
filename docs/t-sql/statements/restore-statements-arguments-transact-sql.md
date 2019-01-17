---
title: RESTORE 인수(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- RESTORE statement, arguments
- RESTORE statement
ms.assetid: 4bfe5734-3003-4165-afd4-b1131ea26e2b
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 78dfe43617d9a519b479e53abbabcf311d726b1d
ms.sourcegitcommit: 467b2c708651a3a2be2c45e36d0006a5bbe87b79
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53980519"
---
# <a name="restore-statements---arguments-transact-sql"></a>RESTORE 문 - 인수(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

이 항목에서는 RESTORE {DATABASE|LOG} 문과 관련 보조 문 집합인 RESTORE FILELISTONLY, RESTORE HEADERONLY, RESTORE LABELONLY, RESTORE REWINDONLY 및 RESTORE VERIFYONLY 등이 있습니다. 대부분의 인수는 이러한 6개의 문에 사용되는 경우에만 지원됩니다. 각 인수에 대한 지원은 인수 설명에 나와 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
 구문에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [RESTORE FILELISTONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
-   [RESTORE HEADERONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE LABELONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)  
  
-   [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)  
  
-   [RESTORE VERIFYONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
## <a name="arguments"></a>인수  
 DATABASE  
 **지원 요소:**  [복원](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 대상 데이터베이스를 지정합니다. 파일 및 파일 그룹의 목록이 지정되어 있으면 해당 파일 및 파일 그룹만 복원됩니다.  
  
 전체 또는 대량 로그 복구 모델을 사용하는 데이터베이스의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 대개 데이터베이스를 복원하기 전에 비상 로그 백업을 수행해야 합니다. RESTORE DATABASE 문에 데이터 백업이 종료된 후 발생한 시간 또는 트랜잭션을 지정해야 하는 WITH REPLACE나 WITH STOPAT 절이 포함되어 있지 않은 경우 비상 로그 백업을 먼저 수행하지 않고 데이터베이스를 복원하면 오류가 발생합니다. 비상 로그 백업에 대한 자세한 내용은 [비상 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)을 참조하세요.  
  
 LOG  
 **지원 요소:**  [복원](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 해당 데이터베이스에 트랜잭션 로그 백업을 적용하도록 지정합니다. 순차적으로 트랜잭션 로그를 적용해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 트랜잭션 로그가 올바른 시퀀스로 해당 데이터베이스로 로드될 수 있도록 백업한 트랜잭션 로그를 확인합니다. 여러 트랜잭션 로그를 적용하려면 마지막 복원 작업을 제외한 모든 복원 작업에 NORECOVERY 옵션을 사용하십시오.  
  
> [!NOTE]  
>  일반적으로 마지막으로 복원된 로그가 비상 로그 백업입니다. *비상 로그 백업*은 일반적으로 데이터베이스에서 오류가 발생한 후 데이터베이스를 복원하기 직전에 수행되는 로그 백업입니다. 손상될 가능성이 있는 데이터베이스에서 비상 로그 백업을 수행하면 아직 백업되지 않은 로그(비상 로그)를 캡처하여 작업이 손실되지 않도록 방지할 수 있습니다. 자세한 내용은 [비상 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)을 참조하세요.  
  
 자세한 내용은 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)을 참조하세요.  
  
 { _database\_name_ | **@**_database\_name\_var_}  
 **지원 요소:**  [복원](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 로그나 전체 데이터베이스가 복원되는 데이터베이스입니다. 변수(**@**_database\_name\_var_)로 제공된 경우, 이 이름은 문자열 상수(**@**_database\_name\_var_ = *database*\_*name*)나 **ntext** 또는 **text** 데이터 형식을 제외한 문자열 데이터 형식의 변수로 지정할 수 있습니다.  
  
 \<file_or_filegroup_or_page> [ **,**...*n* ]  
 **지원 요소:**  [복원](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 RESTORE DATABASE 또는 RESTORE LOG 문에 포함할 논리적 파일이나 파일 그룹 또는 페이지의 이름을 지정합니다. 파일 또는 파일 그룹의 목록을 지정할 수 있습니다.  
  
 단순 복구 모델을 사용하는 데이터베이스의 경우 FILE 및 FILEGROUP 옵션은 대상 파일 또는 파일 그룹이 읽기 전용이거나 PARTIAL 복원인 경우에만 사용할 수 있으며 그 결과 [비활성화된 파일 그룹](../../relational-databases/backup-restore/remove-defunct-filegroups-sql-server.md)이 생성됩니다.  
  
 전체 또는 대량 로그 복구 모델을 사용하는 데이터베이스의 경우 일반적으로 RESTORE DATABASE를 사용하여 하나 이상의 파일, 파일 그룹 및/또는 페이지를 복원한 후 복원된 데이터를 포함하는 파일에 트랜잭션 로그를 적용해야 합니다. 로그를 적용하면 해당 파일이 데이터베이스의 나머지 부분과 일치하게 됩니다. 다음과 같은 경우는 예외입니다.  
  
-   복원할 파일이 마지막으로 백업되기 전에 읽기 전용으로 설정된 경우 트랜잭션 로그를 적용할 필요가 없으며 RESTORE 문에서 이러한 상황에 대해 알려줍니다.  
  
-   백업에 주 파일 그룹이 포함되고 부분 복원이 수행되고 있는 경우. 이런 경우에는 로그가 백업 세트에서 자동으로 복원되기 때문에 복원 로그가 필요하지 않습니다.  
  
FILE **=** { *logical_file_name_in_backup*| **@**_logical\_file\_name\_in\_backup\_var_}  
 데이터베이스 복원에 포함할 파일의 이름을 지정합니다.  
  
FILEGROUP **=** { *logical_filegroup_name* | **@**_logical\_filegroup\_name\_var_ }  
 데이터베이스 복원에 포함할 파일 그룹의 이름을 지정합니다.  
  
 **참고** FILEGROUP은 지정한 파일 그룹이 읽기 전용이고 부분 복원인 경우 즉, WITH PARTIAL이 사용되는 경우에만 단순 복구 모델에서 사용할 수 있습니다. 복원되지 않은 읽기/쓰기 파일 그룹은 존재하지 않는 것으로 표시되므로 결과 데이터베이스로 복원할 수 없습니다.  
  
READ_WRITE_FILEGROUPS  
 모든 읽기/쓰기 파일 그룹을 선택합니다. 이 옵션은 읽기/쓰기 파일 그룹 다음에 복원할 읽기 전용 파일 그룹이 읽기 전용 파일 그룹 앞에 있는 경우에 특히 유용합니다.  
  
PAGE = **'**_file_**:**_page* [ **,**...*n* ]**'**  
 전체 복구 모델 또는 대량 로그 복구 모델을 사용하는 데이터베이스에만 지원되는 페이지 복원의 페이지 목록을 지정합니다. 값은 다음과 같습니다.  
  
PAGE  
 하나 이상의 파일 및 페이지 목록을 나타냅니다.  
  
 *file*  
 복원할 특정 페이지를 포함하는 파일의 ID입니다.  
  
 *page*  
 파일 내에서 복원할 페이지의 페이지 ID입니다.  
  
 *n*  
 여러 페이지를 지정할 수 있음을 나타내는 자리 표시자입니다.  
  
 복원 순서에서 단일 파일로 복원할 수 있는 최대 페이지 수는 1000입니다. 그러나 파일에 손상된 페이지가 많은 경우 페이지 대신 전체 파일을 복원하십시오.  
  
> [!NOTE]  
>  페이지 복원은 복구되지 않습니다.  
  
 페이지 복원에 대한 자세한 내용은 [페이지 복원 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)를 참조하세요.  
  
 [ **,**...*n* ]  
 여러 개의 파일 및 파일 그룹과 페이지를 쉼표로 구분된 목록에 지정할 수 있음을 나타내는 자리 표시자입니다. 사용할 수 있는 숫자에는 제한이 없습니다.  
  
FROM { \<backup_device&gt; [ **,**...*n* ]| \<database_snapshot&gt; } 일반적으로 백업을 복원할 백업 디바이스를 지정합니다. 또는 RESTORE DATABASE 문의 FROM 절에서 데이터베이스를 되돌릴 데이터베이스 스냅숏의 이름을 지정할 수도 있습니다. 이런 경우 WITH 절은 사용할 수 없습니다.  
  
 FROM 절을 생략하면 백업이 복원되지 않습니다. 대신 데이터베이스가 복원됩니다. 이렇게 하면 NORECOVERY 옵션으로 복원된 데이터베이스를 복구하거나 대기 중인 서버로 전환할 수 있습니다. FROM 절을 생략하면 WITH 절에서 NORECOVERY, RECOVERY 또는 STANDBY를 지정해야 합니다.  
  
 \<backup_device&gt; [ **,**...*n* ] 복원 작업에 사용할 논리적 또는 물리적 백업 디바이스를 지정합니다.  
  
 **지원 요소:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md), [RESTORE REWINDONLY](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md) 및 [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 \<backup_device&gt;::= 다음과 같이 백업 작업에 사용할 논리적 백업 디바이스나 물리적 백업 디바이스를 지정합니다.  
  
 { _logical\_backup\_device\_name_ | **@**_logical\_backup\_device\_name\_var_ }  
 데이터베이스가 복원되는 **sp_addumpdevice**에서 만든 백업 디바이스의 논리적 이름입니다. 이 논리적 이름은 식별자에 대한 규칙을 따라야 합니다. 변수(**@**_logical\_backup\_device\_name\_var_)로 제공한 경우 백업 디바이스 이름은 문자열 상수(**@**_logical\_backup\_device\_name\_var_ = _logical\_backup\_device\_name_)나 **ntext** 또는 **text** 데이터 형식을 제외한 문자열 데이터 형식의 변수로 지정할 수 있습니다.  
  
 {DISK | TAPE } **=** { **'**_physical\_backup\_device\_name_**'** | **@**_physical\_backup\_device\_name\_var_ }  
 지정한 디스크나 테이프 장치에서 백업을 복원할 수 있습니다. 디스크나 테이프의 디바이스 유형은 전체 경로와 파일 이름을 포함한 디바이스의 실제 이름으로 지정해야 합니다. `DISK ='Z:\SQLServerBackups\AdventureWorks.bak'` 또는 `TAPE ='\\\\.\TAPE0'`. 변수(**@**_physical\_backup\_device\_name\_var_)로 지정한 경우 디바이스 이름은 문자열 상수(**@**_physical\_backup\_device\_name\_var_ = '*physical_backup_device_name*')나 **ntext** 또는 **text** 데이터 형식을 제외한 문자열 데이터 형식의 변수로 지정할 수 있습니다.  
  
 네트워크 서버에 UNC 이름(컴퓨터 이름 포함)을 사용하는 경우 디스크의 장치 유형을 지정합니다. UNC 이름을 사용하는 방법에 대한 자세한 내용은 [백업 디바이스&amp;#40;SQL Server&amp;#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)를 참조하세요.  
  
 RESTORE 작업을 수행하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하는 계정에 원격 컴퓨터나 네트워크 서버에 대한 READ 권한이 있어야 합니다.  
  
 *n*  
 최대 64개의 백업 장치를 쉼표로 구분된 목록에 지정할 수 있음을 나타내는 자리 표시자입니다.  
  
 복원 순서에 백업이 속한 미디어 세트를 만드는 데 사용된 것만큼의 백업 장치가 필요한지 여부는 복원이 오프라인인지, 아니면 온라인인지에 따라 다음과 같이 달라집니다.  
  
-   오프라인 복원의 경우 백업을 만들 때 보다 적은 장치를 사용하여 백업을 복원할 수 있습니다.  
  
-   온라인 복원의 경우 백업을 만들 때 사용된 백업 장치가 모두 필요합니다. 필요한 장치를 모두 사용하지 않으면 복원이 실패합니다.  
  
 예를 들어 서버에 연결된 4개의 테이프 드라이브로 데이터베이스가 백업된 경우를 고려해 보십시오. 온라인 복원을 수행하려면 서버에 4개의 드라이브가 연결되어 있어야 합니다. 오프라인 복원에서는 시스템의 드라이브가 4개 이하인 경우에도 백업을 복원할 수 있습니다.  
  
> [!NOTE]  
>  미러된 미디어 세트의 백업을 복원하려는 경우 각 미디어 패밀리에 하나의 미러만 지정할 수 있습니다. 그러나 오류가 발생할 때 다른 미러가 있으면 일부 복원 문제를 빨리 해결할 수 있습니다. 손상된 미디어 볼륨은 다른 미러에서 상응하는 볼륨으로 대체할 수 있습니다. 오프라인 복원의 경우 미디어 패밀리보다 적은 수의 장치에서 복원할 수 있지만 각 패밀리는 한 번만 처리됩니다.  
  
\<database_snapshot>::=  
**지원 요소:**  [데이터베이스 복원](../../t-sql/statements/restore-statements-transact-sql.md)  
  
DATABASE_SNAPSHOT **=**_database\_snapshot\_name_  
 데이터베이스를 *database_snapshot_name*으로 지정한 데이터베이스 스냅숏으로 되돌립니다. DATABASE_SNAPSHOT 옵션은 전체 데이터베이스 복원에만 사용할 수 있습니다. 되돌리기 작업에서는 데이터베이스 스냅숏이 전체 데이터베이스 백업을 대신합니다.  
  
 되돌리기 작업을 수행하려면 지정한 데이터베이스 스냅숏이 데이터베이스에서 유일한 스냅숏이어야 합니다. 되돌리기 작업 중에 데이터베이스 스냅숏과 대상 데이터베이스는 둘 다 `In restore`로 표시됩니다. 자세한 내용은 [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md)의 "주의" 섹션을 참조하세요.  
  
### <a name="with-options"></a>WITH 옵션  
 복원 작업에서 사용할 옵션을 지정합니다. 각 옵션을 사용하는 문에 대한 간략한 설명은 이 항목의 뒷부분에 나오는 "WITH 옵션 지원에 대한 요약"을 참조하십시오.  
  
> [!NOTE]  
>  여기서 WITH 옵션은 [RESTORE {DATABASE|LOG}](../../t-sql/statements/restore-statements-transact-sql.md)의 "구문" 섹션에서와 동일한 순서로 구성됩니다.  
  
 PARTIAL  
 **지원 요소:**  [데이터베이스 복원](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 주 파일 그룹과 지정한 보조 파일 그룹을 복원하는 부분 복원 작업을 지정합니다. PARTIAL 옵션은 암시적으로 주 파일 그룹을 선택하므로 FILEGROUP = 'PRIMARY'를 지정할 필요가 없습니다. 보조 파일 그룹을 복원하려면 FILE 옵션이나 FILEGROUP 옵션을 사용하여 명시적으로 파일 그룹을 지정해야 합니다.  
  
 PARTIAL 옵션은 RESTORE LOG 문에서 사용할 수 없습니다.  
  
 PARTIAL 옵션은 증분 복원의 초기 단계를 시작합니다. 나머지 파일 그룹은 나중에 복원할 수 있습니다. 자세한 내용은 [증분 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)을 참조하세요.  
  
 [ **RECOVERY** | NORECOVERY | STANDBY ]  
 **지원 요소:**  [복원](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 **RECOVERY**  
 복원 작업에서 커밋되지 않은 트랜잭션을 모두 롤백하도록 지정합니다. 복원을 수행한 다음 데이터베이스를 사용할 수 있습니다. NORECOVERY, RECOVERY와 STANDBY를 지정하지 않으면 RECOVERY가 기본값이 됩니다.  
  
 후속 RESTORE 작업(차등의 RESTORE LOG 또는 RESTORE DATABASE)을 할 경우에는 대신 NORECOVERY나 STANDBY를 지정해야 합니다.  
  
 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 백업 세트를 복원할 경우 데이터베이스를 업그레이드해야 합니다. WITH RECOVERY를 지정하면 자동으로 업그레이드됩니다. 자세한 내용은 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)을 참조하세요.  
  
> [!NOTE]  
>  FROM 절을 생략하면 WITH 절에서 NORECOVERY, RECOVERY 또는 STANDBY를 지정해야 합니다.  
  
 NORECOVERY  
 복원 작업에서 커밋되지 않은 트랜잭션을 롤백하지 않도록 지정합니다. 나중에 다른 트랜잭션 로그를 적용해야 하는 경우에는 NORECOVERY나 STANDBY 옵션을 지정하십시오. NORECOVERY, RECOVERY와 STANDBY를 지정하지 않으면 RECOVERY가 기본값이 됩니다. NORECOVERY 옵션을 사용하여 오프라인 복원 작업을 수행하는 동안에는 데이터베이스를 사용할 수 없습니다.  
  
 데이터베이스 백업 및 하나 이상의 트랜잭션 로그를 복원하려는 경우나 여러 RESTORE 문이 필요할 때(예: 전체 데이터베이스 백업을 복원한 다음 차등 데이터베이스 백업을 복원하려는 경우)마다 RESTORE 옵션을 사용하려면 최종 RESTORE 문을 제외한 모든 문에 WITH NORECOVERY 옵션이 필요합니다. 따라서 원하는 복구 지점에 도달할 때까지 여러 단계로 구성된 복원 순서의 모든 문에서 WITH NORECOVERY 옵션을 사용한 다음 복구에만 별도의 RESTORE WITH RECOVERY 문을 사용하는 것이 좋습니다.  
  
 파일이나 파일 그룹 복원 작업에 사용할 경우 NORECOVERY를 사용하면 복원 작업 후에 데이터베이스는 복원 상태로 남아있게 됩니다. 다음과 같은 경우 유용합니다.  
  
-   복원 스크립트를 실행하고 항상 로그를 적용할 경우  
  
-   일련의 파일 복원을 사용하고 두 개의 복원 작업 시 데이터베이스를 사용할 경우  
  
 경우에 따라 RESTORE WITH NORECOVERY 옵션은 데이터베이스와 일치되도록 롤포워드 세트를 충분히 롤포워드합니다. 이런 경우 예상대로 롤백은 발생하지 않고 데이터는 오프라인 상태로 유지됩니다. 그러나 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에는 RECOVERY 옵션을 사용하여 롤포워드 세트를 복구할 수 있다는 정보 메시지가 표시됩니다.  
  
STANDBY **=**_standby\_file\_name_  
 복구 결과를 취소할 수 있는 대기 파일을 지정합니다. STANDBY 옵션은 부분 복원을 포함하는 오프라인 복원에 사용할 수 있으며 온라인 복원에는 사용할 수 없습니다. 온라인 복원 작업에 STANDBY 옵션을 지정하려고 하면 복원 작업이 실패하게 됩니다. 데이터베이스 업그레이드가 필요한 경우에도 STANDBY를 사용할 수 없습니다.  
  
 대기 파일은 RESTORE WITH STANDBY의 실행 취소 패스 중에 수정된 페이지에 대한 "쓰기 시 복사" 기존 이미지를 유지하는 데 사용됩니다. 대기 파일을 사용하면 트랜잭션 로그 복원 시 읽기 전용 액세스를 위해 데이터베이스를 가져와 대기 중인 서버 상태나 로그 복원 시 데이터베이스를 검사하는 데 유용한 특수한 복원 상태에 사용할 수 있습니다. RESTORE WITH STANDBY 작업이 완료되면 다음 RESTORE 작업에 의해 실행 취소 파일이 자동으로 삭제됩니다. 다음 RESTORE 작업이 수행되기 전에 이 대기 파일을 수동으로 삭제하면 전체 데이터베이스를 다시 복원해야 합니다. 데이터베이스가 STANDBY 상태에 있으면 다른 데이터베이스 파일과 마찬가지로 주의 깊게 이 대기 파일을 처리해야 합니다. 다른 데이터베이스 파일과 달리 이 파일은 활성 복원 작업 중에 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 의해서만 열려 있습니다.  
  
 *standby_file_name*은 데이터베이스 로그에 위치가 저장되는 대기 파일을 지정합니다. 기존 파일이 지정한 이름을 사용하고 있으면 해당 파일을 덮어쓰고 그렇지 않으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 파일을 만듭니다.  
  
 지정된 대기 파일의 크기 요구 사항은 복원 작업 중에 실행된 커밋되지 않은 트랜잭션의 결과로 발생하는 실행 취소 동작의 볼륨에 따라 달라집니다.  
  
> [!IMPORTANT]  
>  지정한 대기 파일 이름을 포함하는 드라이브의 여유 공간이 모두 사용된 경우에는 복원 작업이 중지됩니다.  
  
 RECOVERY 옵션과 NORECOVERY 옵션에 대한 비교는 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)의 "주의" 섹션을 참조하세요.  
  
LOADHISTORY  
 **지원 요소:**  [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
 복원 작업에서 **msdb** 기록 테이블로 정보를 로드하도록 지정합니다. LOADHISTORY 옵션은 확인하려는 단일 백업 세트에 대해 미디어 세트에 저장된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업에 대한 정보를 **msdb** 데이터베이스의 백업 및 복원 기록 테이블로 로드합니다. 기록 테이블에 대한 자세한 내용은 [System Tables &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)을 참조하세요.  
  
#### <a name="generalwithoptions--n-"></a>\<general_WITH_options> [ ,...n ]  
 일반 WITH 옵션은 모두 RESTORE DATABASE 및 RESTORE LOG 문에서 지원됩니다. 일부 옵션은 아래에 설명된 하나 이상의 보조 문에서도 지원됩니다.  
  
##### <a name="restore-operation-options"></a>복원 작업 옵션  
 이러한 옵션은 복원 작업의 동작에 영향을 줍니다.  
  
MOVE **'**_logical\_file\_name\_in\_backup_**'** TO **'**_operating\_system\_file\_name_**'** [ ...*n* ]  
 **지원 요소:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 및 [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
 *logical_file_name_in_backup*에 논리적 이름이 지정된 데이터 또는 로그 파일을 *operating_system_file_name*에 지정된 위치로 복원하여 제거하도록 지정합니다. 백업 세트에 있는 데이터 또는 로그 파일의 논리적 파일 이름은 백업 세트 생성 시 데이터베이스의 해당 논리적 이름과 일치합니다.  
  
*n*은 추가 MOVE 문을 지정할 수 있음을 나타내는 자리 표시자입니다. 백업 세트에서 새 위치로 복원할 모든 논리적 파일에 대해 MOVE 문을 지정합니다. 기본적으로 *logical_file_name_in_backup* 파일은 원래 위치로 복원됩니다.  
  
> [!NOTE]  
>  백업 세트에서 논리적 파일 목록을 가져오려면 RESTORE FILELISTONLY를 사용하십시오.  
  
 RESTORE 문을 사용하여 동일한 서버에서 데이터베이스의 위치를 다시 지정하거나 다른 서버에 데이터베이스를 복사하는 경우 데이터베이스 파일의 위치를 다시 지정하고 기존 파일과 충돌을 피하는 데 MOVE 옵션이 필요할 수 있습니다.  
  
 RESTORE LOG와 함께 사용할 경우 MOVE 옵션은 복원할 로그에 포함된 기간 동안 추가된 파일의 위치를 다시 지정하는 데만 사용할 수 있습니다. 예를 들어 로그 백업에 `file23` 파일에 대한 파일 추가 작업이 포함되면 이 파일의 위치는 RESTORE LOG에서 MOVE 옵션을 사용하여 다시 지정할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스냅숏 백업과 함께 사용할 경우, MOVE 옵션을 사용해서만 파일을 원본 blob와 동일한 저장소 계정 내에서 Azure blob으로 이동할 수 있습니다. MOVE 옵션을 사용하여 스냅숏 백업을 로컬 파일 또는 다른 저장소 계정으로 복원할 수 없습니다.  
  
 동일한 서버에서 데이터베이스 위치를 다시 지정하거나 다른 서버에 데이터베이스를 복사하려는 경우 RESTORE VERIFYONLY 문을 사용하면 대상에 충분한 공간이 있는지 확인하고 기존 파일과의 충돌 가능성을 식별하는 데 MOVE 옵션이 필요할 수 있습니다.  
  
 자세한 내용은 [백업 및 복원으로 데이터베이스 복사](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)를 참조하세요.  
  
CREDENTIAL  
 **지원 요소:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md) 및 [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 ~ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Microsoft Azure Blob Storage 서비스에서 백업을 복원할 때에만 사용됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 until[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]을 사용하는 경우, URL에서 복원할 때 단일 디바이스에서만 복원할 수 있습니다. URL에서 복원할 때 여러 디바이스에서 복원하려면 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서 [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)까지 사용해야 하며 SAS(공유 액세스 서명) 토큰을 사용해야 합니다. 자세한 내용은 [SQL Server Managed Backup을 Microsoft Azure에 사용](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md) 및 [Powershell 포함 Azure Storage에서 SAS(공유 액세스 서명)로 SQL 자격 증명 단순화](https://blogs.msdn.com/b/sqlcat/archive/2015/03/21/simplifying-creation-sql-credentials-with-shared-access-signature-sas-keys-on-azure-storage-containers-with-powershell.aspx)를 참조하세요.  
  
 REPLACE  
 **지원 요소:**  [복원](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 같은 이름을 가진 다른 데이터베이스가 이미 있을 경우에도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지정한 데이터베이스 및 관련 파일을 만들도록 지정합니다. 그런 경우에는 기존 데이터베이스가 삭제됩니다. REPLACE 옵션을 지정하지 않으면 실수로 다른 데이터베이스를 덮어쓰지 않도록 방지하는 안정성 검사가 수행됩니다. 안정성 검사를 수행하면 다음과 같은 경우 RESTORE DATABASE 문이 데이터베이스를 현재 서버로 복원하지 않습니다.  
  
-   RESTORE 문에서 지정한 데이터베이스가 현재 서버에 이미 있을 경우  
  
-   데이터베이스 이름이 백업 세트에 기록된 데이터베이스 이름과 다를 경우  
  
 또한 REPLACE 옵션을 지정하면 RESTORE에서 복원할 데이터베이스에 속하는지 확인할 수 없는 기존 파일을 덮어쓸 수 있습니다. 대개 RESTORE는 기존 파일 덮어쓰기를 거부합니다. WITH REPLACE는 RESTORE LOG 옵션에도 같은 방법으로 사용할 수 있습니다.  
  
 또한 REPLACE는 데이터베이스를 복원하기 전에 비상 로그를 백업하라는 요구 사항보다 우선 적용됩니다.  
  
 REPLACE 옵션 사용에 대한 자세한 내용은 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)을 참조하세요.  
  
RESTART  
 **지원 요소:**  [복원](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 중단된 복원 작업을 다시 시작하도록 지정합니다. RESTART는 복원 작업이 중단된 시점에서 복원 작업을 다시 시작합니다.  
  
RESTRICTED_USER  
 **지원 요소:**  [복원](../../t-sql/statements/restore-statements-transact-sql.md).  
  
 새로 복원된 데이터베이스에 대한 액세스를 **db_owner**, **dbcreator** 또는 **sysadmin** 역할의 멤버로 제한합니다.  RESTRICTED_USER는 DBO_ONLY 옵션 대신 사용됩니다. DBO_ONLY는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에서 더 이상 사용되지 않습니다.  
  
 RECOVERY 옵션과 함께 사용하십시오.  
  
##### <a name="backup-set-options"></a>백업 세트 옵션  
 이러한 옵션은 복원할 백업이 포함된 백업 세트에서 작동합니다.  
  
FILE **=**{ *backup_set_file_number* | **@**_backup\_set\_file\_number_ }  
 **지원 요소:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) 및 [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 복원할 백업 세트를 나타냅니다. 예를 들어 *backup_set_file_number* 가 **1** 인 경우는 백업 미디어의 첫 번째 백업 세트를 나타내고 *backup_set_file_number* 가 **2** 인 경우는 두 번째 백업 세트를 나타냅니다. 백업 세트의 *backup_set_file_number* 는 [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) 문을 사용하여 가져올 수 없습니다.  
  
 지정하지 않으면 기본값은 **1**입니다. 단, 미디어 세트의 모든 백업 세트가 처리되는 RESTORE HEADERONLY의 경우는 제외됩니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "백업 세트 지정"을 참조하십시오.  
  
> [!IMPORTANT]  
>  이 FILE 옵션은 데이터베이스 파일을 지정하기 위한 FILE 옵션과 관련이 없습니다. FILE **=** { *logical_file_name_in_backup* | **@**_logical\_file\_name\_in\_backup\_var_ }.  
  
 PASSWORD  **=** { *password* | **@**_password\_variable_ }  
 **지원 요소:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) 및 [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 백업 세트에 대한 암호를 제공합니다. 백업 세트 암호는 문자열입니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 백업 세트를 만들 때 암호를 지정한 경우 백업 세트에서 복원 작업을 수행하려면 암호를 입력해야 합니다. 잘못된 암호를 지정하거나 백업 세트에 암호가 없는 경우에 암호를 지정하면 오류가 발생합니다.  
  
> [!IMPORTANT]  
>  이 암호는 미디어 세트에 대한 보호 수준이 낮습니다. 자세한 내용은 관련 문에 대한 사용 권한 섹션을 참조하십시오.  
  
##### <a name="media-set-options"></a>미디어 세트 옵션  
 이러한 옵션은 전체 미디어 세트에서 작동합니다.  
  
 MEDIANAME **=** { *media_name* | **@**_media\_name\_variable_}  
 **지원 요소:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md) 및 [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 미디어에 대한 이름을 지정합니다. 제공된 미디어 이름은 백업 볼륨의 미디어 이름과 일치해야 합니다. 그렇지 않으면 복원 작업이 종료됩니다. RESTORE 문에서 미디어 이름을 지정하지 않을 경우에는 백업 볼륨의 미디어 이름과 일치하는지 확인하지 않습니다.  
  
> [!IMPORTANT]  
>  백업과 복원 작업에서 미디어 이름을 항상 사용하면 복원 작업을 위해 선택한 미디어에 대한 추가 안정성 검사를 제공합니다.  
  
 MEDIAPASSWORD **=** { *mediapassword* | **@**_mediapassword\_variable_ }  
 **지원 요소:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md) 및 [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 미디어 세트에 대한 암호를 제공합니다. 미디어 세트 암호는 문자열입니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 미디어 세트를 포맷할 때 암호를 제공한 경우 미디어 세트의 백업 세트에 액세스하려면 해당 암호를 입력해야 합니다. 잘못된 암호를 지정하거나 미디어 세트에 암호가 없는 경우에 암호를 지정하면 오류가 발생합니다.  
  
> [!IMPORTANT]  
>  이 암호는 미디어 세트에 대한 보호 수준이 낮습니다. 자세한 내용은 관련 문에 대한 "사용 권한" 섹션을 참조하십시오.  
  
 BLOCKSIZE **=** { *blocksize* | **@**_blocksize\_variable_ }  
 **지원 요소:**  [복원](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 물리적 블록 크기(바이트)를 지정합니다. 지원되는 크기는 512, 1024, 2048, 4096, 8192, 16384, 32768 및 65536(64KB) 바이트입니다. 테이프 장치의 기본값은 65536이고 그렇지 않은 경우에는 512입니다. 일반적으로 RESTORE에서 장치에 적합한 블록 크기를 자동으로 선택하기 때문에 이 옵션은 필요하지 않습니다. 명시적으로 지정된 블록 크기는 자동 선택된 블록 크기보다 우선 적용됩니다.  
  
 CD-ROM에서 백업을 복원하는 경우 BLOCKSIZE=2048을 지정합니다.  
  
> [!NOTE]  
>  이 옵션은 일반적으로 테이프 장치에서 읽는 경우에만 성능에 영향을 줍니다.  
  
##### <a name="data-transfer-options"></a>데이터 전송 옵션  
 이 옵션을 사용하면 백업 장치로부터의 데이터 전송을 최적화할 수 있습니다.  
  
 BUFFERCOUNT **=** { *buffercount* | **@**_buffercount\_variable_ }  
 **지원 요소:**  [복원](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 복원 작업에 사용되는 I/O 버퍼의 총 수를 지정합니다. 임의의 양의 정수를 지정할 수 있지만 버퍼 수가 많으면 Sqlservr.exe 프로세스의 부적절한 가상 주소 공간으로 인해 "메모리가 부족합니다"라는 오류가 발생할 수 있습니다.  
  
 버퍼에 사용되는 총 공간은 다음 식으로 결정됩니다. _buffercount_**\**_maxtransfersize_.  
  
 MAXTRANSFERSIZE **=** { _maxtransfersize_ | **@**_maxtransfersize\_variable_ }  
 **지원 요소:**  [복원](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 백업 미디어와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 간에 사용되는 가장 큰 전송 단위(바이트)를 지정합니다. 가능한 값은 최대 4194304바이트(4MB)까지 65536바이트(64KB)의 배수입니다.  
> [!NOTE]  
>  데이터베이스가 FILESTREAM을 구성했거나 메모리 내 OLTP 파일 그룹을 포함하는 경우, 복원 시 `MAXTRANSFERSIZE`는 백업이 생성될 때 사용한 것과 같거나 더 커야 합니다.  
  
##### <a name="error-management-options"></a>오류 관리 옵션  
 이러한 옵션을 사용하면 복원 작업에 대해 백업 체크섬을 설정할 수 있는지 여부와 오류 발생 시 해당 작업을 중지할지 여부를 결정할 수 있습니다.    
  
 { CHECKSUM | NO_CHECKSUM }  
 **지원 요소:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md) 및 [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 기본 동작은 체크섬이 있는 경우 체크섬을 확인하고 없는 경우에는 확인하지 않고 계속 진행하는 것입니다.  
  
 CHECKSUM  
 백업 체크섬을 확인하도록 지정합니다. 백업에 백업 체크섬이 없는 경우에는 복원 작업이 실패하고 체크섬이 없다는 메시지가 표시되도록 합니다.  
  
> [!NOTE]  
>  페이지 체크섬은 백업 체크섬이 사용될 때만 백업 작업에 사용됩니다.  
  
 기본적으로 잘못된 체크섬을 발견하면 RESTORE는 체크섬 오류를 보고하고 중지됩니다. 그러나 CONTINUE_AFTER_ERROR를 지정하는 경우 RESTORE는 체크섬 오류와 잘못된 체크섬을 포함하는 페이지 수를 반환한 후 손상이 허용될 경우 계속 진행합니다.  
  
 백업 체크섬 작업에 대한 자세한 내용은 [백업 및 복원 중 발생 가능한 미디어 오류 &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)를 참조하세요.  
  
 NO_CHECKSUM  
 복원 작업에서 체크섬 유효성 검사를 명시적으로 비활성화합니다.  
  
 { **STOP_ON_ERROR** | CONTINUE_AFTER_ERROR }  
 **지원 요소:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md) 및 [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 STOP_ON_ERROR  
 첫 번째 오류가 발생하면 복원 작업이 중지하도록 지정합니다. 기본값으로 CONTINUE_AFTER_ERROR를 사용하는 VERIFYONLY를 제외하면 RESTORE의 기본 동작입니다.  
  
 CONTINUE_AFTER_ERROR  
 오류가 발생한 후에도 복원 작업을 계속하도록 지정합니다.  
  
 백업에 손상된 페이지가 있는 경우 오류가 없는 다른 백업(예: 페이지가 손상되기 전에 수행된 백업)을 사용하여 복원 작업을 반복하는 것이 가장 좋습니다. 하지만 최후의 수단으로 복원 문의 CONTINUE_AFTER_ERROR 옵션을 사용하여 손상된 백업을 복원하여 데이터를 복원할 수도 있습니다.  
  
##### <a name="filestream-options"></a>FILESTREAM Options  
 FILESTREAM ( DIRECTORY_NAME =*directory_name* )  
 **지원 요소:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 및 [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지
  
 Windows 호환 디렉터리 이름입니다. 이 이름은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 데이터베이스 수준 FILESTREAM 디렉터리 이름 중에서 고유해야 합니다. 고유성 비교는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬 설정에 관계없이 대/소문자를 구분하지 않고 수행됩니다.  
  
##### <a name="monitoring-options"></a>모니터링 옵션  
 이러한 옵션을 사용하면 백업 장치로부터의 데이터 전송을 모니터링할 수 있습니다.  
  
 STATS [ **=** *percentage* ]  
 **지원 요소:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 및 [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
 새로 백분율이 완료될 때마다 메시지를 표시하여 진행 상태를 측정하는 데 사용됩니다. *percentage*를 생략하면 대략 10%가 완료될 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 메시지를 표시합니다.  
  
 STATS 옵션은 다음 간격을 보고할 임계값에 도달한 시점까지의 완료 백분율을 보고합니다. 간격은 대략적으로 지정된 비율을 나타냅니다. 예를 들어 STATS=10이면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 대략적으로 지정된 간격에 따라 보고합니다. 예를 들어 정확하게 40%를 표시하는 대신 43%를 표시할 수 있습니다. 대용량 백업 세트의 경우 완료 백분율이 완료된 I/O 호출 간에 매우 느리게 진행되므로 문제가 되지 않습니다.  
  
##### <a name="tape-options"></a>테이프 옵션  
 이러한 옵션은 테이프 장치에만 사용됩니다. 테이프가 아닌 장치를 사용할 경우 이러한 옵션은 무시됩니다.  
  
 { **REWIND** | NOREWIND }  
 이러한 옵션은 테이프 장치에만 사용됩니다. 테이프가 아닌 장치를 사용하는 경우 이 옵션은 무시됩니다.  
  
 REWIND  
 **지원 요소:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md) 및 [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 테이프를 해제한 다음 되감도록 지정합니다. 기본값은 REWIND입니다.  
  
 NOREWIND  
 **지원 요소:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 및 [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
 다른 모든 복원 문에서 NOREWIND를 지정하면 오류가 발생합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 백업 작업 후에 테이프를 열어 놓도록 지정합니다. 테이프에 여러 개의 백업 작업을 수행할 때 이 옵션을 사용하면 성능을 향상시킬 수 있습니다.  
  
 NOREWIND는 NOUNLOAD를 의미하며 두 옵션은 단일 RESTORE 문 내에서 호환되지 않습니다.  
  
> [!NOTE]  
>  NOREWIND를 사용하는 경우 같은 프로세스에서 실행 중인 BACKUP 또는 RESTORE 문이 REWIND 또는 UNLOAD 옵션을 사용하거나 서버 인스턴스가 종료될 때까지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 테이프 드라이브에 대한 소유권을 보유합니다. 테이프를 열어 두면 다른 프로세스에서 테이프를 액세스하는 것을 방지합니다. 열린 테이프 목록을 표시하고 열린 테이프를 닫는 방법은 [백업 디바이스&amp;#40;SQL Server&amp;#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)를 참조하세요.  
  
 { **UNLOAD** | NOUNLOAD }  
 **지원 요소:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md), [RESTORE REWINDONLY](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md) 및 [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 이러한 옵션은 테이프 장치에만 사용됩니다. 테이프가 아닌 장치를 사용하는 경우 이 옵션은 무시됩니다.  
  
> [!NOTE]  
>  UNLOAD/NOUNLOAD는 세션 기간 동안이나 다른 옵션을 지정하여 다시 설정할 때까지 유지되는 세션 설정입니다.  
  
 UNLOAD  
 백업이 끝나면 테이프를 자동으로 되감고 언로드되도록 지정합니다. UNLOAD는 세션 시작 시의 기본값입니다.  
  
 NOUNLOAD  
 RESTORE 작업 후에 테이프가 테이프 드라이브에 로드된 상태로 남아 있도록 지정합니다.  
  
#### <a name="replicationwithoption"></a><replication_WITH_option>  
 이 옵션은 백업을 만들 때 데이터베이스가 복제된 경우에만 해당합니다.  
  
 KEEP_REPLICATION  
 **지원 요소:**  [복원](../../t-sql/statements/restore-statements-transact-sql.md)  
  
로그 전달에서 작업할 복제를 설정할 때 KEEP_REPLICATION을 사용합니다. 그러면 대기 중인 서버에서 데이터베이스 백업이나 로그 백업이 복원되고 데이터베이스가 복구될 때 복제 설정이 제거되지 않도록 할 수 있습니다. NORECOVERY 옵션을 사용하여 백업을 복원하는 동안 이 옵션을 지정할 수 없습니다. 복원 후 복제가 제대로 실행되도록 하려면 다음을 수행하십시오.  
  
-   웜 대기 서버의 **msdb** 및 **master** 데이터베이스가 주 서버의 **msdb** 및 **master** 데이터베이스와 동기화되어야 합니다.  
  
-   대기 중인 서버의 이름을 주 서버와 동일하게 변경해야 합니다.  
  
#### <a name="changedatacapturewithoption"></a><change_data_capture_WITH_option>  
 이 옵션은 백업을 만들 때 데이터베이스에 변경 데이터 캡처를 사용하도록 설정된 경우에만 해당합니다.  
  
 KEEP_CDC  
 **지원 요소:**  [복원](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 데이터베이스 백업 또는 로그 백업을 다른 서버에서 복원하여 데이터베이스를 복구하는 경우 변경 데이터 캡처 설정이 제거되지 않도록 KEEP_CDC를 사용해야 합니다. NORECOVERY 옵션을 사용하여 백업을 복원하는 동안 이 옵션을 지정할 수 없습니다.  
  
 KEEP_CDC로 데이터베이스를 복원하면 변경 데이터 캡처 작업이 생성되지 않습니다. 데이터베이스 복원 후 로그에서 변경 내용을 추출하려면 복원된 데이터베이스에 대한 캡처 프로세스 작업 및 정리 작업을 다시 만드십시오. 자세한 내용은 [sys.sp_cdc_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)을 참조하세요.  
  
 데이터베이스 미러링에 변경 데이터 캡처를 사용하는 방법은 [변경 데이터 캡처 및 기타 SQL Server 기능](../../relational-databases/track-changes/change-data-capture-and-other-sql-server-features.md)을 참조하세요.  
  
#### <a name="servicebrokerwithoptions"></a>\<service_broker_WITH_options>  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 메시지 배달을 사용 또는 사용하지 않도록 설정하거나 새 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 식별자를 설정합니다. 이 옵션은 백업을 만들 때 데이터베이스에 대해 [!INCLUDE[ssSB](../../includes/sssb-md.md)]를 사용하도록 설정(활성화)한 경우에만 적용됩니다.  
  
 { ENABLE_BROKER  | ERROR_BROKER_CONVERSATIONS  | NEW_BROKER }  
 **지원 요소:**  [데이터베이스 복원](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 ENABLE_BROKER  
 복원 작업이 완료된 후 즉시 메시지를 보낼 수 있도록 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 메시지 배달을 지정합니다. 기본적으로 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 메시지 배달은 복원 작업 동안 해제됩니다. 데이터베이스에는 기존 Service Broker 식별자가 유지됩니다.  
  
 ERROR_BROKER_CONVERSATIONS  
 데이터베이스가 연결 또는 복원되었다는 오류 메시지를 표시하고 모든 대화를 끝냅니다. 이렇게 하면 응용 프로그램에서 기존 대화에 대해 일반적인 정리 작업을 수행할 수 있습니다. Service Broker 메시지 배달은 이 작업이 수행되는 동안 해제되어 있다가 이 작업이 완료된 후 설정됩니다. 데이터베이스에는 기존 Service Broker 식별자가 유지됩니다.  
  
 NEW_BROKER  
 데이터베이스에 새 Service Broker 식별자가 할당되도록 지정합니다. 데이터베이스는 새 Service Broker가 될 것으로 간주되기 때문에 데이터베이스 내의 기존 대화는 종료 대화 메시지 없이 즉시 제거됩니다. 이전 Service Broker 식별자를 참조하는 경로는 새 식별자로 다시 만들어야 합니다.  
  
#### <a name="pointintimewithoptions"></a>\<point_in_time_WITH_options>  
 **지원 요소:**  [RESTORE {DATABASE|LOG}](../../t-sql/statements/restore-statements-transact-sql.md) 및 전체 또는 대량 로그된 복구 모델에 한함.  
  
 STOPAT, STOPATMARK 또는 STOPBEFOREMARK 절에 대상 복구 지점을 지정 데이터베이스를 특정 지정 시간 또는 트랜잭션으로 복원할 수 있습니다. 지정된 시간 또는 트랜잭션은 항상 로그 백업에서 복원됩니다. 복원 순서의 모든 RESTORE LOG 문에서 동일한 STOPAT, STOPATMARK 또는 STOPBEFOREMARK 절에 대상 시간이나 트랜잭션을 지정해야 합니다.  
  
 지정 시간 복원을 수행하려면 먼저 종료 지점이 대상 복원 시간보다 빠른 전체 데이터베이스 백업을 복원해야 합니다. 복원할 데이터베이스를 손쉽게 확인하려면 선택적으로 RESTORE DATABASE 문에 WITH STOPAT, STOPATMARK 또는 STOPBEFOREMARK 절을 지정하여 데이터 백업이 지정된 대상 시간에 비해 너무 최근인 경우 오류가 발생하도록 하면 됩니다. 그러나 데이터 백업에 대상 시간이 포함된 경우에도 항상 전체 데이터 백업이 복원됩니다.  
  
> [!NOTE]  
>  RESTORE_DATABASE 및 RESTORE_LOG 지정 시간 WITH 옵션은 서로 비슷하지만 RESTORE LOG만 *mark_name* 인수를 지원합니다.  
  
 { STOPAT | STOPATMARK | STOPBEFOREMARK }   
 
 STOPAT **=** { **'**_datetime_**'** | **@**_datetime\_var* }  
 데이터베이스가 *datetime* 또는 **@**_datetime\_var_ 매개 변수에 지정된 날짜 및 시간의 상태로 복원되도록 지정합니다. 날짜 및 시간 지정에 대한 자세한 내용은 [날짜 및 시간 데이터 형식 및 함수 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)을 참조하세요.  
  
 STOPAT에 사용되는 변수는 **varchar**, **char**, **smalldatetime** 또는 **datetime** 데이터 형식으로 지정해야 합니다. 지정한 날짜와 시간 전에 작성된 트랜잭션 로그 레코드만 데이터베이스에 적용됩니다.  
  
> [!NOTE]  
>  지정한 STOPAT 시간이 마지막 LOG 백업 이후의 시간이면 데이터베이스는 RESTORE LOG가 NORECOVERY로 실행된 것처럼 복구되지 않은 상태가 됩니다.  
  
 자세한 내용은 [SQL Server 데이터베이스를 지정 시간으로 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)을 참조하세요.  
  
 STOPATMARK **=** { **'**_mark\_name_**'** | **'** lsn:_lsn\_number_**'** } [ AFTER **'**_datetime_**'** ]  
 지정된 복구 지점으로의 복구를 지정합니다. 지정된 트랜잭션은 복구에 포함되지만 트랜잭션이 실제로 생성될 때 원래 커밋된 경우에만 커밋됩니다.  
  
 RESTORE DATABASE 및 RESTORE LOG는 모두 *lsn_number* 매개 변수를 지원합니다. 이 매개 변수는 로그 시퀀스 번호를 지정합니다.  
  
 *mark_name* 매개 변수는 RESTORE LOG 문에서만 지원됩니다. 이 매개 변수는 로그 백업에서 트랜잭션 표시를 식별합니다.  
  
 RESTORE LOG 문에서 AFTER *datetime*을 생략하면 지정한 이름이 있는 첫 번째 표시 지점에서 복구가 중지됩니다. AFTER *datetime*을 지정하면 정확히 *datetime*에 또는 그 후에 지정한 이름이 있는 첫 번째 표시 지점에서 복구가 중지됩니다.  
  
> [!NOTE]  
>  지정한 표시, LSN 또는 시간이 마지막 LOG 백업 이후의 시간이면 데이터베이스는 RESTORE LOG가 NORECOVERY로 실행된 것처럼 복구되지 않은 상태가 됩니다.  
  
 자세한 내용은 [표시된 트랜잭션을 사용하여 관련 데이터베이스를 일관되게 복구 &#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md) 및 [로그 시퀀스 번호로 복구 &#40;SQL Server&#41;](../../relational-databases/backup-restore/recover-to-a-log-sequence-number-sql-server.md)를 참조하세요.  
  
 STOPBEFOREMARK **=** { **'**_mark\_name_**'** | **'** lsn:_lsn\_number_**'** } [ AFTER **'**_datetime_**'** ]  
 지정된 복구 지점까지의 복구를 지정합니다. 지정된 트랜잭션은 복구에 포함되지 않으며 WITH RECOVERY가 사용될 때 롤백됩니다.  
  
 RESTORE DATABASE 및 RESTORE LOG는 모두 *lsn_number* 매개 변수를 지원합니다. 이 매개 변수는 로그 시퀀스 번호를 지정합니다.  
  
 *mark_name* 매개 변수는 RESTORE LOG 문에서만 지원됩니다. 이 매개 변수는 로그 백업에서 트랜잭션 표시를 식별합니다.  
  
 RESTORE LOG 문에서 AFTER *datetime*을 생략하면 지정한 이름이 있는 첫 번째 표시 지점 바로 앞에서 복구가 중지됩니다. AFTER *datetime*을 지정하면 정확히 *datetime*에 또는 그 후에 지정한 이름이 있는 첫 번째 표시 지점 바로 앞에서 복구가 중지됩니다.  
  
> [!IMPORTANT]  
>  부분 복원 순서에서 FILESTREAM 파일 그룹이 제외될 경우 지정 시간 복원은 지원되지 않습니다. 복원 순서를 강제로 계속할 수 있지만 RESTORE 문에서 누락된 FILESTREAM 파일 그룹은 복원되지 않습니다. 지정 시간 복원을 강제로 수행하려면 STOPAT, STOPATMARK 또는 STOPBEFOREMARK 옵션과 함께 CONTINUE_AFTER_ERROR 옵션을 지정해야 합니다. CONTINUE_AFTER_ERROR를 지정하면 부분 복원 순서가 성공하고 FILESTREAM 파일 그룹이 복구 불가능한 상태가 됩니다.  
  
## <a name="result-sets"></a>결과 집합  
 결과 집합에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [RESTORE FILELISTONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
-   [RESTORE HEADERONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE LABELONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)  
  
## <a name="remarks"></a>Remarks  
 추가적인 주의 사항은 다음 항목을 참조하십시오.  
  
-   [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [RESTORE HEADERONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE LABELONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)  
  
-   [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)  
  
-   [RESTORE VERIFYONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
## <a name="specifying-a-backup-set"></a>백업 세트 지정  
 *백업 세트*에는 하나의 성공한 백업 작업의 백업이 포함됩니다. RESTORE, RESTORE FILELISTONLY, RESTORE HEADERONLY 및 RESTORE VERIFYONLY 문은 지정한 백업 장치의 미디어 세트 내에 있는 단일 백업 세트에서 작동합니다. 미디어 세트 내에서 필요한 백업을 지정해야 합니다. 백업 세트의 *backup_set_file_number* 는 [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) 문을 사용하여 가져올 수 없습니다.  
  
 복원할 백업 세트를 지정하는 옵션은 다음과 같습니다.  
  
 FILE **=**{ *backup_set_file_number* | **@**_backup\_set\_file\_number_ }  
  
 여기서 *backup_set_file_number*는 미디어 세트에서의 백업 위치를 나타냅니다. *backup_set_file_number*가 1(FILE = 1)인 경우는 백업 미디어의 첫 번째 백업 세트를 나타내며 *backup_set_file_number*가 2(FILE = 2)인 경우는 두 번째 백업 세트를 나타내는 식입니다.  
  
 다음 표에서 설명하는 것처럼 이 옵션의 동작은 문에 따라 달라집니다.  
  
|인수를 제거합니다.|백업 세트 FILE 옵션의 동작|  
|---------------|-----------------------------------------|  
|RESTORE|기본 백업 세트 파일 번호는 1입니다. RESTORE 문에서는 하나의 백업 세트 FILE 옵션만 사용할 수 있습니다. 순서대로 백업 세트를 지정하는 것이 중요합니다.|  
|RESTORE FILELISTONLY|기본 백업 세트 파일 번호는 1입니다.|  
|RESTORE HEADERONLY|기본적으로 미디어 세트에 있는 모든 백업 세트가 처리됩니다. RESTORE HEADERONLY 결과 집합은 미디어 세트에서의 해당 **위치**를 포함하여 각 백업 세트에 대한 정보를 반환합니다. 지정된 백업 세트에 대한 정보를 반환하려면 해당 위치 번호를 FILE 옵션의 *backup_set_file_number* 값으로 사용합니다.<br /><br /> 참고: 테이프 미디어의 경우 RESTORE HEADER는 로드된 테이프에 있는 백업 세트만 처리합니다.|  
|RESTORE VERIFYONLY|기본 *backup_set_file_number*는 1입니다.|  
  
> [!NOTE]  
>  백업 세트를 지정하기 위한 FILE 옵션은 데이터베이스 파일을 지정하기 위한 FILE 옵션과 관련이 없습니다. FILE **=** { *logical_file_name_in_backup* | **@**_logical\_file\_name\_in\_backup\_var_ }.  
  
## <a name="summary-of-support-for-with-options"></a>WITH 옵션 지원에 대한 요약  
 BLOCKSIZE, BUFFERCOUNT, MAXTRANSFERSIZE, BLOCKSIZE, BUFFERCOUNT, MAXTRANSFERSIZE, PARTIAL, KEEP_REPLICATION, { RECOVERY | NORECOVERY | STANDBY }, REPLACE, RESTART, RESTRICTED_USER 및 { STOPAT | STOPATMARK | STOPBEFOREMARK }  
  
> [!NOTE]  
>  PARTIAL 옵션은 RESTORE DATABASE에서만 지원합니다.  
  
 다음 표에서는 하나 이상의 문에서 사용되는 WITH 옵션 목록과 각 옵션을 지원하는 문을 보여 줍니다. 확인 표시(√)는 지원되는 옵션이며, 대시(-)는 지원되지 않는 옵션입니다.  
  
|WITH 옵션|RESTORE|RESTORE FILELISTONLY|RESTORE HEADERONLY|RESTORE LABELONLY|RESTORE REWINDONLY|RESTORE VERIFYONLY|  
|-----------------|-------------|--------------------------|------------------------|-----------------------|------------------------|------------------------|  
|{ CHECKSUM<br /><br /> &#124; NO_CHECKSUM }|√|√|√|√|-|√|  
|{ CONTINUE_AFTER_ERROR<br /><br /> &#124; STOP_ON_ERROR }|√|√|√|√|-|√|  
|FILE<sup>1</sup>|√|√|√|-|-|√|  
|LOADHISTORY|-|-|-|-|-|√|  
|MEDIANAME|√|√|√|√|-|√|  
|MEDIAPASSWORD|√|√|√|√|-|√|  
|MOVE|√|-|-|-|-|√|  
|PASSWORD|√|√|√|-|-|√|  
|{ REWIND &#124; NOREWIND }|√|REWIND 전용|REWIND 전용|REWIND 전용|-|√|  
|STATS|√|-|-|-|-|√|  
|{ UNLOAD &#124; NOUNLOAD }|√|√|√|√|√|√|  
  
 <sup>1</sup> FILE **=**_backup\_set\_file\_number_. 이는 {FILE | FILEGROUP}과 다릅니다.  
  
## <a name="permissions"></a>Permissions  
 사용 권한에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [RESTORE FILELISTONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
-   [RESTORE HEADERONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE LABELONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)  
  
-   [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)  
  
-   [RESTORE VERIFYONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
## <a name="examples"></a>예  
 예를 보려면 다음 항목을 참조하십시오.  
  
-   [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [RESTORE FILELISTONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
-   [RESTORE HEADERONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
## <a name="see-also"></a>참고 항목  
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE FILELISTONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)   
 [RESTORE HEADERONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [RESTORE LABELONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)   
 [RESTORE REWINDONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE VERIFYONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [SQL Server 데이터베이스 백업 및 복원](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [FILESTREAM&#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)  
  
  

