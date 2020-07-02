---
title: sys. database_recovery_status (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_recovery_status_TSQL
- database_recovery_status
- sys.database_recovery_status
- sys.database_recovery_status_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_recovery_status catalog view
ms.assetid: 46fab234-1542-49be-8edf-aa101e728acf
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e91b41815f39e27bc368a4d61ce84fc23635f160
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734833"
---
# <a name="sysdatabase_recovery_status-transact-sql"></a>sys.database_recovery_status(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  데이터베이스당 하나의 행을 포함합니다. 데이터베이스가 열려 있지 않으면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 해당 데이터베이스를 시작하려고 합니다.  
  
 **Master** 또는 **tempdb**이외의 데이터베이스에 대 한 행을 보려면 다음 중 하나를 적용 해야 합니다.  
  
-   데이터베이스 소유자입니다.  
  
-   ALTER ANY DATABASE 또는 VIEW ANY DATABASE 서버 수준 권한이 있습니다.  
  
-   **Master** 데이터베이스에서 CREATE DATABASE 권한이 있어야 합니다.    
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내에서 고유한 데이터베이스 ID입니다.|  
|**database_guid**|**uniqueidentifier**|데이터베이스의 모든 데이터베이스 파일을 함께 연결하는 데 사용됩니다. 데이터베이스를 제대로 시작하려면 모든 파일의 헤더 페이지에 이 GUID가 있어야 합니다. 현재까지는 하나의 데이터베이스에만 이 GUID가 있었습니다. 그러나 데이터베이스를 복사하고 연결하여 GUID를 중복하여 만들 수 있습니다. 아직 존재하지 않는 데이터베이스를 복원할 때 RESTORE는 항상 새 GUID를 생성합니다.<br /><br /> NULL= 데이터베이스가 오프라인이거나 데이터베이스를 시작할 수 없습니다.|  
|**family_guid**|**uniqueidentifier**|일치하는 복원 상태를 검색하는 데이터베이스 "백업 패밀리"의 식별자입니다.<br /><br /> NULL= 데이터베이스가 오프라인이거나 데이터베이스를 시작할 수 없습니다.|  
|**last_log_backup_lsn**|**numeric(25,0)**|다음 로그 백업의 시작 로그 시퀀스 번호입니다.<br /><br /> NULL 인 경우 데이터베이스가 단순 복구에 있거나 현재 데이터베이스 백업이 없기 때문에 트랜잭션 로그 백업을 수행할 수 없습니다.|  
|**recovery_fork_guid**|**uniqueidentifier**|데이터베이스가 현재 활성화되어 있는 복구 분기 지점을 식별합니다.<br /><br /> NULL= 데이터베이스가 오프라인이거나 데이터베이스를 시작할 수 없습니다.|  
|**first_recovery_fork_guid**|**uniqueidentifier**|복구 분기 시작 지점의 식별자입니다.<br /><br /> NULL= 데이터베이스가 오프라인이거나 데이터베이스를 시작할 수 없습니다.|  
|**fork_point_lsn**|**numeric(25,0)**|**First_recovery_fork_guid** (! =)이 같지 않은 경우 fork_point_lsn **recovery_fork_guid**은 **fork_point_lsn** 현재 분기 지점의 로그 시퀀스 번호입니다. 그렇지 않으면 값은 NULL입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;카탈로그 뷰](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [데이터베이스 및 파일 카탈로그 뷰 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [RESTORE HEADERONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리에 대한 질문과 대답](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
