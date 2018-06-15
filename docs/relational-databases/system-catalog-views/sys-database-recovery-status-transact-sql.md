---
title: sys.database_recovery_status (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2cdefec3d2f5ffd6a8ce326c4d3afd78df47de44
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33181269"
---
# <a name="sysdatabaserecoverystatus-transact-sql"></a>sys.database_recovery_status(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스당 하나의 행을 포함합니다. 데이터베이스가 열려 있지 않으면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 해당 데이터베이스를 시작하려고 합니다.  
  
 아닌 다른 데이터베이스에 대 한 행을 보려면 **마스터** 또는 **tempdb**, 다음 중 하나를 적용 해야 합니다.  
  
-   데이터베이스 소유자입니다.  
  
-   ALTER ANY DATABASE 또는 VIEW ANY DATABASE 서버 수준 권한이 있습니다.  
  
-   대 한 CREATE DATABASE 권한이 **마스터** 데이터베이스입니다.    
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내에서 고유한 데이터베이스 ID입니다.|  
|**database_guid**|**uniqueidentifier**|데이터베이스의 모든 데이터베이스 파일을 함께 연결하는 데 사용됩니다. 데이터베이스를 제대로 시작하려면 모든 파일의 헤더 페이지에 이 GUID가 있어야 합니다. 현재까지는 하나의 데이터베이스에만 이 GUID가 있었습니다. 그러나 데이터베이스를 복사하고 연결하여 GUID를 중복하여 만들 수 있습니다. 아직 존재하지 않는 데이터베이스를 복원할 때 RESTORE는 항상 새 GUID를 생성합니다.<br /><br /> NULL= 데이터베이스가 오프라인이거나 데이터베이스를 시작할 수 없습니다.|  
|**family_guid**|**uniqueidentifier**|일치하는 복원 상태를 검색하는 데이터베이스 "백업 패밀리"의 식별자입니다.<br /><br /> NULL= 데이터베이스가 오프라인이거나 데이터베이스를 시작할 수 없습니다.|  
|**last_log_backup_lsn**|**numeric(25,0)**|다음 로그 백업의 시작 로그 시퀀스 번호입니다.<br /><br /> Null 인 경우, 트랜잭션 로그 백업까지 수행할 수 없습니다 데이터베이스가 단순 복구에 있거나 현재 데이터베이스 백업이 없는 있기 때문에.|  
|**recovery_fork_guid**|**uniqueidentifier**|데이터베이스가 현재 활성화되어 있는 복구 분기 지점을 식별합니다.<br /><br /> NULL= 데이터베이스가 오프라인이거나 데이터베이스를 시작할 수 없습니다.|  
|**first_recovery_fork_guid**|**uniqueidentifier**|복구 분기 시작 지점의 식별자입니다.<br /><br /> NULL= 데이터베이스가 오프라인이거나 데이터베이스를 시작할 수 없습니다.|  
|**fork_point_lsn**|**numeric(25,0)**|경우 **first_recovery_fork_guid** 가 아닌 (! =)를 **recovery_fork_guid**, **fork_point_lsn** 현재 분기 지점의 로그 시퀀스 번호입니다. 그렇지 않으면 값은 NULL입니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [데이터베이스 및 파일 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [RESTORE HEADERONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
