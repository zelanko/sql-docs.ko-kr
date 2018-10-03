---
title: sys.pdw_loader_backup_run_details (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 04fc004f-ee15-4d7a-be08-78357aa99b55
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 76c6b3030ba8701e5d5bb1753a09b1390a713e07
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727972"
---
# <a name="syspdwloaderbackuprundetails-transact-sql"></a>sys.pdw_loader_backup_run_details (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  정보 외의 자세한 정보를 포함 [sys.pdw_loader_backup_runs &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md), 진행 중인 및 완료 된 백업 및 복원 작업에 대 한 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 지속적인 백업, 복원 및 로드 작업에서 완료 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다. 이 정보는 시스템을 다시 시작해도 유지됩니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|특정 백업 또는 복원을 실행에 대 한 고유 식별자입니다.<br /><br /> run_id 및 pdw_node_id이이 보기에 대 한 키를 구성합니다.||  
|pdw_node_id|**int**|이 레코드는에 대 한 세부 정보를 포함 하는 어플라이언스 노드의 고유 식별자입니다.<br /><br /> run_id 및 pdw_node_id이이 보기에 대 한 키를 구성합니다.|에 대 한 node_id를 참조 하세요 [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)합니다.|  
|상태|**nvarchar(16)**|실행의 현재 상태입니다.|'취소'를 ' 완료 ', '실패', '큐 대기', 'RUNNING'|  
|start_time|**datetime**|이 특정 노드에서 작업을 시작 하는 시간입니다.||  
|end_time|**datetime**|작업 종료 된 시간을이 특정 노드에 있는 경우.||  
|total_elapsed_time|**int**|이 특정 노드에서 작업을 실행 하는 총 시간입니다.|Total_elapsed_time 정수 (밀리초 단위로 24.8 일)에 대 한 최대값을 초과 하는 경우 materialization 오류로 인해 오버플로를 발생 합니다.<br /><br /> 시간 (밀리초)의 최 댓 값 24.8 일 하는 것과 같습니다.|  
|진행률|**int**|백분율로 표시 된 작업의 진행률입니다.|0에서 100 사이의|  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
