---
title: sp_detach_db (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/30/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_detach_db
- sp_detach_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_detach_db
- detaching databases [SQL Server]
ms.assetid: abcb1407-ff78-4c76-b02e-509c86574462
author: stevestein
ms.author: sstein
ms.openlocfilehash: eec8b91bbb7d90483b627aebddb7088bc80cb1ea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912891"
---
# <a name="spdetachdb-transact-sql"></a>sp_detach_db(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  서버 인스턴스에서 현재 사용하지 않는 데이터베이스를 분리하고, 필요한 경우 분리하기 전에 모든 테이블에서 UPDATE STATISTICS를 실행합니다.  
  
> [!IMPORTANT]  
>  분리할 복제된 데이터베이스는 게시되지 않습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "주의" 섹션을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_detach_db [ @dbname= ] 'database_name'   
    [ , [ @skipchecks= ] 'skipchecks' ]   
    [ , [ @keepfulltextindexfile = ] 'KeepFulltextIndexFile' ]   
```  
  
## <a name="arguments"></a>인수  
`[ @dbname = ] 'database_name'` 분리할 데이터베이스의 이름이입니다. *database_name* 되는 **sysname** 값 이며 기본값은 NULL입니다.  
  
`[ @skipchecks = ] 'skipchecks'` 업데이트 통계 건너뛰거나 것인지 지정 합니다. *skipchecks* 되는 **nvarchar(10)** 값 이며 기본값은 NULL입니다. UPDATE STATISTICS를 건너뛰려면 지정할 **true**합니다. UPDATE STATISTICS를 명시적으로 실행 하려면 지정할 **false**합니다.  
  
 기본적으로 UPDATE STATISTICS는 테이블과 인덱스에 있는 데이터에 관한 정보를 업데이트하기 위해 수행됩니다. UPDATE STATISTICS는 읽기 전용 미디어로 이동할 데이터베이스에 수행하면 유용합니다.  
  
`[ @keepfulltextindexfile = ] 'KeepFulltextIndexFile'` 분리 되는 데이터베이스에 연결 된 전체 텍스트 인덱스 파일이 데이터베이스 중 삭제 되지 것입니다 지정 작업을 분리 합니다. *KeepFulltextIndexFile* 되는 **nvarchar(10)** 이며 기본값은 값 **true**합니다. 하는 경우 *KeepFulltextIndexFile* 됩니다 **false**, 데이터베이스와 연결 된 모든 전체 텍스트 인덱스 파일 및 전체 텍스트 인덱스의 메타 데이터 데이터베이스가 읽기 전용 아니면 삭제 됩니다. Null 인 경우 또는 **true**, 전체 텍스트 관련 메타 데이터가 유지 됩니다.  
  
> [!IMPORTANT]
>  합니다 **@keepfulltextindexfile** 매개 변수는 이후 버전의에서 제거할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 새 개발 작업에서는 이 매개 변수를 사용하지 말고 현재 이 매개 변수를 사용하는 응용 프로그램은 가능한 한 빨리 수정하십시오.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>설명  
 데이터베이스가 분리되면 모든 해당 메타데이터가 삭제됩니다. 모든 로그인 계정의 기본 데이터베이스 있었다면 **마스터** 해당 계정의 기본 데이터베이스가 됩니다.  
  
> [!NOTE]  
>  모든 로그인 계정의 기본 데이터베이스를 보는 방법에 대 한 자세한 내용은 [sp_helplogins &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md)합니다. 필요한 권한이 있는 경우 사용할 수 있습니다 [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) 로그인에 새 기본 데이터베이스를 할당 합니다.  
  
## <a name="restrictions"></a>Restrictions  
 다음 중 하나라도 해당하는 경우 데이터베이스를 분리할 수 없습니다.  
  
-   데이터베이스가 현재 사용되고 있는 경우. 자세한 내용은 이 항목의 뒷부분에 나오는 "배타적 액세스 권한 얻기"를 참조하십시오.  
  
-   데이터베이스가 복제된 경우 해당 데이터베이스가 게시됩니다.  
  
     데이터베이스를 분리 하기 전에 실행 하 여 게시를 해제 해야 합니다 [sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)합니다.  
  
    > [!NOTE]  
    >  **sp_replicationdboption**을 사용할 수 없는 경우 [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)을 실행하여 복제를 제거할 수 있습니다.  
  
-   데이터베이스에 데이터베이스 스냅숏이 있는 경우  
  
     데이터베이스를 분리하려면 먼저 해당 데이터베이스의 모든 스냅숏을 삭제해야 합니다. 자세한 내용은 [데이터베이스 스냅숏 삭제&#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)인스턴스나 다른 인스턴스에 다시 연결할 수 있습니다.  
  
    > [!NOTE]  
    >  데이터베이스 스냅숏은 분리하거나 연결할 수 없습니다.  
  
-   데이터베이스가 미러링되고 있는 경우  
  
     데이터베이스는 데이터베이스 미러링 세션이 종료된 후에야 분리할 수 있습니다. 자세한 내용은 [데이터베이스 미러링 제거&#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)를 참조하세요.  
  
-   주의 대상 데이터베이스인 경우  
  
     주의 대상 데이터베이스를 분리하기 전에 응급 모드로 설정해야 합니다. 데이터베이스를 응급 모드로 설정하는 방법은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.  
  
-   데이터베이스가 시스템 데이터베이스인 경우  
  
## <a name="obtaining-exclusive-access"></a>배타적 액세스 권한 얻기  
 데이터베이스를 분리하려면 해당 데이터베이스를 단독으로 사용해야 합니다. 분리할 데이터베이스가 사용되고 있으면 분리하기 전에 데이터베이스를 SINGLE_USER 모드로 설정하여 배타적 액세스 권한을 얻으십시오.  
  
 예를 들어, 다음 `ALTER DATABASE` 문을 가져오는 단독으로 액세스 하는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 모든 현재 사용자 데이터베이스에서 연결을 끊고 데이터베이스입니다.  
  
```  
USE master;  
ALTER DATABASE AdventureWorks2012  
SET SINGLE_USER;  
GO  
```  
  
> [!NOTE]  
>  현재 사용자가 데이터베이스를 즉시 적용 또는 지정 된 숫자로 시간 (초) 내에서 ROLLBACK 옵션을 사용할 수도 있습니다. ALTER DATABASE *database_name* SINGLE_USER WITH ROLLBACK 설정 *rollback_option*합니다. 자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.  
  
## <a name="reattaching-a-database"></a>데이터베이스 다시 연결  
 분리된 파일은 그대로 남아 있으며 FOR ATTACH 또는 FOR ATTACH_REBUILD_LOG 옵션과 함께 CREATE DATABASE를 사용하여 다시 연결할 수 있습니다. 또한 파일을 다른 서버로 이동하거나 첨부할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버 자격이 필요 합니다 **sysadmin** 고정 서버 역할의 멤버 자격을 **db_owner** 데이터베이스의 역할입니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 분리 된 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 사용 하 여 데이터베이스 *skipchecks* true로 설정 합니다.  
  
```  
EXEC sp_detach_db 'AdventureWorks2012', 'true';  
```  
  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스를 분리하고 전체 텍스트 인덱스 파일과 전체 텍스트 인덱스의 메타데이터를 유지합니다. 이 명령은 기본 동작으로 UPDATE STATISTICS를 실행합니다.  
  
```  
exec sp_detach_db @dbname='AdventureWorks2012'  
    , @keepfulltextindexfile='true';  
```  
  
## <a name="see-also"></a>관련 항목  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [데이터베이스 분리](../../relational-databases/databases/detach-a-database.md)  
  
  
