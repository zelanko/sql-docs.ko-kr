---
title: sys.dm_os_server_diagnostics_log_configurations | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_os_server_diagnostics_log_configurations
- sys.dm_os_server_diagnostics_log_configurations_TSQL
- dm_os_server_diagnostics_log_configurations
- dm_os_server_diagnostics_log_configurations_TSQL
dev_langs: TSQL
helpviewer_keywords:
- dm_os_server_diagnostics_log_configurations
- sys.dm_os_server_diagnostics_log_configurations
ms.assetid: c09ea433-d283-4f83-af69-d458aad59217
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 606ce60f28af040ba6508725c6c7a4adb6378083
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmosserverdiagnosticslogconfigurations"></a>sys.dm_os_server_diagnostics_log_configurations
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 진단 로그의 현재 구성을 포함하는 하나의 행을 반환합니다. 이러한 속성 설정에 따라 진단 로깅 설정 여부, 로그 파일의 위치, 수 및 크기가 결정됩니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|is_enabled|**bit**|로깅 설정 여부를 나타냅니다.<br /><br /> 1 = 진단 로깅이 설정됩니다.<br /><br /> 0 = 진단 로깅이 해제됩니다.|  
|max_size|**int**|각 진단 로그가 증가할 수 있는 최대 크기(MB)입니다. 기본값은 100  MB입니다.|  
|max_files|**int**|새 진단 로그에 재활용하기 전에 컴퓨터에 저장할 수 있는 최대 진단 로그 파일 수입니다.|  
|path|**nvarchar (260)**|진단 로그의 위치를 나타내는 경로입니다. 기본 위치는 \<\MSSQL\Log >의 설치 폴더 내에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치 클러스터 인스턴스의 합니다.|  
  
## <a name="permissions"></a>Permissions  
 SQL Server 장애 조치(failover) 클러스터 인스턴스에 대한 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 sys.dm_os_server_diagnostics_log_configurations를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 진단 로그에 대한 속성 설정을 반환합니다.  
  
```  
SELECT <list of columns>  
FROM sys.dm_os_server_diagnostics_log_configurations;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|IS_ENABLED|PATH|MAX_SIZE|MAX_FILES|  
|-----------------|----------|---------------|----------------|  
|1.|\<C:\Program Files\Microsoft SQL Server\MSSQL13\MSSQL\Log >|10|10|  
  
## <a name="see-also"></a>관련 항목:  
 [장애 조치(failover) 클러스터 인스턴스 진단 로그 보기 및 읽기](../../sql-server/failover-clusters/windows/view-and-read-failover-cluster-instance-diagnostics-log.md)  
  
  
