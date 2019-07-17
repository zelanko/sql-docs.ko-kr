---
title: 가용성 그룹의 보조 복제본에 대한 읽기 전용 액세스 구성
description: 'Always On 가용성 그룹에 대한 읽기 액세스 권한만 허용하도록 보조 복제본을 구성합니다. '
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- connection access to availability replicas
- Availability Groups [SQL Server], readable secondary replicas
- active secondary replicas [SQL Server], read-only access to
- Availability Groups [SQL Server], read-only routing
- Availability Groups [SQL Server], client connectivity
ms.assetid: 22387419-22c4-43fa-851c-5fecec4b049b
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: b596a81bf48a69e9b4c641e878383a4a513c891b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66793666"
---
# <a name="configure-read-only-access-to-a-secondary-replica-of-an-always-on-availability-group"></a>Always On 가용성 그룹의 보조 복제본에 대한 읽기 전용 액세스 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  기본적으로 주 복제본에 대한 읽기/쓰기 및 읽기 전용 액세스가 모두 허용되며 Always On 가용성 그룹의 보조 복제본에 대한 연결은 허용되지 않습니다. 이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]또는 PowerShell을 사용하여 Always On 가용성 그룹의 가용성 복제본에 대한 연결 액세스를 구성하는 방법을 설명합니다.  
  
 보조 복제본에 대해 읽기 전용 액세스를 사용하도록 설정할 경우의 영향에 대한 자세한 내용과 연결 액세스 소개는 [가용성 복제본에 대한 클라이언트 연결 액세스 정보&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md) 및 [활성 보조: 읽기 가능한 보조 복제본&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)을 참조하세요.  
  
 
##  <a name="Prerequisites"></a> 사전 요구 사항 및 제한 사항  
  
-   다른 연결 액세스를 구성하려면 주 복제본을 호스팅하는 서버 인스턴스에 연결되어 있어야 합니다.  
  
##  <a name="Permissions"></a> 사용 권한  
  
|태스크|사용 권한|  
|----------|-----------------|  
|가용성 그룹을 만들 때 복제본을 구성하려면|CREATE AVAILABILITY GROUP 서버 권한, ALTER ANY AVAILABILITY GROUP 권한, CONTROL SERVER 권한 중 하나와 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.|  
|가용성 복제본을 수정하려면|가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.|  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **가용성 복제본에 대한 액세스를 구성하려면**  
  
1.  개체 탐색기에서 주 복제본을 호스팅하는 서버 인스턴스에 연결하고 서버 트리를 확장합니다.  
  
2.  **Always On 고가용성** 노드 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  복제본을 변경할 가용성 그룹을 클릭합니다.  
  
4.  가용성 복제본을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
5.  **가용성 복제본 속성** 대화 상자에서 다음과 같이 주 역할 및 보조 역할에 대한 연결 액세스를 변경할 수 있습니다.  
  
    -   보조 역할의 경우 **읽기용 보조** 드롭 목록의 다음 값 중에서 새 값을 선택합니다.  
  
         **아니요**  
         이 복제본의 보조 데이터베이스에 대한 사용자 연결이 허용되지 않습니다. 즉, 읽기 액세스가 가능하지 않습니다. 이 값은 기본 설정입니다.  
  
         **읽기 전용만**  
         이 복제본의 보조 데이터베이스에 대한 읽기 전용 연결만 허용됩니다. 즉, 모든 보조 데이터베이스에 대한 읽기 액세스가 가능합니다.  
  
         **예**  
         이 복제본의 보조 데이터베이스에 대한 모든 연결이 허용되지만 읽기 액세스만 가능합니다. 즉, 모든 보조 데이터베이스에 대한 읽기 액세스가 가능합니다.  
  
    -   주 역할의 경우 **주 역할의 연결 모드** 드롭 목록의 다음 값 중에서 새 값을 선택합니다.  
  
         **모든 연결 허용**  
         주 복제본의 데이터베이스에 대한 모든 연결이 허용됩니다. 이 값은 기본 설정입니다.  
  
         **읽기/쓰기 연결 허용**  
         애플리케이션 의도 속성이 **ReadWrite** 로 설정되었거나 애플리케이션 의도 연결 속성이 설정되지 않은 경우에는 연결이 허용됩니다. 애플리케이션 의도 연결 속성이 **ReadOnly** 로 설정된 연결은 허용되지 않습니다. 따라서 고객이 읽기 전용 작업을 실수로 주 복제본에 연결하는 것을 방지할 수 있습니다. 애플리케이션 의도 연결 속성에 대한 자세한 내용은 [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)을 참조하십시오.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **가용성 복제본에 대한 액세스를 구성하려면**  
  
> [!NOTE]  
>  이 절차에 대한 예는 이 섹션의 뒷부분에 나오는 [예제(Transact-SQL)](#TsqlExample)을 참조하세요.  
  
1.  주 복제본을 호스팅하는 서버 인스턴스에 연결합니다.  
  
2.  새 가용성 그룹에 대한 복제본을 지정하려는 경우 [CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 사용합니다. 기존 가용성 그룹의 복제본을 추가하거나 수정하려는 경우에는 [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 사용합니다.  
  
    -   보조 역할에 대한 연결 액세스를 구성하려면 ADD REPLICA 또는 MODIFY REPLICA WITH 절에서 다음과 같이 SECONDARY_ROLE 옵션을 지정합니다.  
  
         SECONDARY_ROLE **(** ALLOW_CONNECTIONS **=** { NO | READ_ONLY | ALL } **)**  
  
         각 항목이 나타내는 의미는 다음과 같습니다.  
  
         아니요  
         이 복제본의 보조 데이터베이스에 대한 직접 연결이 허용되지 않습니다. 즉, 읽기 액세스가 가능하지 않습니다. 이 값은 기본 설정입니다.  
  
         READ_ONLY  
         이 복제본의 보조 데이터베이스에 대한 읽기 전용 연결만 허용됩니다. 즉, 모든 보조 데이터베이스에 대한 읽기 액세스가 가능합니다.  
  
         ALL  
         이 복제본의 보조 데이터베이스에 대한 모든 연결이 허용되지만 읽기 액세스만 가능합니다. 즉, 모든 보조 데이터베이스에 대한 읽기 액세스가 가능합니다.  
  
3.  주 역할에 대한 연결 액세스를 구성하려면 ADD REPLICA 또는 MODIFY REPLICA WITH 절에서 다음과 같이 PRIMARY_ROLE 옵션을 지정합니다.  
  
     PRIMARY_ROLE **(** ALLOW_CONNECTIONS **=** { READ_WRITE | ALL } **)**  
  
     각 항목이 나타내는 의미는 다음과 같습니다.  
  
     READ_WRITE  
     애플리케이션 의도 연결 속성이 **ReadOnly** 로 설정된 연결은 허용되지 않습니다.  애플리케이션 의도 속성이 **ReadWrite** 로 설정되었거나 애플리케이션 의도 연결 속성이 설정되지 않은 경우에는 연결이 허용됩니다. 애플리케이션 의도 연결 속성에 대한 자세한 내용은 [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)을 참조하십시오.  
  
     ALL  
     주 복제본의 데이터베이스에 대한 모든 연결이 허용됩니다. 이 값은 기본 설정입니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예제에서는 *AG2*라는 가용성 그룹에 보조 복제본을 추가합니다. 독립 실행형 서버 인스턴스인 *COMPUTER03\HADR_INSTANCE*가 새 가용성 복제본을 호스트하도록 지정됩니다. 이 복제본은 주 역할에 대해 읽기/쓰기 연결만 허용하고 보조 역할에 대해 읽기 전용 연결만 허용하도록 구성되어 있습니다.  
  
```  
ALTER AVAILABILITY GROUP AG2   
   ADD REPLICA ON   
      'COMPUTER03\HADR_INSTANCE' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER03:7022',  
         PRIMARY_ROLE ( ALLOW_CONNECTIONS = READ_WRITE ),  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY )  
         );   
GO  
```  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
 **가용성 복제본에 대한 액세스를 구성하려면**  
  
> [!NOTE]  
>  코드 예제를 보려면 이 섹션의 뒷부분에 나오는 [예제(PowerShell)](#PSExample)을 참조하세요.  
  
1.  주 복제본을 호스트하는 서버 인스턴스로 디렉터리(**cd**)를 변경합니다.  
  
2.  가용성 그룹에 가용성 복제본을 추가하는 경우 **New-SqlAvailabilityReplica** cmdlet을 사용합니다. 기존 가용성 복제본을 수정하는 경우 **Set-SqlAvailabilityReplica** cmdlet을 사용합니다. 관련 매개 변수는 다음과 같습니다.  
  
    -   보조 역할에 대한 연결 액세스를 구성하려면 **ConnectionModeInSecondaryRole**_secondary_role_keyword_ 매개 변수를 지정합니다. 여기서 *secondary_role_keyword* 에는 다음 값 중 하나를 사용합니다.  
  
         **AllowNoConnections**  
         보조 복제본의 데이터베이스에 대한 직접 연결이 허용되지 않으며 읽기 액세스를 위해 데이터베이스에 연결할 수 없습니다. 이 값은 기본 설정입니다.  
  
         **AllowReadIntentConnectionsOnly**  
         애플리케이션 의도 속성이 **ReadOnly**로 설정된 경우에만 보조 복제본의 데이터베이스에 연결할 수 있습니다. 이 속성에 대한 자세한 내용은 [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)을 참조하십시오.  
  
         **AllowAllConnections**  
         보조 복제본의 데이터베이스에 대해 읽기 전용 액세스를 위한 모든 연결이 허용됩니다.  
  
    -   주 역할에 대한 연결 액세스를 구성하려면 **ConnectionModeInPrimaryRole**_primary_role_keyword_를 지정합니다. 여기서 *primary_role_keyword* 에는 다음 값 중 하나를 사용합니다.  
  
         **AllowReadWriteConnections**  
         애플리케이션 의도 연결 속성이 ReadOnly로 설정된 연결은 허용되지 않습니다. 애플리케이션 의도 속성이 ReadWrite로 설정되었거나 애플리케이션 의도 연결 속성이 설정되지 않은 경우에는 연결이 허용됩니다. 애플리케이션 의도 연결 속성에 대한 자세한 내용은 [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)을 참조하십시오.  
  
         **AllowAllConnections**  
         주 복제본의 데이터베이스에 대한 모든 연결이 허용됩니다. 이 값은 기본 설정입니다.  
  
    > [!NOTE]  
    >  cmdlet의 구문을 보려면 **PowerShell 환경에서** Get-Help [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] cmdlet을 사용합니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)을 참조하세요.  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
###  <a name="PSExample"></a> 예제(PowerShell)  
 다음 예에서는 **ConnectionModeInSecondaryRole** 및 **ConnectionModeInPrimaryRole** 매개 변수를 모두 **AllowAllConnections**으로 설정합니다.  
  
```  
Set-Location SQLSERVER:\SQL\PrimaryServer\default\AvailabilityGroups\MyAg  
$primaryReplica = Get-Item "AvailabilityReplicas\PrimaryServer"  
Set-SqlAvailabilityReplica -ConnectionModeInSecondaryRole "AllowAllConnections" `   
-InputObject $primaryReplica  
Set-SqlAvailabilityReplica -ConnectionModeInPrimaryRole "AllowAllConnections" `   
-InputObject $primaryReplica  
  
```  
  
##  <a name="FollowUp"></a> 후속 작업: 가용성 복제본에 대한 읽기 전용 액세스를 구성한 후  
 **읽을 수 있는 보조 복제본에 대한 읽기 전용 액세스**  
  
-   [bcp 유틸리티](../../../tools/bcp-utility.md) 또는 [sqlcmd 유틸리티](../../../tools/sqlcmd-utility.md)를 사용하는 경우 **-K ReadOnly** 스위치를 지정하여 읽기 전용 액세스를 사용하도록 설정된 보조 복제본에 대한 읽기 전용 액세스를 지정할 수 있습니다.  
  
-   클라이언트 애플리케이션을 읽을 수 있는 보조 복제본에 연결할 수 있도록 설정하려면:  
  
    ||사전 요구 사항|링크|  
    |-|------------------|----------|  
    |![확인란](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "확인란")|가용성 그룹에 수신기가 있는지 확인합니다.|[가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)|  
    |![확인란](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "확인란")|가용성 그룹에 대한 읽기 전용 라우팅을 구성합니다.|[가용성 그룹에 대한 읽기 전용 라우팅 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)|  
  
 **장애 조치(Failover) 후 트리거 및 작업에 영향을 줄 수 있는 요소**  
  
 읽을 수 없는 보조 데이터베이스 또는 읽을 수 있는 보조 데이터베이스에서 실행할 때 실패하는 트리거 및 작업이 있는 경우 트리거와 작업을 스크립팅하여 지정된 복제본에서 데이터베이스가 주 데이터베이스인지 읽을 수 있는 보조 데이터베이스인지 확인해야 합니다. 이 정보를 얻으려면 [DATABASEPROPERTYEX](../../../t-sql/functions/databasepropertyex-transact-sql.md) 함수를 사용하여 데이터베이스의 **Updateability** 속성을 반환합니다. 읽기 전용 데이터베이스를 식별하려면 다음과 같이 READ_ONLY를 값으로 지정합니다.  
  
```  
DATABASEPROPERTYEX([db name],'UpdateAbility') = N'READ_ONLY'  
```  
  
 쓰기 전용 데이터베이스를 식별하려면 READ_WRITE를 값으로 지정합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [가용성 그룹에 대한 읽기 전용 라우팅 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   [Always On: 읽기 가능한 보조의 값 위치 지정](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-value-proposition-of-readable-secondary.aspx)  
  
-   [Always On: 읽기 작업에 보조 복제본을 설정하는 옵션이 2개인 이유는 무엇인가요?](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-why-there-are-two-options-to-enable-a-secondary-replica-for-read-workload.aspx)  
  
-   [Always On: 읽기 가능한 보조 복제본 설정](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-setting-up-readable-seconary-replica.aspx)  
  
-   [Always On: 읽기 가능한 보조 복제본을 설정했지만 내 쿼리가 차단됨](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-i-just-enabled-readble-secondary-but-my-query-is-blocked.aspx)  
  
-   [Always On: 읽기 가능한 보조, 읽기 전용 데이터베이스 및 데이터베이스 스냅샷에서 최신 통계를 사용할 수 있도록 함](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-making-upto-date-statistics-available-on-readable-secondary-read-only-database-and-database-snapshot.aspx)  
  
-   [Always On: 읽기 전용 데이터베이스, 데이터베이스 스냅샷 및 보조 복제본에서 통계 사용 시 문제점](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-challenges-with-statistics-on-readonly-database-database-snapshot-and-secondary-replica.aspx)  
  
-   [Always On: 보조 복제본에서 보고 작업을 실행할 때 주 작업에 미치는 영향](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-impact-on-the-primary-workload-when-you-run-reporting-workload-on-the-secondary-replica.aspx)  
  
-   [Always On: 읽기 가능한 보조 복제본의 보고 작업을 스냅샷 격리로 매핑의 영향](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-impact-of-mapping-reporting-workload-to-snapshot-isolation-on-readable-secondary.aspx)  
  
-   [Always On: 보조 복제본에서 보고 작업을 실행하는 경우 REDO 스레드 차단 최소화](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-minimizing-blocking-of-redo-thread-when-running-reporting-workload-on-secondary-replica.aspx)  
  
-   [Always On: 읽기 가능한 보조 및 데이터 대기 시간](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On.aspx)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [활성 보조 복제본: 읽기 가능한 보조 복제본&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [가용성 복제본에 대한 클라이언트 연결 액세스 정보&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)  
  
  
