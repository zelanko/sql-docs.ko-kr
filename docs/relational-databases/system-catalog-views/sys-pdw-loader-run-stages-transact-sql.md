---
title: sys.pdw_loader_run_stages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 255681e9-323c-42c0-a63c-1f05536efdd5
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ed0721ada78b3aa70741510818c5e312b3bd4d55
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56012635"
---
# <a name="syspdwloaderrunstages-transact-sql"></a>sys.pdw_loader_run_stages (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  진행 중인 및 완료 된 로드 작업에 대 한 정보가 들어 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다. 이 정보는 시스템을 다시 시작해도 유지됩니다.  
  
|||||  
|-|-|-|-|  
|열 이름|데이터 형식|Description|범위|  
|run_id|**int**|실행 하는 로더의 고유 식별자입니다.||  
|stage(단계)|**nvarchar(30)**|실행에 대 한 현재 단계입니다.|'CREATE_STAGING', 'DMS_LOAD', 'LOAD_INSERT', 'LOAD_CLEANUP'|  
|request_id|**nvarchar(32)**|이 단계를 실행 하는 요청의 ID입니다.||  
|상태|**nvarchar(16)**|이 단계는 상태입니다.||  
|start_time|**datetime**|스테이지를 시작한 시간입니다.||  
|end_time|**datetime**|있는 경우 단계 종료 된 시간입니다.|시작 되지 않은 경우 또는 진행에서 NULL입니다.|  
|total_elapsed_time|**int**|총 시간 소요 된 (또는 지금까지 소요)이이 단계를 실행 합니다.|Total_elapsed_time 정수 (밀리초 단위로 24.8 일)에 대 한 최대값을 초과 하는 경우 materialization 오류로 인해 오버플로를 발생 합니다.<br /><br /> 시간 (밀리초)의 최 댓 값 24.8 일 하는 것과 같습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
