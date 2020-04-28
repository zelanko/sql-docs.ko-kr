---
title: sys. pdw_loader_run_stages (Transact-sql) | Microsoft Docs
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
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5d10a3bcbf02e88e054c12060299e9462af3004d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68127449"
---
# <a name="syspdw_loader_run_stages-transact-sql"></a>sys. pdw_loader_run_stages (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  에서 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]진행 중인 로드 작업과 완료 된 로드 작업에 대 한 정보를 포함 합니다. 이 정보는 시스템을 다시 시작해도 유지됩니다.  
  
|||||  
|-|-|-|-|  
|열 이름|데이터 형식|설명|범위|  
|run_id|**int**|로더 실행의 고유 식별자입니다.||  
|stage(단계)|**nvarchar(30)**|실행에 대 한 현재 단계입니다.|' CREATE_STAGING ', ' DMS_LOAD ', ' LOAD_INSERT ', ' LOAD_CLEANUP '|  
|request_id|**nvarchar(32)**|이 단계를 실행 하는 요청의 ID입니다.||  
|상태|**nvarchar (16)**|이 단계의 상태입니다.||  
|start_time|**datetime**|단계가 시작 된 시간입니다.||  
|end_time|**datetime**|단계가 끝난 시간 (있는 경우)입니다.|시작 되지 않았거나 진행 중인 경우 NULL입니다.|  
|total_elapsed_time|**int**|이 단계를 실행 하는 데 걸린 총 시간입니다.|Total_elapsed_time 정수 24.8 (밀리초)의 최대값을 초과 하는 경우 오버플로로 인 한 구체화 실패가 발생 합니다.<br /><br /> 최대 값 (밀리초)은 24.8 일에 해당 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Data Warehouse 및 병렬 Data Warehouse 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
