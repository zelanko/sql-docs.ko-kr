---
title: sp_check_subset_filter (Transact SQL) | Microsoft Docs
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
- sp_check_TSQL
- sp_check_subset_filter
- filter
- subset
- subset_TSQL
- sp_check
- sp_check_subset_filter_TSQL
helpviewer_keywords: sp_check_subset_filter
ms.assetid: 525cfcfc-f317-478d-ba84-72e62285f160
caps.latest.revision: "28"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3341c4f5fc6c637f74dabf913730e6c6e30dfcea
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spchecksubsetfilter-transact-sql"></a>sp_check_subset_filter(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  테이블에 대해 필터 절이 유효한지 확인하는 데 사용됩니다. 이 저장 프로시저는 필터를 사전 계산 파티션과 함께 사용할 수 있는지 여부와 더불어 제공된 필터에 관한 정보를 반환합니다. 이 저장 프로시저는 게시가 포함된 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_check_subset_filter [ @filtered_table = ] 'filtered_table'  
        , [ @subset_filterclause = ] 'subset_filterclause'  
    [ , [ @has_dynamic_filters = ] has_dynamic_filters OUTPUT ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@filtered_table** =] **'***filtered_table***'**  
 필터링된 테이블의 이름입니다. *filtered_table* 은 **nvarchar (400)**, 기본값은 없습니다.  
  
 [  **@subset_filterclause**  =] **'***subset_filterclause***'**  
 테스트할 필터 절입니다. *subset_filterclause* 은 **nvarchar (1000)**, 기본값은 없습니다.  
  
 [  **@has_dynamic_filters** =] *has_dynamic_filters*  
 필터 절이 매개 변수가 있는 행 필터인지 여부입니다. *has_dynamic_filters* 은 **비트**, 기본값은 NULL 이며 출력 매개 변수입니다. 값을 반환 **1** 때 필터 절이 매개 변수가 있는 행 필터.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|게시에서 사전 계산된 파티션을 사용 하기 위한 사전은 여기서 **1** precomputed 파티션을 사용할 수 있다는 것을 의미 하 고 **0** 있습니다 사용할 수 없음을 의미 합니다.|  
|**has_dynamic_filters**|**bit**|매개 변수가 있는 행 필터 중 적어도 하나의; 제공 된 필터 절에 포함 되어 있으면 여기서 **1** 매개 변수가 있는 행 필터를 사용 한다는 의미 및 **0** 이러한 함수는 사용 되지 않음을 의미 합니다.|  
|**dynamic_filters_function_list**|**nvarchar (500)**|아티클을 동적으로 필터링하는 필터 절의 함수 목록이며 이때 각 함수는 세미콜론으로 구분됩니다.|  
|**uses_host_name**|**bit**|경우는 [host_name ()](../../t-sql/functions/host-name-transact-sql.md) 필터 절에 함수를 사용 하는 여기서 **1** 이 함수에 표시 됩니다.|  
|**uses_suser_sname**|**bit**|경우는 [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) 필터 절에 함수를 사용 하는 여기서 **1** 이 함수에 표시 됩니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_check_subset_filter** 병합 복제에 사용 됩니다.  
  
 **sp_check_subset_filter** 는 게시 되지 않으면 경우에 테이블에 대해 실행할 수 있습니다. 이 저장 프로시저는 필터링된 아티클을 정의하기 전에 필터 절을 확인하기 위해 사용할 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_check_subset_filter**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [사전 계산 파티션으로 매개 변수가 있는 필터 성능 최적화](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)  
  
  
