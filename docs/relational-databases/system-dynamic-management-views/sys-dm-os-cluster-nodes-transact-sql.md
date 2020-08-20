---
description: sys.dm_os_cluster_nodes(Transact-SQL)
title: sys. dm_os_cluster_nodes (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_cluster_nodes_TSQL
- dm_os_cluster_nodes_TSQL
- dm_os_cluster_nodes
- sys.dm_os_cluster_nodes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_cluster_nodes dynamic management view
ms.assetid: 92fa804e-2d08-42c6-a36f-9791544b1d42
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c5ee6538ed70c73177f5cd23b14739df48fd2af8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481918"
---
# <a name="sysdm_os_cluster_nodes-transact-sql"></a>sys.dm_os_cluster_nodes(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  장애 조치(failover) 클러스터 인스턴스 구성에 있는 각 노드에 대해 행을 하나씩 반환합니다. 현재 인스턴스가 장애 조치(failover) 클러스터형 인스턴스인 경우에는 이 장애 조치(failover) 클러스터 인스턴스(이전의 "가상 서버"에 해당)가 정의된 노드의 목록을 반환합니다. 현재 서버 인스턴스가 장애 조치(failover) 클러스터형 인스턴스가 아닌 경우에는 빈 행 집합을 반환합니다.  
  
> **참고:** 또는에서이를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 이름 **sys. dm_pdw_nodes_os_cluster_nodes**을 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**NodeName**|**sysname**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스(가상 서버) 구성에 있는 노드의 이름입니다.|  
|상태|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]장애 조치 (failover) 클러스터 인스턴스의 노드 상태: 0, 1, 2, 3,-1. 자세한 내용은 [Getclusternodestate 함수](https://go.microsoft.com/fwlink/?LinkId=204794)를 참조 하세요.|  
|status_description|**nvarchar (20)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 노드의 상태에 대한 설명입니다.<br /><br /> 0 = 가동 중<br /><br /> 1 = 중지됨<br /><br /> 2 = 일시 중지됨<br /><br /> 3 = 조인 중<br /><br /> -1 = 알 수 없음|  
|is_current_owner|bit|1은 이 노드가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 리소스의 현재 소유자임을 의미합니다.|  
|pdw_node_id|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="remarks"></a>설명  
 장애 조치(failover) 클러스터링을 사용하도록 설정된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스(가상 서버) 구성의 일부로 지정된 모든 장애 조치(failover) 클러스터 노드에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 실행할 수 있습니다.  
  
> **참고:** 이 뷰는 이후 릴리스에서 더 이상 사용 되지 않을 fn_virtualservernodes 함수를 대체 합니다.  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 sys. dm_os_cluster_nodes를 사용하여 클러스터형 서버 인스턴스의 노드를 반환합니다.  
  
```  
SELECT NodeName, status, status_description, is_current_owner   
FROM sys.dm_os_cluster_nodes;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|NodeName|상태|status_description|is_current_owner|  
|--------------|------------|-------------------------|------------------------|  
|node1|0|up|1|  
|node2|0|up|0|  
|Node3|1|료|0|  
  
## <a name="see-also"></a>참고 항목  
 [dm_os_cluster_properties &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-properties-transact-sql.md)   
 [dm_io_cluster_shared_drives &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md)   
 [fn_virtualservernodes &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-virtualservernodes-transact-sql.md)   
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  



