---
title: sp_mergemetadataretentioncleanup (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_mergemetadataretentioncleanup
- sp_mergemetadataretentioncleanup_TSQL
helpviewer_keywords:
- sp_mergemetadataretentioncleanup
ms.assetid: 4e8d6343-2a38-421d-a3f3-c37d437a0f88
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6c2724e50c620342a2ac95883357f2d524ed8768
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47620927"
---
# <a name="spmergemetadataretentioncleanup-transact-sql"></a>sp_mergemetadataretentioncleanup(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  메타 데이터를 수동으로 정리 합니다 [MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)를 [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)를 [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md), [MSmerge_past_partition_ 매핑을](../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md), 및 [MSmerge_current_partition_mappings](../../relational-databases/system-tables/msmerge-current-partition-mappings.md) 시스템 테이블입니다. 이 저장 프로시저는 토폴로지의 게시자 및 구독자에서 실행됩니다.  
  
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
 정리 된 행의 수를 반환 합니다 [MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md) 테이블입니다. *num_genhistory_rows* 됩니다 **int**, 기본값은 **0**합니다.  
  
 [  **@num_contents_rows=** ] *num_contents_rows* 출력  
 정리 된 행의 수를 반환 합니다 [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) 테이블입니다. *num_contents_rows* 됩니다 **int**, 기본값은 **0**합니다.  
  
 [  **@num_tombstone_rows=** ] *num_tombstone_rows* 출력  
 정리 된 행의 수를 반환 합니다 [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) 테이블입니다. *num_tombstone_rows* 됩니다 **int**, 기본값은 **0**합니다.  
  
 [  **@aggressive_cleanup_only=** ] *aggressive_cleanup_only*  
 내부적으로만 사용됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
  
> [!IMPORTANT]  
>  이러한 게시 중 하나가 무한 게시 보존 기간을 사용 하 여 데이터베이스에 게시가 여러 개를 실행 중인 **sp_mergemetadataretentioncleanup** 병합 복제 변경 내용 추적 정리 하지 않습니다 데이터베이스에 대 한 메타 데이터입니다. 그러므로 무한 게시 보존은 신중히 사용하십시오. 게시에 무한 보존 기간이 있는지를 확인 하려면 실행 [sp_helpmergepublication &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md) 설정의 값을 사용 하 여 결과의 모든 게시 게시자 **0** 에 대 한 **보존**합니다.  
  
## <a name="permissions"></a>사용 권한  
 구성원만 합니다 **db_owner** 고정 데이터베이스 역할 또는 게시 액세스 목록에서 사용자가 게시 된 데이터베이스를 실행할 수에 대 한 **sp_mergemetadataretentioncleanup**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
