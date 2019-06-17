---
title: sys.dm_pdw_hadoop_operations (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5d2337d4-e2c7-48de-9c26-cdc7e6eb5d55
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 11c8cc0797bafff6cc8c38bffb55023be00003a9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62690429"
---
# <a name="sysdmpdwhadoopoperations-transact-sql"></a>sys.dm_pdw_hadoop_operations (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  각 맵 감소 작업 실행의 일부로 Hadoop에 푸시되는 대 한 행을 포함 한 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 외부 Hadoop 테이블에 대 한 쿼리 합니다. 각 맵 감소 작업을 쿼리에서 조건부 중 하나를 나타냅니다. 이 Hadoop 외부 테이블에 대 한 쿼리 조건자 푸시 다운이 활성화 될 때만 사용 됩니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|이 외부 Hadoop 작업의 ID입니다.|ID로 동일한 [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)합니다.|  
|step_index|**int**|이 Hadoop 작업을 나타내는 쿼리 단계의 인덱스입니다.|step_index 동일 [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)합니다.|  
|operation_type|**nvarchar(255)**|외부 작업의 유형을 설명합니다.|' 외부 Hadoop 작업 '|  
|operation_name|**nvarchar(4000)**|맵 감소 작업에 대 한 작업 ID입니다. 후 Hadoop이 반환한 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 작업을 제출 합니다.||  
|map_progress|**float**|맵 작업에 의해 지금까지 사용 된 입력된 데이터의 비율입니다.|부동 소수점 수 between 및 0과 100 포함 합니다.|  
|reduce_progress|**int**|완료 된 감소 작업의 백분율...|부동 소수점 수 between 및 0과 100 포함 합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [시스템 뷰 &#40;TRANSACT-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
