---
title: syscollector_collection_sets (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 62b63057e34c2d26ad9d8ee3689267c9a06c93dc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754311"
---
# <a name="syscollector_collection_sets-transact-sql"></a>syscollector_collection_sets(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  일정, 컬렉션 모드 및 해당 상태를 포함한 컬렉션 집합에 대한 정보를 제공합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|collection_set_id|**int**|컬렉션 집합의 로컬 식별자입니다. Null을 허용하지 않습니다.|  
|collection_set_uid|**uniqueidentifier**|컬렉션 집합의 전역 고유 식별자입니다. Null을 허용하지 않습니다.|  
|name|**nvarchar(4000)**|컬렉션 집합의 이름입니다. Null을 허용합니다.|  
|대상|**nvarchar(max)**|컬렉션 집합의 대상을 식별합니다. Null을 허용합니다.|  
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
|dump_on_any_error|**bit**|On (1) 또는 off (0)를 설정 하 여 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 오류 발생 시 덤프 파일을 만들지 여부를 나타냅니다. Null을 허용하지 않습니다.|  
|dump_on_codes|**nvarchar(max)**|덤프 파일을 트리거하는 데 사용되는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 오류 코드 목록을 포함합니다. Null을 허용합니다.|  
  
## <a name="permissions"></a>사용 권한  
 dc_operator, dc_proxy에 대한 SELECT가 필요합니다.  
  
## <a name="remarks"></a>설명  
 데이터 수집기 API를 통해 사용자는 자신이 만든 컬렉션 집합만 변경 또는 삭제할 수 있습니다. 시스템에서 제공되는 컬렉션 집합은 수정 또는 삭제할 수 없지만 시스템 컬렉션 집합을 사용하거나 사용하지 않도록 설정하고 해당 구성을 변경할 수는 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;데이터 수집기 저장 프로시저](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;데이터 수집기 뷰](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [데이터 수집](../../relational-databases/data-collection/data-collection.md)  
  
  
