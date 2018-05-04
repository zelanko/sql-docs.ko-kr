---
title: sys.sp_rda_reconcile_batch (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_reconcile_batch
- sys.sp_rda_reconcile_batch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_batch stored procedure
ms.assetid: 6d21eac3-7b6c-4fe0-8bc4-bf503f3948a6
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9b26ea87ae8efc750a83d5f42119e09a34d0fe4c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="syssprdareconcilebatch-transact-sql"></a>sys.sp_rda_reconcile_batch (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  원격 Azure 테이블에 저장 된 일괄 처리 ID로 SQL Server 스트레치 사용 테이블에 저장 된 일괄 처리 ID를 조정 합니다.  
  
 일반적으로 실행 해야 **sp_rda_reconcile_batch** 원격 테이블의 가장 최근에 마이그레이션된 데이터를 수동으로 삭제 한 경우. 가장 최근의 일괄 처리를 포함 하는 원격 데이터를 수동으로 삭제 하면 일괄 처리 Id는 동기화 하 고 마이그레이션 중지 합니다.  
 
 Azure로 이미 마이그레이션된 데이터를 삭제 하려면이 페이지에서 설명을 참조 하세요.
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
   
## <a name="syntax"></a>구문  
  
```  
  
sp_rda_reconcile_batch @objname = '@objname'  
  
```  
  
## <a name="arguments"></a>인수  
 @objname = '*@objname*'  
 SQL Server 스트레치 사용 테이블의 이름입니다.  
  
## <a name="permissions"></a>Permissions  
 Db_owner 권한이 필요합니다.  
  
## <a name="remarks"></a>주의  
 Azure로 이미 마이그레이션된 데이터를 삭제 하려면 다음 작업을 수행 합니다.  
  
1.  데이터 마이그레이션 일시 중지 합니다. 자세한 내용은 [데이터 마이그레이션 일시 중지 및 다시 계속&#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)을 참조하세요.  
  
2.  STAGE_ONLY 힌트와 함께 삭제 명령을 실행 하 여 SQL Server 준비 테이블에서 데이터를 삭제 합니다. 자세한 내용은 참조 하십시오. [관리 업데이트 및 삭제를 확인](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md#adminHints)합니다.
  
3.  REMOTE_ONLY 힌트와 함께 삭제 명령을 실행 하 여 원격 Azure 테이블에서 동일한 데이터를 삭제 합니다.  
  
4.  실행 **sp_rda_reconcile_batch**합니다.  
  
5.  데이터 마이그레이션 다시 시작 합니다. 자세한 내용은 [데이터 마이그레이션 일시 중지 및 다시 계속&#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 일괄 처리 Id을 조정 하려면 다음 문을 실행 합니다.  
  
```sql  
EXEC sp_rda_reconcile_batch @objname = N'StretchEnabledTableName';  
```  
  
  
