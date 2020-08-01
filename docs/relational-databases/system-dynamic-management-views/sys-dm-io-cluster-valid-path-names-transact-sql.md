---
title: sys. dm_io_cluster_valid_path_names (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_io_cluster_valid_path_names
- dm_io_cluster_valid_path_names_TSQL
- sys.dm_io_cluster_valid_path_names_TSQL
- dm_io_cluster_valid_path_names
dev_langs:
- TSQL
helpviewer_keywords:
- dm_io_cluster_valid_path_names
- sys.dm_io_cluster_valid_path_names
- cluster valid path names
- csv name
- cluster shared volume names
ms.assetid: 5bc8a0e5-6c72-425b-8c58-f276eb9add2c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a47313e1fb9a97207f02abcc89bdb66bb791f9ea
ms.sourcegitcommit: 039fb38c583019b3fd06894160568387a19ba04e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2020
ms.locfileid: "87442542"
---
# <a name="sysdm_io_cluster_valid_path_names-transact-sql"></a>sys.dm_io_cluster_valid_path_names(Transact-SQL)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  클러스터된 공유 볼륨을 비롯한 모든 유효한 공유 디스크에서 SQL Server 장애 조치(failover) 클러스터 인스턴스에 대한 정보를 반환합니다. 인스턴스가 클러스터되지 않은 경우 빈 행 집합이 반환됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**path_name**|**Nvarchar (512)**|데이터베이스 및 로그 파일의 루트 디렉터리로 사용할 수 있는 볼륨 탑재 지점 또는 드라이브 경로입니다. Null을 허용하지 않습니다.|  
|**cluster_owner_node**|**Nvarchar (64)**|드라이브의 현재 소유자입니다. CSV(클러스터 공유 볼륨)의 경우 소유자는 메타데이터 서버를 호스팅하는 노드입니다. Null을 허용하지 않습니다.|  
|**is_cluster_shared_volume**|**조금**|이 경로가 위치한 드라이브가 클러스터 공유 볼륨이면 1을 반환하고, 그렇지 않으면 0을 반환합니다.|  
  
## <a name="remarks"></a>설명  
 SQL Server FCI(장애 조치(failover) 클러스터 인스턴스)는 데이터 및 로그 파일 저장을 위해 FCI의 모든 노드 간에 공유 스토리지를 사용해야 합니다. 이 뷰에 나열된 디스크는 인스턴스와 연결된 클러스터 리소스 그룹에 있는 디스크이며 데이터 또는 로그 파일 스토리지에 사용할 수 있는 유일한 디스크입니다.  
  
> [!NOTE]  
>  이 뷰는 이후 릴리스에서 [dm_io_cluster_shared_drives &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md) 를 대체 합니다.  
  
## <a name="permissions"></a>사용 권한  
 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 VIEW SERVER STATE 권한이 있어야 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 sys.dm_io_cluster_valid_path_names를 사용하여 클러스터형 서버 인스턴스의 공유 드라이브를 결정합니다.  
  
```  
SELECT * FROM sys.dm_io_cluster_valid_path_names;  
```  
  
## <a name="see-also"></a>참고 항목  
 [dm_os_cluster_nodes &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [dm_io_cluster_shared_drives &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md)   
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

