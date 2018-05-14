---
title: 서버 인스턴스의 HADR 클러스터 컨텍스트 변경(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- Availability replicas [SQL Server], change WSFC cluster context
ms.assetid: ecd99f91-b9a2-4737-994e-507065a12f80
caps.latest.revision: 32
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 2e312a14c867f455af82d93e1fcf1ebc4b27ed66
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="change-the-hadr-cluster-context-of-server-instance-sql-server"></a>서버 인스턴스의 HADR 클러스터 컨텍스트 변경(SQL Server)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  이 항목에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이상 버전에서 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 을 사용하여 [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] 인스턴스의 HADR 클러스터 컨텍스트를 전환하는 방법에 대해 설명합니다. *HADR 클러스터 컨텍스트* 는 서버 인스턴스에서 호스트하는 가용성 복제본에 대한 메타데이터를 관리하는 WSFC(Windows Server 장애 조치(failover) 클러스터링) 클러스터를 결정합니다.  
  
 새 WSFC 클러스터에서 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 인스턴스로의 클러스터 간 [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] 마이그레이션을 수행하는 동안에만 HADR 클러스터 컨텍스트를 전환합니다. [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 의 클러스터 간 마이그레이션은 가용성 그룹의 작동 중단 시간을 최소화하면서 [!INCLUDE[win8](../../../includes/win8-md.md)] 또는 [!INCLUDE[win8srv](../../../includes/win8srv-md.md)] 로의 OS 업그레이드를 지원합니다. 자세한 내용은 [OS 업그레이드를 위한 Always On 가용성 그룹의 클러스터 간 마이그레이션](http://msdn.microsoft.com/library/jj873730.aspx)을 참조하세요.  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [필수 구성 요소](#Prerequisites)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **가용성 복제본의 클러스터 컨텍스트를 전환하려면:**  [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [가용성 복제본의 클러스터 컨텍스트를 전환한 후](#FollowUp)  
  
-   [관련 태스크](#RelatedTasks)  
  
-   [관련 내용](#RelatedContent)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
> [!CAUTION]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 배포의 클러스터 간 마이그레이션 중에만 HADR 클러스터 컨텍스트를 전환합니다.  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   HADR 클러스터 컨텍스트는 로컬 WSFC 클러스터에서 원격 클러스터로 전환한 다음 다시 원격 클러스터에서 로컬 클러스터로만 전환할 수 있습니다. HADR 클러스터 컨텍스트를 원격 클러스터 간에 전환할 수는 없습니다.  
  
-   HADR 클러스터 컨텍스트는 SQL Server 인스턴스에서 가용성 복제본을 호스팅하지 않을 때만 원격 클러스터로 전환할 수 있습니다.  
  
-   원격 HADR 클러스터 컨텍스트는 언제든지 로컬 클러스터로 다시 전환할 수 있습니다. 그러나 서버 인스턴스에서 가용성 복제본을 호스팅하는 동안에는 컨텍스트를 다시 전환할 수 없습니다.  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
  
-   HADR 클러스터 컨텍스트를 변경하는 서버 인스턴스에서는 [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] 이상(Enterprise Edition 이상)을 실행해야 합니다.  
  
-   서버 인스턴스는 Always On을 사용하도록 설정되어야 합니다. 자세한 내용은 [Always On 가용성 그룹 활성화 및 비활성화&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)를 참조하세요.  
  
-   로컬 클러스터 컨텍스트에서 원격 클러스터 컨텍스트로 전환하려면 서버 인스턴스에서 가용성 복제본을 호스팅해서는 안 됩니다. [sys.availability_replicas](../../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md) 카탈로그 뷰는 행을 반환해서는 안 됩니다.  
  
     서버 인스턴스에 가용성 복제본이 있을 경우 HADR 클러스터 컨텍스트를 변경하려면 먼저 다음 중 하나를 수행해야 합니다.  
  
    |복제본 역할|작업|링크|  
    |------------------|------------|----------|  
    |주|가용성 그룹을 오프라인 상태로 만듭니다.|[가용성 그룹을 오프라인 상태로 만들기&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/take-an-availability-group-offline-sql-server.md)|  
    |보조|가용성 그룹에서 복제본 제거|[가용성 그룹에서 보조 복제본 제거&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md)|  
  
-   원격 클러스터에서 로컬 클러스터로 전환하려면 먼저 모든 동기 커밋 복제본을 동기화해야 합니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   전체 도메인 이름을 지정하는 것이 좋습니다. 이는 짧은 이름의 대상 IP 주소를 찾기 위해 ALTER SERVER CONFIGURATION에서 DNS 확인을 사용하기 때문입니다. 경우에 따라 짧은 이름을 사용하면 DNS 검색 순서로 인해 혼동이 생길 수도 있습니다. 예를 들어 `abc` 도메인의 노드(`node1.abc.com`)에서 다음 명령을 실행한다고 가정합니다. 의도한 대상 클러스터는 `CLUS01` 도메인의 `xyz` 클러스터(`clus01.xyz.com`)입니다. 그러나 로컬 도메인 호스트는 이름이 `CLUS01` 인 클러스터(`clus01.abc.com`)도 호스팅합니다.  
  
     대상 클러스터의 짧은 이름인 `CLUS01`이 지정된 경우 DNS 이름 확인이 잘못된 클러스터의 IP 주소인 `clus01.abc.com`을 반환할 수 있습니다. 이러한 혼동을 방지하려면 다음 예와 같은 대상 클러스터의 전체 이름을 지정합니다.  
  
    ```  
    ALTER SERVER CONFIGURATION SET HADR CLUSTER CONTEXT = 'clus01.xyz.com'  
    ```  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
  
-   **SQL Server 로그인(SQL Server login)**  
  
     CONTROL SERVER 권한이 필요합니다.  
  
-   **SQL Server 서비스 계정**  
  
     서버 인스턴스의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서버스 계정에는 다음이 있어야 합니다.  
  
    -   대상 WSFC 클러스터를 열 수 있는 권한  
  
    -   원격 WSFC 읽기/쓰기 액세스  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **가용성 복제본의 WSFC 클러스터 컨텍스트를 변경하려면**  
  
1.  가용성 그룹의 주 복제본 또는 보조 복제본을 호스팅하는 서버 인스턴스에 연결합니다.  
  
2.  다음과 같이 [ALTER SERVER CONFIGURATION](../../../t-sql/statements/alter-server-configuration-transact-sql.md) 문의 SET HADR CLUSTER CONTEXT 절을 사용합니다.  
  
     ALTER SERVER CONFIGURATION SET HADR CLUSTER CONTEXT **=** { **'***windows_cluster***'**| LOCAL }  
  
     각 항목이 나타내는 의미는 다음과 같습니다.  
  
     *windows_cluster*  
     WSFC 클러스터의 CON(클러스터 개체 이름) 짧은 이름 또는 전체 도메인 이름을 지정할 수 있습니다. 전체 도메인 이름을 지정하는 것이 좋습니다. 자세한 내용은 이 항목의 앞부분에 나오는 [권장 사항](#Recommendations)을 참조하십시오.  
  
     LOCAL  
     로컬 WSFC 클러스터입니다.  
  
### <a name="examples"></a>예  
 다음 예에서는 HARD 클러스터 컨텍스트를 다른 클러스터로 변경합니다. 이 예에서는 대상 WSFC 클러스터( `clus01`)를 식별하기 위해 전체 클러스터 개체 이름( `clus01.xyz.com`)을 지정합니다.  
  
```  
ALTER SERVER CONFIGURATION SET HADR CLUSTER CONTEXT = 'clus01.xyz.com';  
```  
  
 다음 예에서는 HARD 클러스터 컨텍스트를 로컬 WSFC 클러스터로 변경합니다.  
  
```  
ALTER SERVER CONFIGURATION SET HADR CLUSTER CONTEXT = LOCAL;  
```  
  
##  <a name="FollowUp"></a> 후속 작업: 가용성 복제본의 클러스터 컨텍스트를 전환한 후  
 새 HADR 클러스터 컨텍스트는 서버 인스턴스를 다시 시작하지 않아도 즉시 적용됩니다. HADR 클러스터 컨텍스트 설정은 서버 인스턴스를 다시 시작해도 변경되지 않은 영구 인스턴스 수준 설정입니다.  
  
 다음과 같이 [sys.dm_hadr_cluster](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql.md) 동적 관리 뷰를 쿼리하여 새 HADR 클러스터 컨텍스트를 확인합니다.  
  
```  
SELECT cluster_name FROM sys.dm_hadr_cluster  
```  
  
 이 쿼리는 HADR 클러스터 컨텍스트를 설정한 클러스터의 이름을 반환해야 합니다.  
  
 HADR 클러스터 컨텍스트가 새 클러스터로 전환될 경우:  
  
-   현재 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에서 호스팅하는 가용성 복제본에 대한 메타데이터가 정리됩니다.  
  
-   이전에 가용성 복제본에 속한 모든 데이터베이스가 RESTORING 상태가 됩니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [가용성 그룹 수신기 제거&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-listener-sql-server.md)  
  
-   [가용성 그룹을 오프라인 상태로 만들기&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/take-an-availability-group-offline-sql-server.md)  
  
-   [가용성 그룹에 보조 복제본 추가&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [가용성 그룹에서 보조 복제본 제거&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   [SQL Server 2012 기술 문서](http://msdn.microsoft.com/library/bb418445\(SQL.10\).aspx)  
  
-   [SQL Server Always On 팀 블로그: 공식 SQL Server Always On 팀 블로그](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [SQL Server의 WSFC&#40;Windows Server 장애 조치(failover) 클러스터링&#41;](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [ALTER SERVER CONFIGURATION&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-configuration-transact-sql.md)  
  
  
