---
title: sys.dm_pdw_hadoop_operations (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5d2337d4-e2c7-48de-9c26-cdc7e6eb5d55
caps.latest.revision: 5
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 7c7da3f36c73a2b724c3b6709983d5c3ae611ce4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmpdwhadoopoperations-transact-sql"></a>sys.dm_pdw_hadoop_operations (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Hadoop에 푸시 다운할 실행의 일환으로 각 맵 감소 작업에 대 한 행을 포함 한 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 외부 Hadoop 테이블에 대 한 쿼리 합니다. 맵 감소 작업 각 쿼리에 조건부 중 하나를 나타냅니다. Hadoop 외부 테이블에 대 한 쿼리 조건자 푸시 다운을 사용할 때만 사용 됩니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|이 외부 Hadoop 작업의 ID입니다.|에 ID로 동일한 [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)합니다.|  
|step_index|**int**|이 Hadoop 작업을 참조 하는 쿼리 단계의 인덱스입니다.|step_index 동일 [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)합니다.|  
|operation_type|**nvarchar(255)**|외부 작업 유형을 설명합니다.|' 외부 Hadoop 작업 '|  
|operation_name|**nvarchar(4000)**|맵 감소 작업에 대 한 작업 ID입니다. Hadoop 후이 값이 반환 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 작업을 제출 합니다.||  
|map_progress|**float**|맵 작업에 의해 지금까지 소비 된 입력된 데이터의 비율입니다.|부동 소수점 숫자 0에서 100 포함 하 여, 사이입니다.|  
|reduce_progress|**int**|완료 된 reduce 작업의 백분율...|부동 소수점 숫자 0에서 100 포함 하 여, 사이입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 뷰 &#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
