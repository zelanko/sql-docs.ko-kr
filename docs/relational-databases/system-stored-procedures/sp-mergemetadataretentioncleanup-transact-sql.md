---
title: sp_mergemetadataretentioncleanup (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergemetadataretentioncleanup
- sp_mergemetadataretentioncleanup_TSQL
helpviewer_keywords:
- sp_mergemetadataretentioncleanup
ms.assetid: 4e8d6343-2a38-421d-a3f3-c37d437a0f88
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 78ef8690e4f8dd374125d4c8e6e77a4a1964d329
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828317"
---
# <a name="sp_mergemetadataretentioncleanup-transact-sql"></a>sp_mergemetadataretentioncleanup(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md), [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md), [MSmerge_past_partition_mappings](../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md)및 [MSmerge_current_partition_mappings](../../relational-databases/system-tables/msmerge-current-partition-mappings.md) 시스템 테이블에서 메타 데이터의 수동 정리를 수행 합니다. 이 저장 프로시저는 토폴로지의 게시자 및 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_mergemetadataretentioncleanup [ [ @num_genhistory_rows = ] num_genhistory_rows OUTPUT ]  
    [ , [ @num_contents_rows = ] num_contents_rows OUTPUT ]   
    [ , [ @num_tombstone_rows = ] num_tombstone_rows OUTPUT ]   
    [ , [ @aggressive_cleanup_only = ] aggressive_cleanup_only ]  
```  
  
## <a name="arguments"></a>인수  
`[ @num_genhistory_rows = ] num_genhistory_rows OUTPUT`[MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md) 테이블에서 정리 된 행 수를 반환 합니다. *num_genhistory_rows* 은 **int**이며 기본값은 **0**입니다.  
  
`[ @num_contents_rows = ] num_contents_rows OUTPUT`[MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) 테이블에서 정리 된 행 수를 반환 합니다. *num_contents_rows* 은 **int**이며 기본값은 **0**입니다.  
  
`[ @num_tombstone_rows = ] num_tombstone_rows OUTPUT`[MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) 테이블에서 정리 된 행 수를 반환 합니다. *num_tombstone_rows* 은 **int**이며 기본값은 **0**입니다.  
  
`[ @aggressive_cleanup_only = ] aggressive_cleanup_only`내부용 으로만 사용 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
  
> [!IMPORTANT]  
>  데이터베이스에 게시가 여러 개 있고 이러한 게시 중 하나가 무한 게시 보존 기간을 사용 하는 경우 **sp_mergemetadataretentioncleanup** 를 실행 해도 데이터베이스의 병합 복제 변경 내용 추적 메타 데이터가 정리 되지 않습니다. 그러므로 무한 게시 보존은 신중히 사용하십시오. 게시에 무한 보존 기간이 있는지 확인 하려면 게시자에서 [sp_helpmergepublication &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md) 을 실행 하 고 결과 집합의 모든 게시에 대해 **보존**기간으로 **0** 값을 기록해 둡니다.  
  
## <a name="permissions"></a>권한  
 **Db_owner** 고정 데이터베이스 역할의 멤버 또는 게시 된 데이터베이스에 대 한 게시 액세스 목록의 사용자만 **sp_mergemetadataretentioncleanup**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
