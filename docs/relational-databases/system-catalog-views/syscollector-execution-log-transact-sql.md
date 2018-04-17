---
title: syscollector_execution_log (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- syscollector_execution_log_TSQL
- syscollector_execution_log
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- syscollector_execution_log view
ms.assetid: 11554d64-0426-42ce-b7ce-5591f67864d2
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7cf0ba566294c5a89db0e67d0d55a37abf228a17
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="syscollectorexecutionlog-transact-sql"></a>syscollector_execution_log(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  실행 로그의 컬렉션 집합 또는 패키지에 대한 정보를 제공합니다.   
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|log_id|**bigint**|각 컬렉션 집합의 실행을 식별합니다. 이 뷰와 자세한 다른 로그를 조인하는 데 사용됩니다. Null을 허용하지 않습니다.|  
|parent_log_id|**bigint**|부모 패키지 또는 컬렉션 집합을 식별합니다. Null을 허용하지 않습니다. ID는 부모-자식 관계로 연결되어 있으므로 어떤 패키지가 어떤 컬렉션 집합에서 시작되었는지 파악할 수 있습니다. 이 뷰는 로그 항목을 부모-자식 연결로 그룹화하고 패키지의 이름을 들여쓰기로 처리하여 호출 체인을 명확히 볼 수 있도록 합니다.|  
|collection_set_id|**int**|이 로그 항목이 나타내는 컬렉션 집합 또는 패키지를 식별합니다. Null을 허용하지 않습니다.|  
|collection_item_id|**int**|컬렉션 항목을 식별합니다. Null을 허용합니다.|  
|start_time|**datetime**|컬렉션 집합 또는 패키지가 시작된 시간입니다. Null을 허용하지 않습니다.|  
|last_iteration_time|**datetime**|패키지를 계속 실행하기 위해 패키지에서 마지막으로 스냅숏을 캡처한 시간입니다. Null을 허용합니다.|  
|finish_time|**datetime**|종료된 패키지 및 컬렉션 집합의 실행 완료 시간입니다. Null을 허용합니다.|  
|runtime_execution_mode|**smallint**|컬렉션 집합 활동이 데이터 수집이었는지 데이터 업로드였는지를 나타냅니다. Null을 허용합니다.<br /><br /> 값은 다음과 같습니다.<br /><br /> 0 = 컬렉션<br /><br /> 1 = 업로드|  
|상태|**smallint**|컬렉션 집합 또는 패키지의 현재 상태를 나타냅니다. Null을 허용하지 않습니다.<br /><br /> 값은 다음과 같습니다.<br /><br /> 0 = 실행 중<br /><br /> 1 = 완료<br /><br /> 2 = 실패|  
|적용한 후|**nvarchar(128)**|컬렉션 집합 또는 패키지를 시작한 사용자를 식별합니다. Null을 허용하지 않습니다.|  
|package_id|**uniqueidentifier**|이 로그를 생성한 컬렉션 집합 또는 패키지를 식별합니다. Null을 허용합니다.|  
|package_name|**nvarchar(4000)**|이 로그를 생성한 패키지의 이름입니다. Null을 허용합니다.|  
|package_execution_id|**uniqueidentifier**|[!INCLUDE[ssIS](../../includes/ssis-md.md)] 로그 테이블에 대한 링크를 제공합니다. Null을 허용합니다.|  
|failure_message|**nvarchar(2048)**|컬렉션 집합 또는 패키지가 실패한 경우 해당 구성 요소에 대한 가장 최근의 오류 메시지입니다. Null을 허용합니다. 자세한 오류 정보를 가져오려면는 [fn_syscollector_get_execution_details &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-functions/fn-syscollector-get-execution-details-transact-sql.md) 함수입니다.|  
  
## <a name="permissions"></a>Permissions  
 dc_operator에 대한 SELECT가 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 수집기 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [데이터 수집기 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)  
  
  
