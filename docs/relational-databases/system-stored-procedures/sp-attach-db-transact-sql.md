---
title: sp_attach_db (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_attach_db_TSQL
- sp_attach_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_attach_db
ms.assetid: 59bc993e-7913-4091-89cb-d2871cffda95
caps.latest.revision: 69
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 460d9eab90fb65f4d271829d76d72dfa26f0b1b0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="spattachdb-transact-sql"></a>sp_attach_db(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  서버에 데이터베이스를 연결합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] CREATE DATABASE를 사용 하는 것이 좋습니다 *database_name* FOR ATTACH 대신. 자세한 내용은 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)를 참조하세요.  
  
> [!NOTE]  
>  하나 이상의 새 위치가 있는 경우 여러 로그 파일이 다시 작성 하려면 CREATE DATABASE를 사용 하 여 *database_name* FOR ATTACH_REBUILD_LOG 합니다.  
  
> [!IMPORTANT]  
>  알 수 없거나 신뢰할 수 없는 출처의 데이터베이스는 연결 또는 복원하지 않는 것이 좋습니다. 이러한 데이터베이스에 포함된 악성 코드가 의도하지 않은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드를 실행하거나 스키마 또는 물리적 데이터베이스 구조를 수정하여 오류가 발생할 수 있습니다. 알 수 없거나 신뢰할 수 없는 소스의 데이터베이스를 사용하기 전에 비프로덕션 서버의 데이터베이스에서 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 를 실행하여 데이터베이스에서 코드(예: 저장 프로시저 또는 다른 사용자 정의 코드)를 시험해 보세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_attach_db [ @dbname= ] 'dbname'  
    , [ @filename1= ] 'filename_n' [ ,...16 ]   
```  
  
## <a name="arguments"></a>인수  
 [ **@dbname=** ] **'***dbnam* **'**  
 서버에 연결될 데이터베이스의 이름입니다. 이름은 고유해야 합니다. *dbname* 은 **sysname**, 기본값은 NULL입니다.  
  
 [ **@filename1=** ] **'***filename_n***'**  
 경로를 포함한 데이터베이스 파일의 물리적 이름입니다. *filename_n* 은 **nvarchar (260)**, 기본값은 NULL입니다. 파일 이름은 16개까지 지정할 수 있습니다. 시작 하는 매개 변수 이름이 **@filename1** 으로 증가 하 고 **@filename16**합니다. 파일 이름 목록에는 적어도 주 파일이 포함되어야 합니다. 주 파일에는 데이터베이스의 다른 파일을 가리키는 시스템 테이블이 포함됩니다. 또한 목록은 데이터베이스가 분리된 다음 이동된 모든 파일을 포함해야 합니다.  
  
> [!NOTE]  
>  이 인수는 CREATE DATABASE 문의 FILENAME 매개 변수에 매핑됩니다. 자세한 내용은 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)를 참조하세요.  
>   
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 서버 인스턴스에 전체 텍스트 카탈로그 파일이 포함된 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 데이터베이스를 연결할 경우 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서와 같이 다른 데이터베이스 파일과 함께 이전 위치에서 카탈로그 파일이 연결됩니다. 자세한 내용은 [전체 텍스트 검색 업그레이드](../../relational-databases/search/upgrade-full-text-search.md)를 참조하세요.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>주의  
 **sp_attach_db** 이전에 명시적를 사용 하 여 데이터베이스 서버에서 분리 된 데이터베이스에서에 저장된 프로시저를 실행 해야 **sp_detach_db** 작업 데이터베이스나 복사 합니다. CREATE DATABASE를 사용 하 여 16 개 이상의 파일을 지정 해야 할 경우 *a s e _* FOR ATTACH 또는 CREATE DATABASE *database_name* FOR_ATTACH_REBUILD_LOG 합니다. 자세한 내용은 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)를 참조하세요.  
  
 지정되지 않은 모든 파일은 마지막으로 알려진 위치에 있는 것으로 가정합니다. 다른 위치에서 파일을 사용하려면 새 위치를 지정해야 합니다.  
  
 최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 만든 데이터베이스를 이전 버전에서 연결할 수 없습니다.  
  
> [!NOTE]  
>  데이터베이스 스냅숏은 분리하거나 연결할 수 없습니다.  
  
 분리되지 않고 복사된 복제 데이터베이스를 연결하는 경우에는 다음 사항을 고려합니다.  
  
-   데이터베이스를 원래 데이터베이스와 동일한 서버 인스턴스 및 버전에 연결하는 경우에는 추가 작업이 필요하지 않습니다.  
  
-   데이터베이스를 동일한 서버 인스턴스의 업그레이드된 버전에 연결하는 경우에는 연결 작업이 완료된 다음, [sp_vupgrade_replication](../../relational-databases/system-stored-procedures/sp-vupgrade-replication-transact-sql.md)을 실행하여 복제를 업그레이드해야 합니다.  
  
-   데이터베이스를 버전에 관계없이 다른 서버 인스턴스에 연결하는 경우에는 연결 작업이 완료된 다음, [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)을 실행하여 복제를 제거해야 합니다.  
  
 데이터베이스가 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스로 처음으로 연결되거나 복원될 때 데이터베이스 마스터 키(서비스 마스터 키로 암호화됨)의 복사본은 서버에 아직 저장되지 않은 상태입니다. 데이터베이스 마스터 키를 암호 해독하려면 **OPEN MASTER KEY** 문을 사용해야 합니다. DMK를 암호 해독한 후에는 **ALTER MASTER KEY REGENERATE** 문을 사용하여 SMK(서비스 마스터 키)로 암호화된 DMK의 복사본을 서버에 프로비전함으로써 앞으로 자동 암호 해독을 사용하도록 설정할 수 있습니다. 데이터베이스가 이전 버전에서 업그레이드되지 않은 경우에는 DMK를 다시 생성해야 최신 AES 알고리즘을 사용할 수 있습니다. DMK를 다시 생성하는 방법은 [ALTER MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)를 참조하세요. AES로 업그레이드하기 위해 DMK 키를 다시 생성하는 데 소요되는 시간은 DMK에서 보호하는 개체 수에 따라 달라집니다. AES로 업그레이드하기 위해 DMK 키를 다시 생성하는 작업은 한 번만 필요하며 키 회전 전략의 일부로 이후에 수행하는 다시 생성 작업에 영향을 주지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 데이터베이스가 연결 될 때 사용 권한을 처리 되는 방법에 대 한 정보를 참조 하십시오. [CREATE DATABASE &#40;SQL Server TRANSACT-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]의 파일을 현재 서버에 연결합니다.  
  
```  
EXEC sp_attach_db @dbname = N'AdventureWorks2012',   
    @filename1 =   
N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_Data.mdf',   
    @filename2 =   
N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_log.ldf';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [sp_detach_db&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [sp_helpfile&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [sp_removedbreplication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
