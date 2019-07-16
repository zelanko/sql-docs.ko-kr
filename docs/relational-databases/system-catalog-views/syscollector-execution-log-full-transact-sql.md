---
title: syscollector_execution_log_full (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syscollector_execution_log_full
- syscollector_execution_log_full_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- syscollector_execution_log_full view
ms.assetid: 6c8db22d-2e4c-4b7c-ac5a-8762ef1b175b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4bcbbf3d4e0e0b77156b7adceedbdc5aad97afdc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060362"
---
# <a name="syscollectorexecutionlogfull-transact-sql"></a>syscollector_execution_log_full(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  실행 로그가 꽉 찬 경우 컬렉션 집합 또는 패키지에 대한 정보를 제공합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|log_id|**bigint**|각 컬렉션 집합의 실행을 식별합니다. 이 뷰와 자세한 다른 로그를 조인하는 데 사용됩니다. Null을 허용합니다.|  
|parent_log_id|**bigint**|부모 패키지 또는 컬렉션 집합을 식별합니다. Null을 허용하지 않습니다. ID는 부모-자식 관계로 연결되어 있으므로 어떤 패키지가 어떤 컬렉션 집합에서 시작되었는지 파악할 수 있습니다. 이 뷰는 로그 항목을 부모-자식 연결로 그룹화하고 패키지의 이름을 들여쓰기로 처리하여 호출 체인을 명확히 볼 수 있도록 합니다.|  
|name|**nvarchar(4000)**|이 로그 항목이 나타내는 컬렉션 집합 또는 패키지의 이름입니다. Null을 허용합니다.|  
|상태|**smallint**|컬렉션 집합 또는 패키지의 현재 상태를 나타냅니다. Null을 허용합니다.<br /><br /> 값은 다음과 같습니다.<br /><br /> 0 = 실행 중<br /><br /> 1 = 완료<br /><br /> 2 = 실패|  
|runtime_execution_mode|**smallint**|컬렉션 집합 활동이 데이터 수집이었는지 데이터 업로드였는지를 나타냅니다. Null을 허용합니다.|  
|start_time|**datetime**|컬렉션 집합 또는 패키지가 시작된 시간입니다. Null을 허용합니다.|  
|last_iteration_time|**datetime**|패키지를 계속 실행하기 위해 패키지에서 마지막으로 스냅숏을 캡처한 시간입니다. Null을 허용합니다.|  
|finish_time|**datetime**|종료된 패키지 및 컬렉션 집합의 실행 완료 시간입니다. Null을 허용합니다.|  
|duration|**int**|패키지 또는 컬렉션 집합이 시작된 이후부터의 실행 시간(초)입니다. Null을 허용합니다.|  
|failure_message|**nvarchar(2048)**|컬렉션 집합 또는 패키지가 실패한 경우 해당 구성 요소에 대한 가장 최근의 오류 메시지입니다. Null을 허용합니다. 자세한 오류 정보를 가져오려면 합니다 [fn_syscollector_get_execution_details &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-functions/fn-syscollector-get-execution-details-transact-sql.md) 함수입니다.|  
|적용한 후|**nvarchar(128)**|컬렉션 집합 또는 패키지를 시작한 사용자를 식별합니다. Null을 허용합니다.|  
|package_execution_id|**uniqueidentifier**|[!INCLUDE[ssIS](../../includes/ssis-md.md)] 로그 테이블에 대한 링크를 제공합니다. Null을 허용합니다.|  
|collection_set_id|**int**|msdb의 데이터 컬렉션 구성 테이블에 대한 링크를 제공합니다. Null을 허용합니다.|  
  
## <a name="permissions"></a>사용 권한  
 에 대 한 SELECT가 필요 **dc_operator**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 수집기 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [데이터 수집기 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)  
  
  
