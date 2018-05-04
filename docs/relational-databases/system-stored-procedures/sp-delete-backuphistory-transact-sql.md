---
title: sp_delete_backuphistory (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_delete_backuphistory
- sp_delete_backuphistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_backuphistory
ms.assetid: bdb56834-616e-47e4-b942-e895d2325e97
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ec51b862cbaf3709fa1eeedf41f2e8167b093184
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spdeletebackuphistory-transact-sql"></a>sp_delete_backuphistory(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 날짜보다 오래된 백업 세트의 항목을 삭제하여 백업 및 복원 기록 테이블의 크기를 줄입니다. 행이 추가 백업에 추가 되 고 각 백업 후 복원 기록 테이블 또는 복원 작업이 수행 됩니다. 따라서 다음 정기적으로 실행 하는 **sp_delete_backuphistory**합니다.  
  
> [!NOTE]  
>  백업 및 복원 기록 테이블은 **msdb** 데이터베이스입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_backuphistory [ @oldest_date = ] 'oldest_date'   
```  
  
## <a name="arguments"></a>인수  
 [ **@oldest_date=** ] **'***oldest_date***'**  
 백업 및 복원 기록 테이블에서 보유하고 있는 가장 오래된 날짜입니다. *oldest_date* 은 **datetime**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>주의  
 **sp_delete_backuphistory** 에서 실행 되어야 합니다는 **msdb** 데이터베이스에 있으며 다음 테이블에 영향을 줍니다.  
  
-   [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md)  
  
-   [backupfilegroup](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)  
  
-   [backupmediafamily](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)  
  
-   [backupmediaset](../../relational-databases/system-tables/backupmediaset-transact-sql.md)  
  
-   [backupset](../../relational-databases/system-tables/backupset-transact-sql.md)  
  
-   [restorefile](../../relational-databases/system-tables/restorefile-transact-sql.md)  
  
-   [restorefilegroup](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)  
  
-   [restorehistory](../../relational-databases/system-tables/restorehistory-transact-sql.md)  
  
 물리적 백업 파일은 모든 기록이 삭제된 경우에도 유지됩니다.  
  
## <a name="permissions"></a>Permissions  
 멤버 자격이 필요는 **sysadmin** 고정된 서버 역할을 하지만 사용 권한을 다른 사용자에 게 부여할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 백업 및 복원 기록 테이블에서 2010년 1월 14일 오전 12시 이전의 모든 항목을 삭제합니다.  
  
```  
USE msdb;  
GO  
EXEC sp_delete_backuphistory @oldest_date = '01/14/2010';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_delete_database_backuphistory &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-backuphistory-transact-sql.md)   
 [백업 기록 및 헤더 정보&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  
