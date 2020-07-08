---
title: sys. sp_rda_reconcile_batch (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_reconcile_batch
- sys.sp_rda_reconcile_batch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_batch stored procedure
ms.assetid: 6d21eac3-7b6c-4fe0-8bc4-bf503f3948a6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c8ce7b946005eca97d57ef709557ec9b4334339c
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2020
ms.locfileid: "86053237"
---
# <a name="syssp_rda_reconcile_batch-transact-sql"></a>sys. sp_rda_reconcile_batch (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  스트레치 사용 SQL Server 테이블에 저장 된 일괄 처리 ID를 원격 Azure 테이블에 저장 된 일괄 처리 ID로 조정 합니다.  
  
 일반적으로 원격 테이블에서 가장 최근에 마이그레이션한 데이터를 수동으로 삭제 한 경우에만 **sp_rda_reconcile_batch** 를 실행 해야 합니다. 최신 일괄 처리가 포함 된 원격 데이터를 수동으로 삭제 하면 일괄 처리 Id가 동기화 되지 않고 마이그레이션이 중지 됩니다.  
 
 이미 Azure로 마이그레이션된 데이터를 삭제 하려면이 페이지의 설명을 참조 하세요.
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
   
## <a name="syntax"></a>구문  
  
```  
  
sp_rda_reconcile_batch @objname = '@objname'  
  
```  
  
## <a name="arguments"></a>인수  
 \@objname = '* \@ objname*'  
 스트레치 사용 SQL Server 테이블의 이름입니다.  
  
## <a name="permissions"></a>사용 권한  
 Db_owner 권한이 필요 합니다.  
  
## <a name="remarks"></a>설명  
 이미 Azure로 마이그레이션된 데이터를 삭제 하려면 다음 작업을 수행 합니다.  
  
1.  데이터 마이그레이션을 일시 중지 합니다. 자세한 내용은 [데이터 마이그레이션 일시 중지 및 다시 계속&#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)을 참조하세요.  
  
2.  STAGE_ONLY 힌트와 함께 DELETE 명령을 실행 하 여 SQL Server 준비 테이블에서 데이터를 삭제 합니다. 자세한 내용은 [관리 업데이트 및 삭제 만들기](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md#adminHints)를 참조 하세요.
  
3.  REMOTE_ONLY 힌트와 함께 DELETE 명령을 실행 하 여 원격 Azure 테이블에서 동일한 데이터를 삭제 합니다.  
  
4.  **Sp_rda_reconcile_batch**를 실행 합니다.  
  
5.  데이터 마이그레이션을 다시 시작 합니다. 자세한 내용은 [데이터 마이그레이션 일시 중지 및 다시 계속&#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 일괄 처리 Id를 조정 하려면 다음 문을 실행 합니다.  
  
```sql  
EXEC sp_rda_reconcile_batch @objname = N'StretchEnabledTableName';  
```  
  
  
