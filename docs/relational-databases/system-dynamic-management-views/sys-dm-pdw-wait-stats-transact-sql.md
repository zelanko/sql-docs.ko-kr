---
description: sys.dm_pdw_wait_stats (Transact-sql)
title: sys.dm_pdw_wait_stats (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cfb8d905-c34f-44de-9574-dde81e170916
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: 417b5f5d88d5a150653e6910eabb8f7692657b2c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461574"
---
# <a name="sysdm_pdw_wait_stats-transact-sql"></a>sys.dm_pdw_wait_stats (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]서로 다른 노드에서 실행 되는 인스턴스와 관련 된 OS 상태와 관련 된 정보를 보유 합니다. 대기 유형 목록과 해당 설명에 대 한 자세한 내용은 [sys.dm_os_wait_stats](https://msdn.microsoft.com/library/ms179984\(v=sql.120\).aspx)를 참조 하세요.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|**pdw_node_id**|**int**|이 항목이 참조 하는 노드의 ID입니다.||  
|**wait_name**|**nvarchar(255)**|대기 유형의 이름입니다.||  
|**max_wait_time**|**bigint**|이 대기 유형의 최대 대기 시간입니다.||  
|**request_count**|**bigint**|처리 중인이 대기 유형의 대기 수입니다.||  
|**signal_time**|**bigint**|대기 스레드가 신호를 받은 시간과 실행을 시작한 시간 사이의 차이입니다.||  
|**completed_count**|**bigint**|마지막 서버가 다시 시작 된 이후에 완료 된이 유형의 총 대기 수입니다.||  
|**wait_time**|**bigint**|Millisecons에서이 대기 유형의 총 대기 시간입니다. Signal_time 포함||  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;Azure Synapse 분석 및 병렬 데이터 웨어하우스 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [Transact-sql&#41;sys.dm_pdw_waits &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
  
