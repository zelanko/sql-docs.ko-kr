---
title: sp_check_join_filter (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- filter_TSQL
- sp_check_TSQL
- sp_check_join_filter
- sp_check_join_filter_TSQL
- join
- join_TSQL
- filter
- sp_check
helpviewer_keywords:
- sp_check_join_filter
ms.assetid: e9699d59-c8c9-45f6-a561-f7f95084a540
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bba95120f551af10d8a67d162339086c291190b9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47708452"
---
# <a name="spcheckjoinfilter-transact-sql"></a>sp_check_join_filter(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  두 테이블 간의 조인 필터를 확인하여 조인 필터 절이 유효한지 여부를 확인하는 데 사용됩니다. 또한 이 저장 프로시저는 제공된 조인 필터를 지정된 테이블의 사전 계산 파티션에서 사용할 수 있는지 여부를 비롯하여 이 필터에 대한 정보를 반환합니다. 이 저장 프로시저는 게시자에서 게시에 대해 실행됩니다. 자세한 내용은 [사전 계산 파티션으로 매개 변수가 있는 필터 성능 최적화](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_check_join_filter [ @filtered_table = ] 'filtered_table'  
        , [@join_table = ] 'join_table'  
        , [ @join_filterclause = ] 'join_filterclause'  
```  
  
## <a name="arguments"></a>인수  
 [ **@filtered_table**=] **'***filtered_table***'**  
 필터링된 테이블의 이름입니다. *filtered_table* 됩니다 **nvarchar(400)**, 기본값은 없습니다.  
  
 [ **@join_table**=] **'***join_table***'**  
 조인 되는 테이블의 이름인 *filtered_table*합니다. *join_table* 됩니다 **nvarchar(400)**, 기본값은 없습니다.  
  
 [ **@join_filterclause** =] **'***join_filterclause***'**  
 테스트할 조인 필터 절입니다. *join_filterclause* 됩니다 **nvarchar(1000)**, 기본값은 없습니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|사전 계산 파티션을 게시에 사전는 여기서 **1** 나타내고 파티션을 사용할 수 있음을 의미 하 고 **0** 는 사용할 수 없음을 의미 합니다.|  
|**has_dynamic_filters**|**bit**|제공 된 필터 절에 매개 변수가 있는 필터링 함수가; 하나 이상 포함 되어 있는지 여부 여기서 **1** 하는 매개 변수가 있는 필터링 함수가 사용 됨을 의미 하 고 **0** 함수를 사용 하지 않음을 의미 합니다.|  
|**dynamic_filters_function_list**|**nvarchar(500)**|필터 절에서 아티클에 대해 매개 변수가 있는 필터를 정의하는 함수 목록입니다. 여기서 각 함수는 세미콜론으로 구분됩니다.|  
|**uses_host_name**|**bit**|경우는 [host_name ()](../../t-sql/functions/host-name-transact-sql.md) 필터 절에 함수를 사용 하는 위치 **1** 이 함수에 표시 됩니다.|  
|**uses_suser_sname**|**bit**|경우는 [suser_sname ()](../../t-sql/functions/suser-sname-transact-sql.md) 필터 절에 함수를 사용 하는 위치 **1** 이 함수에 표시 됩니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_check_join_filter** 병합 복제에 사용 됩니다.  
  
 **sp_check_join_filter** 게시 되지 않은 경우에 모든 관련된 테이블에 대해 실행할 수 있습니다. 이 저장 프로시저는 두 아티클 간의 조인 필터를 정의하기 전 조인 필터 절을 확인하는 데 사용될 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_check_join_filter**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
