---
title: "가용성 그룹을 오프라인 상태로 만들기(SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Availability Groups [SQL Server], take offline
ms.assetid: 50f5aad8-0dff-45ef-8350-f9596d3db898
caps.latest.revision: "38"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7d62f2509b563f4bfaeb975db4e99a2d540f7705
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="take-an-availability-group-offline-sql-server"></a>가용성 그룹을 오프라인 상태로 만들기(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 항목에서는 [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] 이상 버전에서 [!INCLUDE[tsql](../../../includes/tsql-md.md)]을 사용하여 Always On 가용성 그룹을 ONLINE 상태에서 OFFLINE 상태로 변경하는 방법을 설명합니다. 동기 커밋 복제본이 동기화되지 않을 경우 OFFLINE 작업이 오류를 발생시키고 가용성 그룹을 ONLINE 상태로 유지하기 때문에 동기 커밋 데이터베이스의 데이터는 손실되지 않습니다. 가용성 그룹을 온라인 상태로 유지하면 데이터 손실이 발생하지 않도록 동기화되지 않은 동기화 커밋 데이터베이스가 보호됩니다. 가용성 그룹이 오프라인 상태로 전환된 후에는 클라이언트에서 해당 데이터베이스를 사용할 수 없게 되고 사용자가 가용성 그룹을 다시 온라인 상태로 전환할 수 없습니다. 따라서 WSFC 클러스터 간에 가용성 그룹 리소스를 마이그레이션하려는 경우에만 가용성 그룹을 오프라인으로 전환해야 합니다.  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]의 클러스터 간 마이그레이션 중에 응용 프로그램이 가용성 그룹의 주 복제본에 직접 연결할 경우 가용성 그룹을 오프라인 상태로 전환해야 합니다. [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 의 클러스터 간 마이그레이션은 가용성 그룹의 작동 중단 시간을 최소화하면서 OS 업그레이드를 지원합니다. 일반적으로 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 의 클러스터 간 마이그레이션은 OS를 [!INCLUDE[win8](../../../includes/win8-md.md)] 또는 [!INCLUDE[win8srv](../../../includes/win8srv-md.md)]로 업그레이드하려는 경우에 사용합니다. 자세한 내용은 [OS 업그레이드를 위한 Always On 가용성 그룹의 클러스터 간 마이그레이션](http://msdn.microsoft.com/library/jj873730.aspx)을 참조하세요.  
  
-   **시작하기 전에:**  
  
     [필수 구성 요소](#Prerequisites)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **가용성 그룹을 오프라인 상태로 전환하는 데 사용되는 도구:**  [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [가용성 그룹을 오프라인 상태로 전환한 후](#FollowUp)  
  
-   [관련 내용](#RelatedContent)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
> [!CAUTION]  
>  OFFLINE 옵션은 가용성 그룹 리소스의 클러스터 간 마이그레이션에만 사용합니다.  
  
###  <a name="Prerequisites"></a> 필수 구성 요소  
  
-   OFFLINE 명령을 입력하는 서버 인스턴스에서 [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] 이상(Enterprise Edition 이상)을 실행해야 합니다.  
  
-   가용성 그룹이 현재 온라인 상태여야 합니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
 가용성 그룹을 오프라인 상태로 전환하기 전에 가용성 그룹 수신기를 삭제합니다. 자세한 내용은 [가용성 그룹 수신기 제거&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-listener-sql-server.md)로 업그레이드하려는 경우에 사용합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **가용성 그룹을 오프라인 상태로 전환하려면**  
  
1.  가용성 그룹의 가용성 복제본을 호스팅하는 서버 인스턴스에 연결합니다. 이 복제본은 주 복제본일 수도 있고 보조 복제본일 수도 있습니다.  
  
2.  다음과 같은 [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) 문을 사용합니다.  
  
     ALTER AVAILABILITY GROUP *group_name* OFFLINE  
  
     여기서 *group_name* 은 가용성 그룹의 이름입니다.  
  
### <a name="example"></a>예제  
 다음 예에서는 `AccountsAG` 가용성 그룹을 오프라인 상태로 전환합니다.  
  
```  
ALTER AVAILABILITY GROUP AccountsAG OFFLINE;  
```  
  
##  <a name="FollowUp"></a> 후속 작업: 가용성 그룹을 오프라인 상태로 전환한 후  
  
-   **OFFLINE 작업의 로깅:**  OFFLINE 작업이 시작된 WSFC 노드의 ID는 WSFC 클러스터 로그와 SQL ERRORLOG에 저장됩니다.  
  
-   **가용성 그룹을 오프라인으로 전환하기 전에 해당 수신기를 삭제하지 않은 경우:**  가용성 그룹을 다른 WSFC 클러스터에 마이그레이션하는 경우 수신기의 VNN 및 VIP를 삭제합니다. 수신기의 VNN 및 VIP는 장애 조치(Failover) 클러스터 관리자 콘솔, [Remove-ClusterResource](http://technet.microsoft.com/library/ee461015\(WS.10\).aspx) PowerShell Cmdlet 또는 [cluster.exe](http://technet.microsoft.com/library/ee461015\(WS.10\).aspx)를 사용하여 삭제할 수 있습니다. cluster.exe는 Windows 8에서 더 이상 사용되지 않습니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [가용성 그룹 수신기 제거&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-listener-sql-server.md)  
  
-   [서버 인스턴스의 HADR 클러스터 컨텍스트 변경&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-hadr-cluster-context-of-server-instance-sql-server.md)  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   [SQL Server 2012 기술 문서](http://msdn.microsoft.com/library/bb418445\(SQL.10\).aspx)  
  
-   [SQL Server Always On 팀 블로그: 공식 SQL Server Always On 팀 블로그](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
