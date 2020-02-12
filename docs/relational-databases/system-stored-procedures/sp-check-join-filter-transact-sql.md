---
title: sp_check_join_filter (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
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
ms.openlocfilehash: 28589be83c62f705457e990b328be98e88905568
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68771268"
---
# <a name="sp_check_join_filter-transact-sql"></a>sp_check_join_filter(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  두 테이블 간의 조인 필터를 확인하여 조인 필터 절이 유효한지 여부를 확인하는 데 사용됩니다. 또한 이 저장 프로시저는 제공된 조인 필터를 지정된 테이블의 사전 계산 파티션에서 사용할 수 있는지 여부를 비롯하여 이 필터에 대한 정보를 반환합니다. 이 저장 프로시저는 게시자에서 게시에 대해 실행됩니다. 자세한 내용은 [사전 계산 파티션으로 매개 변수가 있는 필터 성능 최적화](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_check_join_filter [ @filtered_table = ] 'filtered_table'  
        , [@join_table = ] 'join_table'  
        , [ @join_filterclause = ] 'join_filterclause'  
```  
  
## <a name="arguments"></a>인수  
`[ @filtered_table = ] 'filtered_table'`필터링 된 테이블의 이름입니다. *filtered_table* 은 **nvarchar (400)** 이며 기본값은 없습니다.  
  
`[ @join_table = ] 'join_table'`*Filtered_table*에 조인 되는 테이블의 이름입니다. *join_table* 은 **nvarchar (400)** 이며 기본값은 없습니다.  
  
`[ @join_filterclause = ] 'join_filterclause'`테스트 중인 조인 필터 절입니다. *join_filterclause* 는 **nvarchar (1000)** 이며 기본값은 없습니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|게시가 사전 계산 파티션에 대해 한정 되는지 여부입니다. 여기서 **1** 은 precomupted 파티션을 사용할 수 있음을 의미 하 고 **0** 은 사용할 수 없음을 의미 합니다.|  
|**has_dynamic_filters**|**bit**|제공 된 필터 절에 매개 변수가 있는 필터링 함수가 하나 이상 포함 되어 있는지 여부입니다. 여기서 **1** 은 매개 변수가 있는 필터링 함수가 사용 됨을 의미 하 고 **0** 은 이러한 함수를 사용 하지 않음을 의미 합니다.|  
|**dynamic_filters_function_list**|**nvarchar (500)**|필터 절에서 아티클에 대해 매개 변수가 있는 필터를 정의하는 함수 목록입니다. 여기서 각 함수는 세미콜론으로 구분됩니다.|  
|**uses_host_name**|**bit**|[HOST_NAME ()](../../t-sql/functions/host-name-transact-sql.md) 함수가 필터 절에 사용 되는 경우 **1** 은이 함수가 있음을 의미 합니다.|  
|**uses_suser_sname**|**bit**|[SUSER_SNAME ()](../../t-sql/functions/suser-sname-transact-sql.md) 함수가 필터 절에 사용 되는 경우 **1** 은이 함수가 있음을 의미 합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_check_join_filter** 는 병합 복제에 사용 됩니다.  
  
 **sp_check_join_filter** 는 게시 되지 않은 경우에도 관련 테이블에 대해 실행할 수 있습니다. 이 저장 프로시저는 두 아티클 간의 조인 필터를 정의하기 전 조인 필터 절을 확인하는 데 사용될 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_check_join_filter**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
