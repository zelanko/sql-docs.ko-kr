---
title: 대기 시간 측정 및 연결 유효성 검사(트랜잭션)
description: SSMS(SQL Server Management Studio), T-SQL(Transact-SQL) 또는 RMO(복제 관리 개체)에서 복제 모니터를 사용하여 SQL Server의 트랜잭션 게시에 대한 대기 시간을 측정하고 연결의 유효성을 검사하는 방법에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, performance
- tracer tokens [SQL Server replication]
- latency [SQL Server replication]
- transactional replication, tracer tokens
- monitoring performance [SQL Server replication], tracer tokens
ms.assetid: 4addd426-7523-4067-8d7d-ca6bae4c9e34
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 355840dee0c7ff327968457a54f55730665d5afe
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321858"
---
# <a name="measure-latency-and-validate-connections-for-transactional-replication"></a>트랜잭션 복제에 대한 대기 시간 측정 및 연결 유효성 검사
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  이 항목에서는 복제 모니터, [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 트랜잭션 복제에 대한 대기 시간을 측정하고 연결의 유효성을 검사하는 방법에 대해 설명합니다. 트랜잭션 복제는 트랜잭션 복제 토폴로지에서 대기 시간을 측정하고 게시자, 배포자 및 구독자 간 연결의 유효성을 검사하는 편리한 방법을 제공하는 추적 프로그램 토큰 기능을 제공합니다. 토큰(적은 양의 데이터)은 게시 데이터베이스의 트랜잭션 로그에 기록되고, 일반적인 복제된 트랜잭션인 것처럼 표시되고, 시스템을 통해 전달되며 다음을 계산할 수 있습니다.  
  
-   게시자에서 커밋된 트랜잭션과 배포자의 배포 데이터베이스에서 삽입된 해당 명령 사이의 경과 시간  
  
-   배포 데이터베이스에 삽입된 명령과 구독자에서 커밋된 해당 트랜잭션 사이의 경과 시간  
  
 이러한 계산을 잘 검토하면 다음을 비롯한 여러 가지 질문에 대답할 수 있습니다.  
  
-   게시자의 변경 내용을 받는 데 가장 오래 걸리는 구독자는 무엇입니까?  
  
-   추적 프로그램 토큰을 받아야 할 구독자가 있습니까? 있다면 아직 추적 프로그램 토큰을 받지 못한 구독자는 무엇입니까?  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
-   **대기 시간을 측정하고 연결의 유효성을 검사하려면:**  
  
     [SQL Server 복제 모니터](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
 또한 추적 프로그램 토큰은 모든 작업을 중지하고 모든 노드가 처리 중인 변경 내용을 모두 받았는지 확인하므로 시스템을 중지시킬 때 유용할 수 있습니다. 자세한 내용은 [복제 토폴로지 정지&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)를 참조하세요.  
  
 추적 토큰을 사용하려면 다음과 같이 특정 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 버전을 사용해야 합니다.  
  
-   배포자는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이후 버전이어야 합니다.  
  
-   게시자는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이후 버전이거나 Oracle 게시자여야 합니다.  
  
-   밀어넣기 구독의 경우 구독자가 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 7.0 이후 버전이면 추적 프로그램 토큰 통계는 게시자, 배포자 및 구독자에서 수집됩니다.  
  
-   끌어오기 구독의 경우 구독자가 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이후 버전이면 추적 프로그램 토큰 통계는 구독자에서만 수집됩니다. 구독자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 7.0이나 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)]인 경우 게시자와 배포자를 통해서만 통계가 수집됩니다.  
  
 또한 다음과 같이 주의해야 할 다른 문제 및 제한 사항이 많이 있습니다.  
  
-   추적 프로그램 토큰을 받으려면 구독이 활성 상태여야 합니다. 구독이 초기화되었다면 활성 상태입니다.  
  
-   다시 초기화는 관련 구독에 대해 보류 중인 추적 프로그램 토큰을 제거합니다.  
  
-   구독자는 자신의 초기 동기화 이후에 생성된 추적 프로그램 토큰만 받습니다.  
  
-   구독자를 다시 게시하면 추적 프로그램 토큰이 전달되지 않습니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 보조 인스턴스에 대한 장애 조치(failover) 후에 복제 모니터는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 게시 인스턴스 이름을 조정할 수 없으며 계속해서 원래 주 인스턴스 이름으로 복제 정보를 표시합니다. 장애 조치(Failover) 후 복제 모니터를 사용하여 추적 프로그램 토큰을 입력할 수 없지만 새 게시자가 [!INCLUDE[tsql](../../../includes/tsql-md.md)]을 사용하여 입력한 추적 프로그램 토큰은 복제 모니터에 표시됩니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server 복제 모니터 사용  
 복제 모니터를 시작하는 방법은 [복제 모니터 시작](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)을 참조하세요.  
  
#### <a name="to-insert-a-tracer-token-and-view-information-on-the-token"></a>추적 프로그램 토큰을 삽입하고 이 토큰에 대한 정보를 보려면  
  
1.  왼쪽 창에서 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
2.  **추적 프로그램 토큰** 탭을 클릭합니다.  
  
3.  **추적 프로그램 삽입**을 클릭합니다.  
  
4.  다음 열에서 추적 프로그램 토큰에 대한 경과된 시간을 확인합니다. **게시자에서 배포자로 연결 시 대기 시간**, **배포자에서 구독자로 연결 시 대기 시간** 및 **총 대기 시간**. 값 **보류 중** 은 토큰이 지정된 지점에 아직 도달하지 않았음을 나타냅니다.  
  
#### <a name="to-view-information-on-a-tracer-token-inserted-previously"></a>이전에 삽입한 추적 프로그램 토큰에 대한 정보를 보려면  
  
1.  왼쪽 창에서 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
2.  **추적 프로그램 토큰** 탭을 클릭합니다.  
  
3.  **삽입된 시간** 드롭다운 목록에서 시간을 선택합니다.  
  
4.  다음 열에서 추적 프로그램 토큰에 대한 경과된 시간을 확인합니다. **게시자에서 배포자로 연결 시 대기 시간**, **배포자에서 구독자로 연결 시 대기 시간** 및 **총 대기 시간**. 값 **보류 중** 은 토큰이 지정된 지점에 아직 도달하지 않았음을 나타냅니다.  
  
    > [!NOTE]  
    >  추적 프로그램 토큰 정보는 배포 데이터베이스의 기록 보존 기간에 의해 제어되는 다른 기록 데이터와 같은 시간 동안 유지됩니다. 배포 데이터베이스 속성 변경에 대한 자세한 내용은 [게시자 및 배포자 속성 보기 및 수정](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)을 참조하세요.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-post-a-tracer-token-to-a-transactional-publication"></a>트랜잭션 게시에 추적 프로그램 토큰을 게시하려면  
  
1.  (옵션) 게시 데이터베이스의 게시자에서 [sp_helppublication&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)을 실행합니다. 해당 게시가 있는지 그리고 상태가 활성 상태인지 확인합니다.  
  
2.  (옵션) 게시 데이터베이스의 게시자에서 [sp_helpsubscription&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)을 실행합니다. 해당 구독이 있는지 그리고 상태가 활성 상태인지 확인합니다.  
  
3.  게시 데이터베이스의 게시자에서 [sp_posttracertoken &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-posttracertoken-transact-sql.md)을 실행하여 **\@publication**을 지정합니다. **\@tracer_token_id** 출력 매개 변수의 값을 확인합니다.  
  
#### <a name="to-determine-latency-and-validate-connections-for-a-transactional-publication"></a>트랜잭션 복제에 대한 대기 시간을 확인하고 연결 유효성을 검사하려면  
  
1.  이전 절차를 따라 게시에 추적 프로그램 토큰을 게시합니다.  
  
2.  게시 데이터베이스의 게시자에서 [sp_helptracertokens &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md)를 실행하여 **\@publication**을 지정합니다. 그러면 해당 게시에 게시된 모든 추적 프로그램 토큰의 목록이 반환됩니다. 결과 집합에서 원하는 **tracer_id** 를 확인합니다.  
  
3.  게시 데이터베이스의 게시자에서 [sp_helptracertokenhistory &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)를 실행하여 **\@publication**을 지정하고 **\@tracer_id**에 대해 2단계에서 얻은 추적 프로그램 토큰 ID를 지정합니다. 그러면 선택한 추적 프로그램 토큰에 대한 대기 시간 정보가 반환됩니다.  
  
#### <a name="to-remove-tracer-tokens"></a>추적 프로그램 토큰을 제거하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_helptracertokens &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md)를 실행하여 **\@publication**을 지정합니다. 그러면 해당 게시에 게시된 모든 추적 프로그램 토큰의 목록이 반환됩니다. 결과 집합에서 삭제할 추적 프로그램 토큰의 **tracer_id** 를 확인합니다.  
  
2.  게시 데이터베이스의 게시자에서 **\@publication**을 지정한 다음 `@tracer_id`에 2단계에서 얻은 삭제할 추적 프로그램의 ID를 지정하고 [sp_deletetracertokenhistory&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md)를 실행합니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 이 예제에서는 추적 프로그램 토큰 레코드를 게시하고 게시된 추적 프로그램 토큰의 반환된 ID를 사용하여 대기 시간 정보를 봅니다.  
  
 [!code-sql[HowTo#sp_tracertokens](../../../relational-databases/replication/codesnippet/tsql/measure-latency-and-vali_1.sql)]  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
  
#### <a name="to-post-a-tracer-token-to-a-transactional-publication"></a>트랜잭션 게시에 추적 프로그램 토큰을 게시하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.TransPublication> 클래스의 인스턴스를 만듭니다.  
  
3.  게시에 대해 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 속성을 설정하고 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 연결로 설정합니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 3단계에서 게시 속성이 올바르게 정의되지 않았거나 게시가 없습니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.TransPublication.PostTracerToken%2A> 메서드를 호출합니다. 이 메서드는 게시의 트랜잭션 로그에 추적 프로그램 토큰을 삽입합니다.  
  
#### <a name="to-determine-latency-and-validate-connections-for-a-transactional-publication"></a>트랜잭션 복제에 대한 대기 시간을 확인하고 연결 유효성을 검사하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 배포자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 클래스의 인스턴스를 만듭니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>및 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A> 속성을 설정하고 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 연결로 설정합니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 3단계에서 게시 모니터 속성이 올바르게 정의되지 않았거나 해당 게시가 없는 것입니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokens%2A> 메서드를 호출합니다. 반환된 <xref:System.Collections.ArrayList> 개체를 <xref:Microsoft.SqlServer.Replication.TracerToken> 개체의 배열로 캐스팅합니다.  
  
6.  <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokenHistory%2A> 메서드를 호출합니다. 5단계에서 삽입한 추적 프로그램 토큰에 대한 <xref:Microsoft.SqlServer.Replication.TracerToken.TracerTokenId%2A> 값을 전달합니다. 그러면 선택한 추적 프로그램 토큰에 대한 대기 시간 정보가 <xref:System.Data.DataSet> 개체로 반환됩니다. 모든 추적 프로그램 토큰 정보가 반환되면 게시자와 배포자 간의 연결 및 배포자와 구독자 간의 연결이 모두 있으며 복제 토폴로지가 작동하고 있는 것입니다.  
  
#### <a name="to-remove-tracer-tokens"></a>추적 프로그램 토큰을 제거하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 배포자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 클래스의 인스턴스를 만듭니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>및 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A> 속성을 설정하고 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 연결로 설정합니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 3단계에서 게시 모니터 속성이 올바르게 정의되지 않았거나 해당 게시가 없는 것입니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokens%2A> 메서드를 호출합니다. 반환된 <xref:System.Collections.ArrayList> 개체를 <xref:Microsoft.SqlServer.Replication.TracerToken> 개체의 배열로 캐스팅합니다.  
  
6.  <xref:Microsoft.SqlServer.Replication.PublicationMonitor.CleanUpTracerTokenHistory%2A> 메서드를 호출합니다. 다음 값 중 하나를 전달합니다.  
  
    -   5단계에서 삽입한 추적 프로그램 토큰에 대한 <xref:Microsoft.SqlServer.Replication.TracerToken.TracerTokenId%2A> 입니다. 그러면 선택한 토큰에 대한 정보가 삭제됩니다.  
  
    -   <xref:System.DateTime> 개체입니다. 그러면 지정한 날짜보다 오래된 모든 토큰에 대한 정보가 삭제됩니다.  
  
  
