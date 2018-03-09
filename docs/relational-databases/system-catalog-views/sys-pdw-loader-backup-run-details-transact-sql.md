---
title: sys.pdw_loader_backup_run_details (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 04fc004f-ee15-4d7a-be08-78357aa99b55
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 02b934db7152723e66aab5818751cb748d2e2a87
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="syspdwloaderbackuprundetails-transact-sql"></a>sys.pdw_loader_backup_run_details (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  정보 외의 자세한 정보를 포함 [sys.pdw_loader_backup_runs &#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md), 진행 중인 시간 및 완료 된 백업 및 복원 작업에 대 한 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 지속적인 시간 및 완료 된 백업, 복원 및 로드 작업에서 하는 방법에 대 한 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다. 정보는 시스템을 다시 시작 유지합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|특정 백업 또는 복원을 실행에 대 한 고유 식별자입니다.<br /><br /> run_id 및 pdw_node_id이이 보기에 대 한 키를 형성합니다.||  
|pdw_node_id|**int**|이 레코드 세부 정보를 포함 하는 어플라이언스 노드의 고유 식별자입니다.<br /><br /> run_id 및 pdw_node_id이이 보기에 대 한 키를 형성합니다.|에 대 한 node_id를 참조 하십시오. [sys.dm_pdw_nodes &#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|상태|**nvarchar(16)**|실행의 현재 상태입니다.|'취소', ' 완료 ', '실패', '대기', '실행 중|  
|start_time|**datetime**|이 특정 노드에서 작업을 시작 된 시간입니다.||  
|end_time|**datetime**|작업 종료 된 시간을이 특정 노드에 있는 경우.||  
|total_elapsed_time|**int**|이 특정 노드에서 작업을 실행 하는 총 시간입니다.|Total_elapsed_time 정수 (밀리초에서 24.8 일)에 대 한 최대값을 초과 하면 오버플로 materialization 오류로 인해 발생 합니다.<br /><br /> 밀리초의 최대값 24.8 일 하는 것과 같습니다.|  
|진행 중|**int**|백분율로 표현 된 작업의 진행률입니다.|0에서 100|  
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
