---
title: sys.dm_os_cluster_nodes (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_os_cluster_nodes_TSQL
- dm_os_cluster_nodes_TSQL
- dm_os_cluster_nodes
- sys.dm_os_cluster_nodes
dev_langs: TSQL
helpviewer_keywords: sys.dm_os_cluster_nodes dynamic management view
ms.assetid: 92fa804e-2d08-42c6-a36f-9791544b1d42
caps.latest.revision: "36"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 72e71c2b008116fe352fbf3c827ac638077eae61
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmosclusternodes-transact-sql"></a>sys.dm_os_cluster_nodes(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  장애 조치(failover) 클러스터 인스턴스 구성에 있는 각 노드에 대해 행을 하나씩 반환합니다. 현재 인스턴스가 장애 조치(failover) 클러스터형 인스턴스인 경우에는 이 장애 조치(failover) 클러스터 인스턴스(이전의 "가상 서버"에 해당)가 정의된 노드의 목록을 반환합니다. 현재 서버 인스턴스가 장애 조치(failover) 클러스터형 인스턴스가 아닌 경우에는 빈 행 집합을 반환합니다.  
  
> **참고:** 로 표현에서 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_os_cluster_nodes**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**NodeName**|**sysname**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스(가상 서버) 구성에 있는 노드의 이름입니다.|  
|상태|**int**|에 있는 노드의 상태는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치 클러스터 인스턴스의: 0, 1, 2, 3,-1입니다. 자세한 내용은 참조 [GetClusterNodeState 함수](http://go.microsoft.com/fwlink/?LinkId=204794)합니다.|  
|status_description|**nvarchar (20)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 노드의 상태에 대한 설명입니다.<br /><br /> 0 = 가동 중<br /><br /> 1 = 중지됨<br /><br /> 2 = 일시 중지됨<br /><br /> 3 = 조인 중<br /><br /> -1 = 알 수 없음|  
|is_current_owner|bit|1은 이 노드가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 리소스의 현재 소유자임을 의미합니다.|  
|pdw_node_id|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="remarks"></a>주의  
 장애 조치(failover) 클러스터링을 사용하도록 설정된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스(가상 서버) 구성의 일부로 지정된 모든 장애 조치(failover) 클러스터 노드에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 실행할 수 있습니다.  
  
> **참고:** 이 보기에는 이후 릴리스에서 중단 될 예정 않는 fn_virtualservernodes 함수를 대체 합니다.  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 sys. dm_os_cluster_nodes를 사용하여 클러스터형 서버 인스턴스의 노드를 반환합니다.  
  
```  
SELECT NodeName, status, status_description, is_current_owner   
FROM sys.dm_os_cluster_nodes;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|NodeName|상태|status_description|is_current_owner|  
|--------------|------------|-------------------------|------------------------|  
|node1|0|up|1.|  
|node2|0|up|0|  
|Node3|1.|down|0|  
  
## <a name="see-also"></a>관련 항목:  
 [sys.dm_os_cluster_properties &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-properties-transact-sql.md)   
 [sys.dm_io_cluster_shared_drives &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md)   
 [sys.fn_virtualservernodes &#40; Transact SQL &#41;](../../relational-databases/system-functions/sys-fn-virtualservernodes-transact-sql.md)   
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  



