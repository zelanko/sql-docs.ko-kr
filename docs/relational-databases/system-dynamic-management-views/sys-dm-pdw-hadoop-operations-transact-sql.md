---
description: sys.dm_pdw_hadoop_operations (Transact-sql)
title: sys.dm_pdw_hadoop_operations (Transact-sql) | Microsoft Docs
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
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: 25c2e732fea0b92866f233a51a69103028245418
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472804"
---
# <a name="sysdm_pdw_hadoop_operations-transact-sql"></a>sys.dm_pdw_hadoop_operations (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  외부 Hadoop 테이블에서 쿼리를 실행 하는 과정의 일부로 Hadoop에 푸시되는 각 지도 감소 작업에 대 한 행을 포함 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 합니다. 각 맵 감소 작업은 쿼리의 조건자 중 하나를 나타냅니다. 이는 Hadoop 외부 테이블에 대 한 쿼리에 조건자 푸시 다운을 사용 하는 경우에만 사용 됩니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|이 외부 Hadoop 작업의 ID입니다.|[Transact-sql&#41;&#40;SYS.DM_PDW_EXEC_REQUESTS ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)ID와 동일 합니다.|  
|step_index|**int**|이 Hadoop 작업을 참조 하는 쿼리 단계의 인덱스입니다.|[Transact-sql&#41;&#40;sys.dm_pdw_request_steps ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)step_index와 동일 합니다.|  
|operation_type|**nvarchar(255)**|외부 작업의 유형을 설명 합니다.|' 외부 Hadoop 작업 '|  
|operation_name|**nvarchar(4000)**|지도 감소 작업의 작업 ID입니다. 이는 작업을 제출한 후 Hadoop에서 반환 됩니다 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] .||  
|map_progress|**float**|현재까지 맵 작업에서 사용한 입력 데이터의 백분율입니다.|0과 100를 포함 하는의 부동 소수점 숫자입니다.|  
|reduce_progress|**int**|완료 된 작업 감소의 백분율입니다.|0과 100를 포함 하는의 부동 소수점 숫자입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 뷰 ](../../t-sql/language-reference.md)  
  
