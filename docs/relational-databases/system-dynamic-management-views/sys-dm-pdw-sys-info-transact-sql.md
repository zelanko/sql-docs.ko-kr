---
title: sys.dm_pdw_sys_info (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
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
ms.assetid: 686976b4-2d5d-4d64-bf12-56eba1dc59b1
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 750579342ab5a59115fe2aa2dd3d78d151a6f44c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmpdwsysinfo-transact-sql"></a>sys.dm_pdw_sys_info (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  어플라이언스에서 전체 작업을 반영 하는 어플라이언스 수준 카운터 집합을 제공 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|total_sessions|**int**|시스템에서 현재 세션 수입니다.|0 ~ max_active_sessions (아래 참조)입니다.|  
|idle_sessions|**int**|현재 유휴 세션 수입니다.||  
|active_requests|**int**|현재 실행 중인 활성 요청 수입니다.||  
|queued_requests|**int**|현재 대기 중인 요청의 수입니다.||  
|active_loads|**int**|시스템에서 현재 실행 중인 부하의 수입니다.||  
|queued_loads|**int**|실행을 기다리는 대기 로드 수입니다.||  
|active_backups|**int**|현재 실행 중인 백업의 수입니다.||  
|active_restores|**int**|현재 실행 중인 백업 복원의 수입니다.||  
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
