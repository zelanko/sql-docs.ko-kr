---
title: sys. dm_io_cluster_shared_drives (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_io_cluster_shared_drives_TSQL
- sys.dm_io_cluster_shared_drives
- dm_io_cluster_shared_drives_TSQL
- dm_io_cluster_shared_drives
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_io_cluster_shared_drives dynamic management view
ms.assetid: c8fcced8-c780-49dc-99bd-6beb3ca532c4
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e89252effd6e8fbb14d800837328c9ff8042e0d3
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827951"
---
# <a name="sysdm_io_cluster_shared_drives-transact-sql"></a>sys.dm_io_cluster_shared_drives(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  이 뷰에서는 현재 서버 인스턴스가 클러스터형 서버인 경우 각 공유 드라이브의 이름을 반환합니다. 현재 서버 인스턴스가 클러스터형 인스턴스가 아닌 경우 빈 행 집합을 반환합니다.  
  
> [!NOTE]  
>  에서이를 호출 하려면 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 이름 **sys. dm_pdw_nodes_io_cluster_shared_drives**를 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**DriveName**|**nchar(2)**|클러스터 공유 디스크 배열에 속한 개별 디스크를 나타내는 드라이브 이름(드라이브 문자)입니다. 열은 Null을 허용하지 않습니다.|  
|**pdw_node_id**|**int**|**적용 대상**: sspdw<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="remarks"></a>설명  
 클러스터를 활성화한 경우 인스턴스가 다른 노드로 장애 조치(Failover)된 후 공유 디스크에 액세스할 수 있도록 하려면 장애 조치 클러스터 인스턴스에는 공유 디스크에 상주할 데이터 및 로그 파일이 필요합니다. 이 뷰의 각 행은 이 클러스터형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 사용하는 단일 공유 디스크를 나타냅니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 데이터 또는 로그 파일은 이 뷰에 나열된 디스크에만 저장할 수 있습니다. 이 뷰에 나열된 디스크는 인스턴스와 연관된 클러스터 리소스 그룹에 있는 디스크입니다.  
  
> [!NOTE]  
>  이 뷰는 이후 릴리스에서 더 이상 사용되지 않습니다. 대신 [dm_io_cluster_valid_path_names &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql.md) 를 사용 하는 것이 좋습니다.  
  
## <a name="permissions"></a>권한  
 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 VIEW SERVER STATE 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 sys.dm_io_cluster_shared_drives를 사용하여 클러스터형 서버 인스턴스의 공유 드라이브를 결정합니다.  
  
```  
SELECT * FROM sys.dm_io_cluster_shared_drives;  
```  
  
 결과 집합은 다음과 같습니다.  
  
 DriveName  
  
 --------\-  
  
 m  
  
 n  
  
## <a name="see-also"></a>참고 항목  
 [dm_io_cluster_valid_path_names &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql.md)   
 [dm_os_cluster_nodes &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [fn_servershareddrives &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-servershareddrives-transact-sql.md)   
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  
