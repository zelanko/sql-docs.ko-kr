---
description: sys. dm_pdw_sys_info (Transact-sql)
title: sys. dm_pdw_sys_info (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 686976b4-2d5d-4d64-bf12-56eba1dc59b1
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 0222938fe9e7b40b3982695e8e2bb47e86a2f078
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88397729"
---
# <a name="sysdm_pdw_sys_info-transact-sql"></a>sys. dm_pdw_sys_info (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  기기의 전체 작업을 반영 하는 일련의 어플라이언스 수준 카운터를 제공 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|total_sessions|**int**|현재 시스템에 있는 세션 수입니다.|0 max_active_sessions (아래 참조)|  
|idle_sessions|**int**|현재 유휴 상태인 세션 수입니다.||  
|active_requests|**int**|현재 실행 중인 활성 요청 수입니다.||  
|queued_requests|**int**|현재 큐에 대기 중인 요청 수입니다.||  
|active_loads|**int**|시스템에서 현재 실행 중인 부하의 수입니다.||  
|queued_loads|**int**|실행 대기 중인 지연 로드 수입니다.||  
|active_backups|**int**|현재 실행 중인 백업 수입니다.||  
|active_restores|**int**|현재 실행 중인 백업 복원 수입니다.||  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
