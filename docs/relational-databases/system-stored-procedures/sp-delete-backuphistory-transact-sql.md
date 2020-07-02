---
title: sp_delete_backuphistory (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_backuphistory
- sp_delete_backuphistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_backuphistory
ms.assetid: bdb56834-616e-47e4-b942-e895d2325e97
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 64fef5a7f6d135961a6757a92d734e75f2114273
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760106"
---
# <a name="sp_delete_backuphistory-transact-sql"></a>sp_delete_backuphistory(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  지정한 날짜보다 오래된 백업 세트의 항목을 삭제하여 백업 및 복원 기록 테이블의 크기를 줄입니다. 각 백업 또는 복원 작업을 수행한 후에 추가 행이 백업 및 복원 기록 테이블에 추가 됩니다. 따라서 **sp_delete_backuphistory**을 정기적으로 실행 하는 것이 좋습니다.  
  
> [!NOTE]  
>  백업 및 복원 기록 테이블은 **msdb** 데이터베이스에 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_backuphistory [ @oldest_date = ] 'oldest_date'   
```  
  
## <a name="arguments"></a>인수  
`[ @oldest_date = ] 'oldest\_date'`백업 및 복원 기록 테이블에 보존 되는 가장 오래 된 날짜입니다. *oldest_date* 은 **datetime**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 **sp_delete_backuphistory** **msdb** 데이터베이스에서 실행 해야 하며 다음 테이블에 영향을 줍니다.  
  
-   [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md)  
  
-   [backupfilegroup](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)  
  
-   [backupmediafamily](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)  
  
-   [backupmediaset](../../relational-databases/system-tables/backupmediaset-transact-sql.md)  
  
-   [backupset](../../relational-databases/system-tables/backupset-transact-sql.md)  
  
-   [restorefile](../../relational-databases/system-tables/restorefile-transact-sql.md)  
  
-   [restorefilegroup](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)  
  
-   [restorehistory](../../relational-databases/system-tables/restorehistory-transact-sql.md)  
  
 물리적 백업 파일은 모든 기록이 삭제된 경우에도 유지됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버 자격이 필요 하지만 다른 사용자에 게 사용 권한을 부여할 수 있습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 백업 및 복원 기록 테이블에서 2010년 1월 14일 오전 12시 이전의 모든 항목을 삭제합니다.  
  
```  
USE msdb;  
GO  
EXEC sp_delete_backuphistory @oldest_date = '01/14/2010';  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_delete_database_backuphistory &#40;](../../relational-databases/system-stored-procedures/sp-delete-database-backuphistory-transact-sql.md)   
 [백업 기록 및 헤더 정보&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  
