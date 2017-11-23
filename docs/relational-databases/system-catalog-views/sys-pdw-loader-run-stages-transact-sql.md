---
title: sys.pdw_loader_run_stages (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 255681e9-323c-42c0-a63c-1f05536efdd5
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d209fff76a89f84b67e351864b102ebf8ecbcd5f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwloaderrunstages-transact-sql"></a>sys.pdw_loader_run_stages (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  진행 중인 시간 및 완료 된 로드 작업에 대 한 정보가 들어 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다. 정보는 시스템을 다시 시작 유지합니다.  
  
|||||  
|-|-|-|-|  
|열 이름|데이터 형식|Description|범위|  
|run_id|**int**|실행 하는 로더의 고유 식별자입니다.||  
|stage(단계)|**nvarchar (30)**|실행의 현재 단계입니다.|'CREATE_STAGING', 'DMS_LOAD', 'LOAD_INSERT', 'LOAD_CLEANUP'|  
|request_id|**nvarchar (32)**|이 단계를 실행 하는 요청의 ID입니다.||  
|상태|**nvarchar(16)**|이 단계의 상태입니다.||  
|start_time|**datetime**|스테이지 시작 된 시간입니다.||  
|end_time|**datetime**|있는 경우 스테이지 종료 된 시간입니다.|시작 되지 않은 경우 또는 진행 중 NULL입니다.|  
|total_elapsed_time|**int**|실행 하는 데 걸린 (또는 지금까지 소요)이이 단계 총 시간입니다.|Total_elapsed_time 정수 (밀리초에서 24.8 일)에 대 한 최대값을 초과 하면 오버플로 materialization 오류로 인해 발생 합니다.<br /><br /> 밀리초의 최대값 24.8 일 하는 것과 같습니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
