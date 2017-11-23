---
title: sp_check_dynamic_filters (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
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
helpviewer_keywords: sp_check_dynamic_filters
ms.assetid: dd7760db-a3a5-460f-bd97-b8d436015e19
caps.latest.revision: "23"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 096c6ff70b712b283191afeddbb7e9d9c6afd36a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spcheckdynamicfilters-transact-sql"></a>sp_check_dynamic_filters(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  게시에 대해 매개 변수가 있는 행 필터 속성에 대한 정보, 특히 게시에 대한 필터링된 데이터 파티션을 생성하는 데 사용하는 함수와 이 게시에서 사전 계산 파티션만 사용하도록 한정하는지 여부를 표시합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_check_dynamic_filters [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>인수  
 [  **@publication** =] **'***게시***'**  
 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|게시에서 사전 계산된 파티션을 사용 하기 위한 사전은 여기서 **1** precomputed 파티션을 사용할 수 있다는 것을 의미 하 고 **0** 있습니다 사용할 수 없음을 의미 합니다.|  
|**has_dynamic_filters**|**bit**|게시;에서 하나 이상의 매개 변수가 있는 행 필터 정의 된 경우 여기서 **1** 하나 이상의 매개 변수가 있는 행 필터가 존재 하는 방법 및 **0** 동적 필터가 존재 함을 의미 합니다.|  
|**dynamic_filters_function_list**|**nvarchar (500)**|게시에서 아티클을 필터링하는 데 사용하는 함수의 목록입니다. 목록에서 각 함수는 세미콜론으로 구분되어 있습니다.|  
|**validate_subscriber_info**|**nvarchar (500)**|게시에서 아티클을 필터링하는 데 사용하는 함수의 목록입니다. 목록에서 각 함수는 더하기 기호(+)로 구분되어 있습니다.|  
|**uses_host_name**|**bit**|경우는 [host_name ()](../../t-sql/functions/host-name-transact-sql.md) 함수가 매개 변수가 있는 행 필터에 사용 될 여기서 **1** 이 함수가 동적 필터링에 사용 됨을 의미 합니다.|  
|**uses_suser_sname**|**bit**|경우는 [suser_sname ()](../../t-sql/functions/suser-sname-transact-sql.md) 함수가 매개 변수가 있는 행 필터에 사용 될 여기서 **1** 이 함수가 동적 필터링에 사용 됨을 의미 합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_check_dynamic_filters** 병합 복제에 사용 됩니다.  
  
 게시가 사전 계산된 파티션을 사용 하도록 정의 된 경우 **sp_check_dynamic_filters** 사전 계산 파티션의 제한이 위반에 대 한 확인 합니다. 위반이 발견된 경우 오류가 반환됩니다. 자세한 내용은 [사전 계산 파티션으로 매개 변수가 있는 필터 성능 최적화](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)를 참조하세요.  
  
 매개 변수가 있는 행 필터가 있는 것처럼 게시를 정의했는데 매개 변수가 있는 필터가 없으면 오류가 반환됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_check_dynamic_filters**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [매개 변수가 있는 필터로 병합 게시에 대 한 파티션 관리](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)   
 [sp_check_join_filter &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-check-join-filter-transact-sql.md)   
 [sp_check_subset_filter &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-check-subset-filter-transact-sql.md)  
  
  
