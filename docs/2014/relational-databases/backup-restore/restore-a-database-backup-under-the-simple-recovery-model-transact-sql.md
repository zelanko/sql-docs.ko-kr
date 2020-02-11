---
title: 단순 복구 모델에서 데이터베이스 백업 복원(Transact-SQL) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full backups [SQL Server]
- database restores [SQL Server], full backups
- backing up databases [SQL Server], full backups
- database backups [SQL Server], full backups
- restoring databases [SQL Server], full backups
ms.assetid: a928fa36-e285-476f-9a7b-6840a8bb7283
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e2fd00fd96fe9b0bf7e1b605d935908970d0c1fc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62875622"
---
# <a name="restore-a-database-backup-under-the-simple-recovery-model-transact-sql"></a>단순 복구 모델에서 데이터베이스 백업 복원(Transact-SQL)
  이 항목에서는 전체 데이터베이스 백업을 복원하는 방법에 대해 설명합니다.  
  
> [!IMPORTANT]  
>  이 작업을 수행하려면 복원될 데이터베이스를 현재 사용하고 있는 사람이 전체 데이터베이스 백업을 복원하는 시스템 관리자뿐이어야 합니다.  
  
## <a name="prerequisites-and-recommendations"></a>필수 조건 및 권장 사항  
  
-   암호화된 데이터베이스를 복원하려면 데이터베이스를 암호화하는 데 사용된 인증서 또는 비대칭 키에 대한 액세스 권한이 있어야 합니다. 인증서 또는 비대칭 키가 없으면 데이터베이스를 복원할 수 없습니다. 따라서 데이터베이스 암호화 키를 암호화하는 데 사용되는 인증서는 백업이 필요한 동안에는 유지되어야 합니다. 자세한 내용은 [SQL Server Certificates and Asymmetric Keys](../security/sql-server-certificates-and-asymmetric-keys.md)을 참조하세요.  
  
-   보안을 위해서는 알 수 없거나 신뢰할 수 없는 출처의 데이터베이스는 연결 또는 복원하지 않는 것이 좋습니다. 이러한 데이터베이스에 포함된 악성 코드가 의도하지 않은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드를 실행하거나 스키마 또는 물리적 데이터베이스 구조를 수정하여 오류가 발생할 수 있습니다. 알 수 없거나 신뢰할 수 없는 소스의 데이터베이스를 사용하기 전에 비프로덕션 서버의 데이터베이스에서 [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) 를 실행하여 데이터베이스에서 코드(예: 저장 프로시저 또는 다른 사용자 정의 코드)를 시험해 보세요.  
  
## <a name="database-compatibility-level-after-upgrade"></a>업그레이드 후 데이터베이스 호환성 수준  
 업그레이드 후에는 **tempdb**, **모델**, **msdb** 및 **리소스** 데이터베이스의 호환성 수준이 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 의 호환성 수준으로 설정됩니다. **마스터** 시스템 데이터베이스는 업그레이드 이전의 호환성 수준이 100 미만이 아니었다면 이전 호환성 수준으로 유지됩니다. **마스터** 의 호환성 수준이 업그레이드 이전에 100 미만이었다면 업그레이드 후에는 100으로 설정됩니다.  
  
 사용자 데이터베이스의 호환성 수준이 업그레이드 이전에 100 이상이었다면 업그레이드 후에도 동일하게 유지됩니다. 업그레이드 이전에 호환성 수준이 90이었다면 업그레이드된 데이터베이스에서는 호환성 수준이 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 지원되는 가장 낮은 호환성 수준인 100으로 설정됩니다.  
  
> [!NOTE]  
>  새 사용자 데이터베이스는 **모델** 데이터베이스의 호환성 수준을 상속합니다.  
  
## <a name="procedures"></a>프로시저  
  
#### <a name="to-restore-a-full-database-backup"></a>전체 데이터베이스 백업을 복원하려면  
  
1.  RESTORE DATABASE 문을 실행하여 전체 데이터베이스 백업을 복원합니다. 이때 다음을 지정합니다.  
  
    -   복원할 데이터베이스의 이름  
  
    -   복원할 전체 데이터베이스 백업이 있는 백업 디바이스  
  
    -   전체 데이터베이스 백업을 복원한 후 적용할 트랜잭션 로그 또는 차등 데이터베이스 백업이 있을 경우 NORECOVERY 절  
  
    > [!IMPORTANT]  
    >  암호화된 데이터베이스를 복원하려면 데이터베이스를 암호화하는 데 사용된 인증서 또는 비대칭 키에 대한 액세스 권한이 있어야 합니다. 인증서 또는 비대칭 키가 없으면 데이터베이스를 복원할 수 없습니다. 따라서 데이터베이스 암호화 키를 암호화하는 데 사용되는 인증서는 백업이 필요한 동안에는 유지되어야 합니다. 자세한 내용은 [SQL Server Certificates and Asymmetric Keys](../security/sql-server-certificates-and-asymmetric-keys.md)을 참조하세요.  
  
2.  필요에 따라 다음을 지정할 수도 있습니다.  
  
    -   복원할 백업 디바이스의 백업 세트를 식별하기 위한 FILE 절  
  
> [!NOTE]  
>  이전 버전 데이터베이스를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 복원하면 데이터베이스가 자동으로 업그레이드됩니다. 일반적으로 데이터베이스는 즉시 사용할 수 있습니다. 그러나 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스에 전체 텍스트 인덱스가 있는 경우 업그레이드 프로세스는  **upgrade_option** 서버 속성의 설정에 따라 인덱스를 가져오거나 다시 설정하거나 다시 작성합니다. 업그레이드 옵션이 가져오기(**upgrade_option** = 2) 또는 다시 작성(**upgrade_option** = 0)으로 설정되어 있는 경우 업그레이드하는 동안 전체 텍스트 인덱스를 사용할 수 없습니다. 인덱싱되는 데이터 양에 따라 가져오기 작업은 몇 시간씩 걸릴 수 있으며 다시 작성 작업은 10배 정도 더 걸릴 수 있습니다. 업그레이드 옵션이 가져오기로 설정되어 있으면 전체 텍스트 카탈로그를 사용할 수 없는 경우 관련된 전체 텍스트 인덱스가 다시 작성됩니다. **upgrade_option** 서버 속성의 설정을 변경하려면 [sp_fulltext_service](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql)를 사용합니다.  
  
## <a name="example"></a>예제  
  
### <a name="description"></a>Description  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 전체 데이터베이스 백업을 테이프에서 복원합니다.  
  
### <a name="example"></a>예제  
  
```  
USE master;  
GO  
RESTORE DATABASE AdventureWorks2012  
   FROM TAPE = '\\.\Tape0';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [전체 데이터베이스 복원&#40;전체 복구 모델&#41;](complete-database-restores-full-recovery-model.md)   
 [전체 데이터베이스 복원&#40;단순 복구 모델&#41;](complete-database-restores-simple-recovery-model.md)   
 [전체 데이터베이스 백업&#40;SQL Server&#41;](full-database-backups-sql-server.md)   
 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [백업 기록 및 헤더 정보&#40;SQL Server&#41;](backup-history-and-header-information-sql-server.md)   
 [시스템 데이터베이스 다시 작성](../databases/system-databases.md)  
  
  
