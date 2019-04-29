---
title: sys.index_resumable_operations (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/14/2019
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 780cffa17f6ee1af70d942545632c98c9d6dc1e7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63004378"
---
# <a name="indexresumableoperations-transact-sql"></a>index_resumable_operations (Transact SQL)

[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]
**sys.index_resumable_operations** 모니터링 하 고 다시 시작 가능한 인덱스 다시 작성에 대 한 현재 실행 상태를 확인 하는 시스템 뷰입니다.  
**적용 대상**: SQL Server 2017 및 Azure SQL Database
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|이 인덱스 (null 허용 안 함) 속한 개체의 ID입니다.|  
|**index_id**|**int**|인덱스의 ID입니다 (null 허용 안 함)입니다. **index_id** 는 개체 내 에서만 고유 합니다.|
|**name**|**sysname**|인덱스의 이름입니다. **이름** 는 개체 내 에서만 고유 합니다.|  
|**sql_text**|**nvarchar(max)**|T-SQL DDL 문 텍스트|
|**last_max_dop**|**smallint**|마지막 MAX_DOP 사용 (기본값 = 0)|
|**partition_number**|**int**|내 소유 하는 인덱스 또는 힙의 파티션 번호입니다. 대/소문자 또는 분할 되지 않은 테이블 및 인덱스에 대 한 모든 파티션을 다시 값이이 열은 NULL 되는 합니다.|
|**state**|**tinyint**|다시 시작 가능한 인덱스에 대 한 작업 상태:<br /><br />0 = 실행 중<br /><br />1=Pause|
|**state_desc**|**nvarchar(60)**|작업 상태 (실행 중 또는 일시 중지) 다시 시작 가능한 인덱스에 대 한 설명|  
|**start_time**|**datetime**|인덱스 작업 시작 시간 (null 허용 안 함)|
|**last_pause_time**|**datatime**| 인덱스 작업 (nullable) 마지막으로 일시 중지 시간입니다. 작업 실행을 일시 중지 된 경우 NULL입니다.|
|**total_execution_time**|**int**|시작 시간 (분) (null 허용 안 함)에서 총 실행 시간|
|**percent_complete**|**real**|% (Null 허용 안 함)에 인덱스 작업의 진행률 완료 합니다.|
|**page_count**|**bigint**|매핑 인덱스 (null 허용 안 함) 새 인덱스 작성 작업을 할당 하는 인덱스 페이지의 총 수입니다.

## <a name="permissions"></a>사용 권한

[!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  

## <a name="example"></a>예제

 일시 중지 상태에 있는 모든 다시 시작 가능한 인덱스 다시 작성 작업을 나열 합니다.

```sql
SELECT * FROM  sys.index_resumable_operations WHERE STATE = 1;  
```

## <a name="see-also"></a>관련 항목

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
- [SQL Server 시스템 카탈로그 쿼리 FAQ](querying-the-sql-server-system-catalog-faq.md)
