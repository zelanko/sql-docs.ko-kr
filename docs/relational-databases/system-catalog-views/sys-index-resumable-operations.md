---
title: sys.index_resumable_operations (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.reviewer: 
ms.service: 
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.index_resumable_operations_TSQL
- sys.indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.indexes
- sys.index_resumable_operations
ms.assetid: 
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 53b6aad214f3d1760bb03ff340e5a5dab30c1067
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="indexresumableoperations-transact-sql"></a>index_resumable_operations (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]
**sys.index_resumable_operations** 를 모니터링 하 고 다시 시작 가능한 인덱스 다시 작성에 대 한 현재 실행 상태를 확인 하는 시스템 뷰입니다.  
**적용 대상**: SQL Server 2017 및 Azure SQL 데이터베이스 
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|이 인덱스 (null 허용 안 함) 속해 없는 개체의 ID입니다.|  
|**index_id**|**int**|인덱스 ID입니다 (null 허용 안 함)입니다. **index_id** 는 개체 내 에서만 고유 합니다.|
|**name**|**sysname**|인덱스의 이름입니다. **이름** 는 개체 내 에서만 고유 합니다.|  
|**sql_text**|**nvarchar(max)**|T-SQL DDL 문의 텍스트|
|**last_max_dop**|**smallint**|마지막 MAX_DOP 사용 (기본값 = 0)|
|**partition_number**|**int**|내에서 소유 하는 인덱스 또는 힙의 파티션 번호입니다. 대/소문자 또는 분할 되지 않은 테이블 및 인덱스에 대 한 모든 파티션을 다시 작성 값이 열은 NULL 되는 합니다.|
|**상태**|**tinyint**|다시 시작 가능한 인덱스에 대 한 작동 상태:<br /><br />0=Running<br /><br />1=Pause|
|**state_desc**|**nvarchar(60)**|작동 상태 (실행 중 또는 일시 중지) 다시 시작 가능한 인덱스에 대 한 설명|  
|**start_time**|**datetime**|인덱스 작업 시작 시간 (null 허용 안 함)|
|**last_pause_time**|**datatime**| 인덱스 작업 (null 허용) 마지막 일시 중지 시간입니다. 작업 실행을 일시 중지 된 경우 NULL입니다.|
|**total_execution_time**|**int**|시작 시간 (분) (null 허용 안 함)에서 총 실행 시간|
|**percent_complete**|**real**|인덱스 작업 진행 완료 % (null 허용 안 함).|
|**page_count**|**bigint**|새 인덱스 작성 작업 및 매핑 인덱스 (null 허용 안 함)에 의해 할당 되는 인덱스 페이지의 총 수입니다. 

## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
   
## <a name="example"></a>예제  
 일시 중지 상태에 있는 모든 다시 시작 가능한 인덱스 다시 작성 작업을 나열 합니다. 
  
```  
SELECT * FROM  sys.index_resumable_operations WHERE STATE = 1;  
```  
  
## <a name="see-also"></a>관련 항목: 
 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)    
 [카탈로그 뷰 &#40; Transact SQL &#41; ](catalog-views-transact-sql.md) [카탈로그 뷰 &#40; 개체 Transact SQL &#41; ](object-catalog-views-transact-sql.md) [sys.indexes&#40; Transact SQL &#41; ](sys-xml-indexes-transact-sql.md) [sys.index_columns&#40; Transact SQL &#41;](sys-index-columns-transact-sql.md)   
 [sys.xml_indexes &#40; Transact SQL &#41;](sys-xml-indexes-transact-sql.md)   
 [sys.objects &#40; Transact SQL &#41;](sys-index-columns-transact-sql.md)   
 [sys.key_constraints &#40; Transact SQL &#41;](sys-key-constraints-transact-sql.md)   
 [sys.filegroups &#40; Transact SQL &#41;](sys-filegroups-transact-sql.md)   
 [sys.partition_schemes &#40; Transact SQL &#41;](sys-partition-schemes-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](querying-the-sql-server-system-catalog-faq.md)   
  
