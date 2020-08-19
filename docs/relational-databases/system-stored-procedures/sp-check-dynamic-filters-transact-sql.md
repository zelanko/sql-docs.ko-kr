---
description: sp_check_dynamic_filters(Transact-SQL)
title: sp_check_dynamic_filters (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- dynamic_filters_TSQL
- sp_check_TSQL
- check
- sp_check_dynamic filter
- check_TSQL
- filters_TSQL
- check_dynamic_filters_TSQL
- dynamic filters
- filters
- check dynamic filters
- sp_check_dynamic filter_TSQL
- sp_check_for_sync_trigger_TSQL
- sp_check
helpviewer_keywords:
- sp_check_dynamic_filters
ms.assetid: dd7760db-a3a5-460f-bd97-b8d436015e19
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a03c61bc663597f27e3305813528edaf3e395635
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486227"
---
# <a name="sp_check_dynamic_filters-transact-sql"></a>sp_check_dynamic_filters(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  게시에 대해 매개 변수가 있는 행 필터 속성에 대한 정보, 특히 게시에 대한 필터링된 데이터 파티션을 생성하는 데 사용하는 함수와 이 게시에서 사전 계산 파티션만 사용하도록 한정하는지 여부를 표시합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_check_dynamic_filters [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'` 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|게시가 사전 계산 파티션을 사용 하기에 적합 한지 여부입니다. 여기서 **1** 은 사전 계산 파티션을 사용할 수 있음을 의미 하 고 **0** 은 사용할 수 없음을 의미 합니다.|  
|**has_dynamic_filters**|**bit**|하나 이상의 매개 변수가 있는 행 필터가 게시에 정의 되어 있으면이 고, 그렇지 않으면입니다. 여기서 **1** 은 매개 변수가 있는 행 필터가 하나 이상 존재 함을 의미 하 고 **0** 은 동적 필터가 없음을 의미 합니다.|  
|**dynamic_filters_function_list**|**nvarchar (500)**|게시에서 아티클을 필터링하는 데 사용하는 함수의 목록입니다. 목록에서 각 함수는 세미콜론으로 구분되어 있습니다.|  
|**validate_subscriber_info**|**nvarchar (500)**|게시에서 아티클을 필터링하는 데 사용하는 함수의 목록입니다. 목록에서 각 함수는 더하기 기호(+)로 구분되어 있습니다.|  
|**uses_host_name**|**bit**|[HOST_NAME ()](../../t-sql/functions/host-name-transact-sql.md) 함수가 매개 변수가 있는 행 필터에서 사용 되는 경우 **1** 은이 함수가 동적 필터링에 사용 됨을 의미 합니다.|  
|**uses_suser_sname**|**bit**|[SUSER_SNAME ()](../../t-sql/functions/suser-sname-transact-sql.md) 함수가 매개 변수가 있는 행 필터에서 사용 되는 경우 **1** 은이 함수가 동적 필터링에 사용 됨을 의미 합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_check_dynamic_filters** 는 병합 복제에 사용 됩니다.  
  
 사전 계산 파티션을 사용 하도록 게시를 정의 하는 경우 **sp_check_dynamic_filters** 는 사전 계산 파티션의 제한 사항을 위반 하는지 확인 합니다. 위반이 발견된 경우 오류가 반환됩니다. 자세한 내용은 [사전 계산 파티션으로 매개 변수가 있는 필터 성능 최적화](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)를 참조하세요.  
  
 매개 변수가 있는 행 필터가 있는 것처럼 게시를 정의했는데 매개 변수가 있는 필터가 없으면 오류가 반환됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_check_dynamic_filters**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [매개 변수가 있는 필터를 사용 하 여 병합 게시에 대 한 파티션 관리](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)   
 [Transact-sql&#41;sp_check_join_filter &#40;](../../relational-databases/system-stored-procedures/sp-check-join-filter-transact-sql.md)   
 [Transact-sql&#41;sp_check_subset_filter &#40;](../../relational-databases/system-stored-procedures/sp-check-subset-filter-transact-sql.md)  
  
  
