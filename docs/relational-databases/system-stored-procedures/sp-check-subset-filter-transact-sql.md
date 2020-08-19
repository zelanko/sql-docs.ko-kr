---
description: sp_check_subset_filter(Transact-SQL)
title: sp_check_subset_filter (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_check_TSQL
- sp_check_subset_filter
- filter
- subset
- subset_TSQL
- sp_check
- sp_check_subset_filter_TSQL
helpviewer_keywords:
- sp_check_subset_filter
ms.assetid: 525cfcfc-f317-478d-ba84-72e62285f160
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 55b5160842e5be4bda385fd23afd22d304dc2dae
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486185"
---
# <a name="sp_check_subset_filter-transact-sql"></a>sp_check_subset_filter(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  테이블에 대해 필터 절이 유효한지 확인하는 데 사용됩니다. 이 저장 프로시저는 필터를 사전 계산 파티션과 함께 사용할 수 있는지 여부와 더불어 제공된 필터에 관한 정보를 반환합니다. 이 저장 프로시저는 게시가 포함된 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_check_subset_filter [ @filtered_table = ] 'filtered_table'  
        , [ @subset_filterclause = ] 'subset_filterclause'  
    [ , [ @has_dynamic_filters = ] has_dynamic_filters OUTPUT ]  
```  
  
## <a name="arguments"></a>인수  
`[ @filtered_table = ] 'filtered_table'` 필터링 된 테이블의 이름입니다. *filtered_table* 은 **nvarchar (400)** 이며 기본값은 없습니다.  
  
`[ @subset_filterclause = ] 'subset_filterclause'` 테스트 중인 필터 절입니다. *subset_filterclause* 는 **nvarchar (1000)** 이며 기본값은 없습니다.  
  
`[ @has_dynamic_filters = ] has_dynamic_filters` 필터 절이 매개 변수가 있는 행 필터 인지 여부입니다. *has_dynamic_filters* 은 **bit**이며 기본값은 NULL이 고 출력 매개 변수입니다. 필터 절이 매개 변수가 있는 행 필터 이면 값 **1** 을 반환 합니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|게시가 사전 계산 파티션을 사용 하기에 적합 한지 여부입니다. 여기서 **1** 은 사전 계산 파티션을 사용할 수 있음을 의미 하 고 **0** 은 사용할 수 없음을 의미 합니다.|  
|**has_dynamic_filters**|**bit**|제공 된 필터 절에 매개 변수가 있는 행 필터가 하나 이상 포함 되어 있는지 여부입니다. 여기서 **1** 은 매개 변수가 있는 행 필터가 사용 됨을 의미 하 고 **0** 은 이러한 함수를 사용 하지 않음을 의미 합니다.|  
|**dynamic_filters_function_list**|**nvarchar (500)**|아티클을 동적으로 필터링하는 필터 절의 함수 목록이며 이때 각 함수는 세미콜론으로 구분됩니다.|  
|**uses_host_name**|**bit**|[HOST_NAME ()](../../t-sql/functions/host-name-transact-sql.md) 함수가 필터 절에 사용 되는 경우 **1** 은이 함수가 있음을 의미 합니다.|  
|**uses_suser_sname**|**bit**|[SUSER_SNAME ()](../../t-sql/functions/suser-sname-transact-sql.md) 함수가 필터 절에 사용 되는 경우 **1** 은이 함수가 있음을 의미 합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_check_subset_filter** 는 병합 복제에 사용 됩니다.  
  
 테이블이 게시 되지 않은 경우에도 모든 테이블에 대해 **sp_check_subset_filter** 를 실행할 수 있습니다. 이 저장 프로시저는 필터링된 아티클을 정의하기 전에 필터 절을 확인하기 위해 사용할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_check_subset_filter**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [사전 계산 파티션으로 매개 변수가 있는 필터 성능 최적화](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)  
  
  
