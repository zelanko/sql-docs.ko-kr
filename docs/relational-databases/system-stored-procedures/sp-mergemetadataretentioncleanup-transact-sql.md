---
title: sp_mergemetadataretentioncleanup (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_mergemetadataretentioncleanup
- sp_mergemetadataretentioncleanup_TSQL
helpviewer_keywords:
- sp_mergemetadataretentioncleanup
ms.assetid: 4e8d6343-2a38-421d-a3f3-c37d437a0f88
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 4ac0c7820ab4f336057a3d747409b0e1af09248d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spmergemetadataretentioncleanup-transact-sql"></a>sp_mergemetadataretentioncleanup(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  메타 데이터를 수동으로 정리는 [MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md), [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md), [MSmerge_past_partition_ 매핑](../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md), 및 [MSmerge_current_partition_mappings](../../relational-databases/system-tables/msmerge-current-partition-mappings.md) 시스템 테이블입니다. 이 저장 프로시저는 토폴로지의 게시자 및 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_mergemetadataretentioncleanup [ [ @num_genhistory_rows = ] num_genhistory_rows OUTPUT ]  
    [ , [ @num_contents_rows = ] num_contents_rows OUTPUT ]   
    [ , [ @num_tombstone_rows = ] num_tombstone_rows OUTPUT ]   
    [ , [ @aggressive_cleanup_only = ] aggressive_cleanup_only ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@num_genhistory_rows=** ] *num_genhistory_rows* 출력  
 정리 된 행의 수를 반환 된 [MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md) 테이블입니다. *num_genhistory_rows* 은 **int**, 기본값은 **0**합니다.  
  
 [  **@num_contents_rows=** ] *num_contents_rows* 출력  
 정리 된 행의 수를 반환 된 [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) 테이블입니다. *num_contents_rows* 은 **int**, 기본값은 **0**합니다.  
  
 [  **@num_tombstone_rows=** ] *num_tombstone_rows* 출력  
 정리 된 행의 수를 반환 된 [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) 테이블입니다. *num_tombstone_rows* 은 **int**, 기본값은 **0**합니다.  
  
 [  **@aggressive_cleanup_only=** ] *aggressive_cleanup_only*  
 내부적으로만 사용됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
  
> [!IMPORTANT]  
>  데이터베이스에 게시가 여러 개 있고 이러한 게시 중 하나가 무한 게시 보존 기간을 사용 하 여, 실행 **sp_mergemetadataretentioncleanup** 병합 복제 변경 내용 추적 정리 하지 않습니다 데이터베이스에 대 한 메타 데이터입니다. 그러므로 무한 게시 보존은 신중히 사용하십시오. 게시에 무한 보존 기간이 있는지를 확인 하려면 실행 [sp_helpmergepublication &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md) 게시자에서 결과의 모든 게시의 값을 사용 하 여 설정 **0** 에 대 한 **보존**합니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **db_owner** 고정 데이터베이스 역할 또는 게시 액세스 목록에 사용자가 실행할 수 있는 게시 된 데이터베이스에 대 한 **sp_mergemetadataretentioncleanup**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
