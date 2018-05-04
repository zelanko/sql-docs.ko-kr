---
title: sys.dm_tran_version_store (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_version_store_TSQL
- sys.dm_tran_version_store
- dm_tran_version_store
- dm_tran_version_store_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_version_store dynamic management view
ms.assetid: 7ab44517-0351-4f91-bdd9-7cf940f03c51
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2d543c994c5d5ede69a5ddf347ef15d5a719bf72
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmtranversionstore-transact-sql"></a>sys.dm_tran_version_store(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  버전 저장소의 모든 버전 레코드를 표시하는 가상 테이블을 반환합니다. **sys.dm_tran_version_store** 되었습니다 전체 버전 저장소를 쿼리하며 버전 저장소가 매우 클 수 있으므로 실행할 경우 비효율적입니다.  
  
 각 버전 레코드는 일부 추적/상태 정보와 함께 이진 데이터로 저장됩니다. 데이터베이스 테이블의 레코드와 마찬가지로 버전 저장소 레코드도 8192바이트 페이지로 저장됩니다. 레코드가 8192바이트를 초과하면 두 개의 레코드로 분할됩니다.  
  
 버전 레코드는 이진 데이터로 저장되므로 각 데이터베이스의 다양한 데이터 정렬로 인한 문제가 발생하지 않습니다. 사용 하 여 **sys.dm_tran_version_store** 버전 저장소에 있는 이진 형태로 행의 이전 버전을 찾을 수 있습니다.  
  
  
## <a name="syntax"></a>구문  
  
```  
sys.dm_tran_version_store  
```  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**transaction_sequence_num**|**bigint**|레코드 버전을 생성하는 트랜잭션 시퀀스 번호입니다.|  
|**version_sequence_num**|**bigint**|버전 레코드 시퀀스 번호입니다. 이 값은 버전 생성 트랜잭션 내에서 고유합니다.|  
|**database_id**|**int**|버전 레코드의 데이터베이스 ID입니다.|  
|**rowset_id**|**bigint**|레코드의 행 집합 ID입니다.|  
|**상태**|**tinyint**|버전이 지정된 레코드가 두 개 레코드로 분할되었는지 여부를 나타냅니다. 값이 0이면 레코드가 한 페이지에 저장됩니다. 값이 1이면 레코드가 두 개 레코드로 분할되어 서로 다른 두 페이지에 저장됩니다.|  
|**min_length_in_bytes**|**smallint**|레코드의 최소 길이(바이트)입니다.|  
|**record_length_first_part_in_bytes**|**smallint**|버전 레코드에서 첫 번째 부분의 길이(바이트)입니다.|  
|**record_image_first_part**|**varbinary(8000)**|버전 레코드에서 첫 번째 부분의 이진 이미지입니다.|  
|**record_length_second_part_in_bytes**|**smallint**|버전 레코드에서 두 번째 부분의 길이(바이트)입니다.|  
|**record_image_second_part**|**varbinary(8000)**|버전 레코드에서 두 번째 부분의 이진 이미지입니다.|  
  
## <a name="permissions"></a>Permissions

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다.   
  
## <a name="examples"></a>예  
 다음 예에서는 ALLOW_SNAPSHOT_ISOLATION 및 READ_COMMITTED_SNAPSHOT 옵션이 ON으로 설정된 데이터베이스에서 각각 XSN(트랜잭션 시퀀스 번호)으로 식별되는 4개의 동시 트랜잭션이 실행되는 테스트 시나리오를 사용합니다. 다음 트랜잭션이 실행되고 있습니다.  
  
-   XSN-57은 직렬화 격리에서 실행되는 UPDATE 작업입니다.  
  
-   XSN-58은 XSN-57과 같습니다.  
  
-   XSN-59는 스냅숏 격리에서 실행되는 SELECT 작업입니다.  
  
-   XSN-60은 XSN-59와 같습니다.  
  
 다음 쿼리가 실행됩니다.  
  
```  
SELECT  
    transaction_sequence_num,  
    version_sequence_num,  
    database_id rowset_id,  
    status,  
    min_length_in_bytes,  
    record_length_first_part_in_bytes,  
    record_image_first_part,  
    record_length_second_part_in_bytes,  
    record_image_second_part  
  FROM sys.dm_tran_version_store;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
transaction_sequence_num version_sequence_num database_id  
------------------------ -------------------- -----------  
57                      1                    9             
57                      2                    9             
57                      3                    9             
58                      1                    9             
  
rowset_id            status min_length_in_bytes  
-------------------- ------ -------------------  
72057594038321152    0      12                   
72057594038321152    0      12                   
72057594038321152    0      12                   
72057594038386688    0      16                   
  
record_length_first_part_in_bytes  
---------------------------------  
29                                 
29                                 
29                                 
33                                 
  
record_image_first_part                                               
--------------------------------------------------------------------  
0x50000C0073000000010000000200FCB000000001000000270000000000          
0x50000C0073000000020000000200FCB000000001000100270000000000          
0x50000C0073000000030000000200FCB000000001000200270000000000          
0x500010000100000002000000030000000300F800000000000000002E0000000000  
  
record_length_second_part_in_bytes record_image_second_part  
---------------------------------- ------------------------  
0                                  NULL  
0                                  NULL  
0                                  NULL  
0                                  NULL  
```  
  
 출력은 XSN-57이 한 테이블에서 행 버전 3개를 만들었으며 XSN-58이 다른 테이블에서 행 버전 하나를 만들었음을 보여 줍니다.  
  
## <a name="see-also"></a>관련 항목:  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [트랜잭션 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
