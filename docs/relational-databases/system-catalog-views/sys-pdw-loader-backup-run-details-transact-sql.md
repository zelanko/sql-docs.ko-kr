---
description: sys.pdw_loader_backup_run_details (Transact-sql)
title: sys.pdw_loader_backup_run_details (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 04fc004f-ee15-4d7a-be08-78357aa99b55
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 243bbff033bfa3b9327227da6fdbf200d28e1ee5
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92034813"
---
# <a name="syspdw_loader_backup_run_details-transact-sql"></a>sys.pdw_loader_backup_run_details (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  에는 [sys.pdw_loader_backup_runs &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)정보 뿐만 아니라에서 진행 중 이며 완료 된 백업 및 복원 작업과 진행 중 이며 완료 된 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 백업, 복원 및 로드 작업에 대 한 정보를 설명 합니다 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] . 이 정보는 시스템을 다시 시작해도 유지됩니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|특정 백업 또는 복원 실행에 대 한 고유 식별자입니다.<br /><br /> run_id 및 pdw_node_id이 보기의 키를 구성 합니다.||  
|pdw_node_id|**int**|이 레코드가 세부 정보를 보유 하는 어플라이언스 노드의 고유 식별자입니다.<br /><br /> run_id 및 pdw_node_id이 보기의 키를 구성 합니다.|[Sys.dm_pdw_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)에서 node_id를 참조 하세요.|  
|상태|**nvarchar (16)**|실행의 현재 상태입니다.|' 취소 됨 ', ' 완료 됨 ', ' 실패 ', ' 대기 중 ', ' 실행 중 '|  
|start_time|**datetime**|이 특정 노드에서 작업이 시작 된 시간입니다.||  
|end_time|**datetime**|이 특정 노드에서 작업이 끝난 시간입니다 (있는 경우).||  
|total_elapsed_time|**int**|이 특정 노드에서 작업이 실행 된 총 시간입니다.|Total_elapsed_time 정수 24.8 (밀리초)의 최대값을 초과 하는 경우 오버플로로 인 한 구체화 실패가 발생 합니다.<br /><br /> 최대 값 (밀리초)은 24.8 일에 해당 합니다.|  
|progress|**int**|비율로 표시 되는 작업의 진행률입니다.|0~100|  
  
## <a name="see-also"></a>참고 항목  
 [Azure Synapse Analytics 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
