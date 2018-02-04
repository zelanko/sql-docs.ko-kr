---
title: syscollector_collection_sets (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- syscollector_collection_sets_TSQL
- syscollector_collection_sets
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- syscollector_collection_sets view
ms.assetid: db0def92-f25b-45da-9709-eab972b33800
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e9f33a49eef6a80e058a12ff032322bb9060c7af
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="syscollectorcollectionsets-transact-sql"></a>syscollector_collection_sets(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  일정, 컬렉션 모드 및 해당 상태를 포함한 컬렉션 집합에 대한 정보를 제공합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|collection_set_id|**int**|컬렉션 집합의 로컬 식별자입니다. Null을 허용하지 않습니다.|  
|collection_set_uid|**uniqueidentifier**|컬렉션 집합의 전역 고유 식별자입니다. Null을 허용하지 않습니다.|  
|name|**nvarchar(4000)**|컬렉션 집합의 이름입니다. Null을 허용합니다.|  
|target|**nvarchar(max)**|컬렉션 집합의 대상을 식별합니다. Null을 허용합니다.|  
|is_system|**bit**|설정(1) 또는 해제(0)하여 컬렉션 집합이 데이터 수집기에 포함되는지, 아니면 dc_admin에 의해 나중에 추가되는지를 나타냅니다. 이는 자체적으로 또는 타사에서 개발한 사용자 지정 컬렉션 집합이 될 수 있습니다. Null을 허용하지 않습니다.|  
|is_running|**bit**|컬렉션 집합이 실행 중인지 여부를 나타냅니다. Null을 허용하지 않습니다.|  
|collection_mode|**smallint**|컬렉션 집합에 대한 컬렉션 모드를 지정합니다. Null을 허용하지 않습니다.<br /><br /> 컬렉션 모드는 다음 중 하나입니다.<br /><br /> 0 - 캐시된 모드. 데이터 컬렉션과 업로드가 별도의 일정에 속해 있습니다.<br /><br /> 1 - 캐시되지 않은 모드. 데이터 컬렉션과 업로드가 같은 일정에 속해 있습니다.|  
|proxy_id|**int**|컬렉션 집합 작업 단계를 실행하는 데 사용되는 프록시를 식별합니다. Null을 허용합니다.|  
|schedule_uid|**uniqueidentifier**|컬렉션 집합 일정에 대한 포인터를 제공합니다. Null을 허용합니다.|  
|collection_job_id|**uniqueidentifier**|컬렉션 작업을 식별합니다. Null을 허용합니다.|  
|upload_job_id|**uniqueidentifier**|컬렉션 업로드 작업을 식별합니다. Null을 허용합니다.|  
|logging_level|**smallint**|로깅 수준(0, 1 또는 2)을 지정합니다. Null을 허용하지 않습니다.|  
|days_until_expiration|**smallint**|수집된 데이터가 관리 데이터 웨어하우스에 저장되는 일 수입니다. Null을 허용하지 않습니다.|  
|description|**nvarchar(4000)**|컬렉션 집합을 설명합니다. Null을 허용합니다.|  
|dump_on_any_error|**bit**|설정 (1) 또는 해제 (0)를 만들지 여부를 지정 하는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 덤프 파일에 오류가 있습니다. Null을 허용하지 않습니다.|  
|dump_on_codes|**nvarchar(max)**|덤프 파일을 트리거하는 데 사용되는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 오류 코드 목록을 포함합니다. Null을 허용합니다.|  
  
## <a name="permissions"></a>Permissions  
 dc_operator, dc_proxy에 대한 SELECT가 필요합니다.  
  
## <a name="remarks"></a>주의  
 데이터 수집기 API를 통해 사용자는 자신이 만든 컬렉션 집합만 변경 또는 삭제할 수 있습니다. 시스템에서 제공되는 컬렉션 집합은 수정 또는 삭제할 수 없지만 시스템 컬렉션 집합을 사용하거나 사용하지 않도록 설정하고 해당 구성을 변경할 수는 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 수집기 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [데이터 수집기 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)  
  
  
