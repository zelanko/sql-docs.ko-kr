---
title: sys.pdw_nodes_tables (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 473b5d14-171b-4a16-9195-acf36d3f786c
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 79ab5f34c5d079076d3c54bffa201e03f48ac7ad
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="syspdwnodestables-transact-sql"></a>sys.pdw_nodes_tables (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  에 주 서버에 일부 권한이 부여 또는 보안 주체를 소유 하는 각 테이블 개체에 대 한 행을 포함 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|\<열을 상속 >||이 뷰가 상속 하는 열 목록은 참조 [sys.objects](http://msdn.microsoft.com/en-us/c36fa71e-549a-4533-a6cd-1314d26f533f)합니다.||  
|lob_data_space_id|**int**||항상 0입니다.|  
|filestream_data_space_id|**int**|FILESTREAM 파일 그룹에 대 한 데이터 공간 ID 또는 [!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|NULL|  
|max_column_id_used|**int**|이 테이블에서 사용 되는 최대 열 ID입니다.||  
|lock_on_bulk_load|**bit**|대량 로드 시 테이블이 잠깁니다.|TBD|  
|uses_ansi_nulls|**bit**|테이블이 SET ANSI_NULLS 데이터베이스 옵션을 ON으로 설정하여 생성되었습니다.|1.|  
|is_replicated|**bit**|1 = 테이블이 복제를 사용 하 여 게시 합니다.|0; 복제는 지원 되지 않습니다.|  
|has_replication_filter|**bit**|1 = 테이블에 복제 필터가 있습니다.|0|  
|is_merge_published|**bit**|1 = 테이블이 병합 복제를 사용하여 게시됩니다.|0; 지원 되지 않습니다.|  
|is_sync_tran_subscribed|**bit**|1 = 테이블이 즉시 업데이트 구독을 사용하여 구독됩니다.|0; 지원 되지 않습니다.|  
|has_unchecked_assembly_data|**bit**|1 = 테이블은 마지막 ALTER ASSEMBLY를 수행하는 동안 정의가 변경된 어셈블리에 종속되어 있는 데이터를 포함합니다. 다음 번 DBCC CHECKDB 또는 DBCC CHECKTABLE이 성공적으로 수행된 후에 다시 0으로 설정됩니다.|0; CLR 지원 되지 않습니다.|  
|text_in_row_limit|**int**|0 = text in row 옵션이 설정되지 않았습니다.|항상 0입니다.|  
|large_value_types_out_of_row|**bit**|1 = 큰 값 유형은 행 밖에 저장됩니다.|항상 0입니다.|  
|is_tracked_by_cdc|**bit**|1 = 테이블에 변경 데이터 캡처 설정|항상 0; CDC 지원 되지 않습니다.|  
|lock_escalation|**tinyint**|테이블에 대 한 LOCK_ESCALATION 옵션의 값: 2 = 자동|항상 2입니다.|  
|lock_escalation_desc|**nvarchar(60)**|Lock_escalation 옵션의 텍스트 설명입니다.|항상 ꞌAUTOꞌ 합니다.|  
|pdw_node_id|**int**|고유 식별자는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 노드.|NOT NULL|  
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
