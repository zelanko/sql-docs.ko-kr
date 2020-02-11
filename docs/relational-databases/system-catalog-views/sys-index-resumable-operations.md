---
title: sys. index_resumable_operations (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.index_resumable_operations_TSQL
- sys.indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.indexes
- sys.index_resumable_operations
ms.assetid: ''
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d33b78710605841e4559f9c402a18210e25b2daa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73980299"
---
# <a name="sysindex_resumable_operations-transact-sql"></a>sys. index_resumable_operations (Transact-sql)

[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]
**index_resumable_operations** 는 다시 시작 가능한 인덱스 다시 작성 또는 만들기에 대 한 현재 실행 상태를 모니터링 하 고 확인 하는 시스템 뷰입니다.  
**적용 대상**: SQL Server (2017 이상) 및 Azure SQL Database
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|이 인덱스가 속한 개체의 ID입니다. null을 허용 하지 않습니다.|  
|**index_id**|**int**|인덱스의 ID입니다. null을 허용 하지 않습니다. **index_id** 는 개체 내 에서만 고유 합니다.|
|**name**|**sysname**|인덱스의 이름입니다. **이름은** 개체 내 에서만 고유 합니다.|  
|**sql_text**|**nvarchar(max)**|DDL T-sql 문 텍스트|
|**last_max_dop**|**smallint**|마지막으로 사용한 MAX_DOP (기본값 = 0)|
|**partition_number**|**int**|소유 인덱스 또는 힙 내의 파티션 번호입니다. 분할 되지 않은 테이블 및 인덱스의 경우 또는 모든 파티션이 다시 작성 되는 경우이 열의 값은 NULL입니다.|
|**상태일**|**tinyint**|다시 시작 가능한 인덱스의 작동 상태:<br /><br />0 = 실행 중<br /><br />1 = 일시 중지|
|**state_desc**|**nvarchar (60)**|다시 시작 가능한 인덱스의 작동 상태 (실행 중 또는 일시 중지 됨)에 대 한 설명입니다.|  
|**start_time**|**datetime**|인덱스 작업 시작 시간 (null 허용 안 함)|
|**last_pause_time**|**datatime**| 인덱스 작업 마지막 일시 중지 시간 (nullable)입니다. 작업이 실행 중이 고 일시 중지 되지 않은 경우 NULL입니다.|
|**total_execution_time**|**int**|시작 시간의 총 실행 시간 (분) (null 허용 안 함)|
|**percent_complete**|**실제로**|인덱스 작업 진행률이% (null을 허용 하지 않음)에 완료 되었습니다.|
|**page_count**|**bigint**|새 인덱스 및 매핑 인덱스에 대 한 인덱스 작성 작업에 의해 할당 된 인덱스 페이지의 총 수입니다 (null 허용 안 함).

## <a name="permissions"></a>사용 권한

[!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  

## <a name="example"></a>예제

 일시 중지 상태의 다시 시작 가능한 인덱스 생성 또는 다시 작성 작업을 모두 나열 합니다.

```sql
SELECT * FROM  sys.index_resumable_operations WHERE STATE = 1;  
```

## <a name="see-also"></a>참고 항목

- [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)
- [CREATE  INDEX](../../t-sql/statements/create-index-transact-sql.md)
- [카탈로그 뷰](catalog-views-transact-sql.md)
- [개체 카탈로그 뷰](object-catalog-views-transact-sql.md)
- [sys.indexes](sys-xml-indexes-transact-sql.md)
- [sys.index_columns](sys-index-columns-transact-sql.md)
- [sys.xml_indexes](sys-xml-indexes-transact-sql.md)
- [sys.objects](sys-index-columns-transact-sql.md)
- [sys.key_constraints](sys-key-constraints-transact-sql.md)
- [sys.filegroups](sys-filegroups-transact-sql.md)
- [sys.partition_schemes](sys-partition-schemes-transact-sql.md)
- [SQL Server 시스템 카탈로그 쿼리에 대한 질문과 대답](querying-the-sql-server-system-catalog-faq.md)
