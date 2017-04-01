---
title: "매개 변수가 있는 필터로 병합 게시에 대한 파티션 관리 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "파티션 [SQL Server 복제]"
  - "병합 복제 파티션 [SQL Server 복제], SQL Server Management Studio"
  - "매개 변수가 있는 필터 [SQL Server 복제], 파티션 관리"
ms.assetid: fb5566fe-58c5-48f7-8464-814ea78e6221
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# 매개 변수가 있는 필터로 병합 게시에 대한 파티션 관리
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 매개 변수가 있는 필터로 병합 게시에 대한 파티션을 관리하는 방법에 대해 설명합니다. 매개 변수가 있는 행 필터를 사용하여 겹치지 않는 파티션을 생성할 수 있습니다. 이러한 파티션을 제한하여 특정 파티션을 하나의 구독에서만 받도록 할 수 있습니다. 이러한 경우 구독자 수가 많으면 파티션 수가 많아지고 이에 따라 동일한 수의 분할된 스냅숏이 필요합니다. 자세한 내용은 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)을 참조하세요.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [권장 사항](#Recommendations)  
  
-   **다음을 사용하여 매개 변수가 있는 필터로 병합 게시에 대한 파티션을 관리하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   권장하는 복제 토폴로지를 스크립팅할 경우 게시 스크립트는 데이터 파티션을 만드는 저장 프로시저 호출을 포함합니다. 스크립트는 생성된 파티션에 대한 참조와 하나 이상의 파티션을 다시 만드는 방법(필요한 경우)을 제공합니다. 자세한 내용은 [Scripting Replication](../../../relational-databases/replication/scripting-replication.md)을 참조하세요.  
  
-   겹치지 않는 파티션과 함께 구독을 생성하는 매개 변수가 있는 필터가 게시에 사용된 경우 특정 구독이 손실되어 다시 만들어야 하면 구독된 파티션을 제거하고 구독을 다시 만든 다음 파티션을 다시 만듭니다. 자세한 내용은 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)을 참조하세요. 복제에서는 게시 만들기 스크립트가 생성될 때 기존 구독자 파티션에 대한 만들기 스크립트를 생성합니다. 자세한 내용은 [Scripting Replication](../../../relational-databases/replication/scripting-replication.md)을 참조하세요.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 파티션을 관리할는 **데이터 파티션을** 의 페이지는 **게시 속성-\< 게시>** 대화 상자입니다. 이 대화 상자에 액세스하는 방법은 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요. 이 페이지에서는 파티션을 만들거나 삭제하고, 구독자가 스냅숏 생성 및 배달을 시작하도록 허용하고, 하나 이상의 파티션에 대한 스냅숏을 생성하고, 스냅숏을 정리할 수 있습니다.  
  
#### 파티션을 만들려면  
  
1.  에 **데이터 파티션을** 의 페이지는 **게시 속성-\< 게시>** 대화 상자를 클릭 하 여 **추가**.  
  
2.  에 **데이터 파티션 추가** 대화 상자에 대 한 값을 입력 합니다는 **host_name ()** 및/또는 **suser_sname ()** 만들려는 파티션에 관련 된 값입니다.  
  
3.  선택적으로 스냅숏을 새로 고칠 일정을 지정합니다.  
  
    1.  선택 **다음 시간에 실행 되도록이 파티션에 대 한 스냅숏 에이전트를 예약 합니다.**  
  
    2.  기본으로 제공되는 스냅숏 새로 고침 일정을 그대로 적용하거나 **변경** 을 클릭하여 다른 일정을 지정합니다.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 파티션을 삭제하려면  
  
1.  **데이터 파티션** 페이지의 표에서 파티션을 선택합니다.  
  
2.  **삭제**를 클릭합니다.  
  
#### 구독자가 스냅숏 생성 및 배달을 시작하도록 허용하려면  
  
1.  **데이터 파티션** 페이지에서 **새 구독자가 동기화할 때 필요한 경우 자동으로 파티션 정의 및 스냅숏 생성**을 선택합니다.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 파티션에 대한 스냅숏을 생성하려면  
  
1.  **데이터 파티션** 페이지의 표에서 파티션을 선택합니다.  
  
2.  **선택한 스냅숏 지금 생성**을 클릭합니다.  
  
#### 파티션에 대한 스냅숏을 정리하려면  
  
1.  **데이터 파티션** 페이지의 표에서 파티션을 선택합니다.  
  
2.  **기존 스냅숏 정리**를 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 매개 변수가 있는 필터를 사용하여 게시를 보다 잘 관리하려면 복제 저장 프로시저를 사용하여 기존 파티션을 프로그래밍 방식으로 열거합니다. 파티션을 만들거나 기존 파티션을 삭제할 수도 있습니다. 기존 파티션의 다음 정보를 가져올 수 있습니다.  
  
-   파티션의 필터링 하는 방법 (사용 하 여 [SUSER_SNAME (& a) #40; TRANSACT-SQL & #41;](../../../t-sql/functions/suser-sname-transact-sql.md) 또는 [HOST_NAME (& a) #40; Transact-SQL & #41;](../../../t-sql/functions/host-name-transact-sql.md)).  
  
-   분할된 스냅숏을 생성하는 작업의 이름  
  
-   분할된 스냅숏 작업이 마지막으로 실행된 시간  
  
 두 부분으로 구성된 스냅숏의 두 번째 부분은 새 구독이 초기화될 때 요청에 따라 생성될 수 있지만, 아래의 절차를 사용하면 이 스냅숏이 생성되는 방식을 제어하고 가장 편리할 때 이 스냅숏을 미리 생성할 수 있습니다. 자세한 내용은 [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)을 참조하세요.  
  
#### 기존 파티션의 정보를 보려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_helpmergepartition (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql.md)합니다. **@publication**에 게시 이름을 지정합니다. (선택 사항) 지정 **@suser_sname** 또는 **@host_name** 단일 필터링 조건을 기반 정보만 반환 되도록 합니다.  
  
#### 새 파티션을 정의하고 분할된 새 스냅숏을 생성하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addmergepartition (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md)합니다. **@publication**에 게시 이름을 지정하고 다음 중 하나에 파티션을 정의하는 매개 변수가 있는 값을 지정합니다.  
  
    -   **@suser_sname** 매개 변수가 있는 필터에서 반환한 값으로 정의 된 경우- [SUSER_SNAME (& a) #40; TRANSACT-SQL & #41;](../../../t-sql/functions/suser-sname-transact-sql.md)합니다.  
  
    -   **@host_name** 매개 변수가 있는 필터에서 반환한 값으로 정의 된 경우- [HOST_NAME (& a) #40; TRANSACT-SQL & #41;](../../../t-sql/functions/host-name-transact-sql.md)합니다.  
  
2.  이 새 파티션에 대해 매개 변수가 있는 스냅숏을 만들고 초기화합니다. 자세한 내용은 [Create a Snapshot for a Merge Publication with Parameterized Filters](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)을 참조하세요.  
  
#### 파티션을 삭제하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_dropmergepartition (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-dropmergepartition-transact-sql.md)합니다. **@publication** 에 게시 이름을 지정하고 다음 중 하나에 파티션을 정의하는 매개 변수가 있는 값을 지정합니다.  
  
    -   **@suser_sname** 매개 변수가 있는 필터에서 반환한 값으로 정의 된 경우- [SUSER_SNAME (& a) #40; TRANSACT-SQL & #41;](../../../t-sql/functions/suser-sname-transact-sql.md)합니다.  
  
    -   **@host_name** 매개 변수가 있는 필터에서 반환한 값으로 정의 된 경우- [HOST_NAME (& a) #40; TRANSACT-SQL & #41;](../../../t-sql/functions/host-name-transact-sql.md)합니다.  
  
     이 경우 파티션에 대한 스냅숏 작업과 스냅숏 파일도 제거됩니다.  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
 매개 변수가 있는 필터를 사용하여 게시를 보다 잘 관리하려면 RMO(복제 관리 개체)를 사용하여 새 구독자 파티션을 프로그래밍 방식으로 만들고, 기존 구독자 파티션을 열거하고, 프로그래밍 방식으로 열거합니다. 구독자 파티션을 만드는 방법은 [Create a Snapshot for a Merge Publication with Parameterized Filters](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)을 참조하세요. 기존 파티션에 대한 다음 정보를 가져올 수 있습니다.  
  
-   파티션에서 기반으로 사용하는 값 및 필터링 기능  
  
-   구독자에 대해 매개 변수가 있는 스냅숏을 생성하는 작업의 이름  
  
-   매개 변수가 있는 스냅숏 작업이 마지막으로 실행된 시간  
  
#### 기존 파티션의 정보를 보려면  
  
1.  사용 하 여 게시자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.MergePublication> 클래스입니다. 설정의 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 게시 및 설정에 대 한 속성의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 1 단계에서 만든 합니다.  
  
3.  호출의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 2단계에서 게시 속성이 올바르게 정의되지 않았거나 게시가 없습니다.  
  
4.  호출 된 <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergePartitions%2A> 메서드를 배열에 결과 전달 하 고 <xref:Microsoft.SqlServer.Replication.MergePartition> 개체입니다.  
  
5.  각 <xref:Microsoft.SqlServer.Replication.MergePartition> 배열에 개체를 원하는 속성을 가져옵니다.  
  
#### 기존 파티션을 삭제하려면  
  
1.  사용 하 여 게시자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.MergePublication> 클래스입니다. 설정의 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 및 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 게시 및 설정에 대 한 속성의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 1 단계에서 만든 합니다.  
  
3.  호출의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 2단계에서 게시 속성이 올바르게 정의되지 않았거나 게시가 없습니다.  
  
4.  호출 된 <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergePartitions%2A> 메서드를 배열에 결과 전달 하 고 <xref:Microsoft.SqlServer.Replication.MergePartition> 개체입니다.  
  
5.  각 <xref:Microsoft.SqlServer.Replication.MergePartition> 배열에 개체, 파티션을 삭제 되어야 할지 여부를 결정 합니다. 값에 따라 일반적으로이 결정은 <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterLogin%2A> 속성 또는 <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterHostName%2A> 속성입니다.  
  
6.  호출 된 <xref:Microsoft.SqlServer.Replication.MergePublication.RemoveMergePartition%2A> 메서드를는 <xref:Microsoft.SqlServer.Replication.MergePublication> 2 단계에서 개체입니다. 전달 된 <xref:Microsoft.SqlServer.Replication.MergePartition> 5 단계에서 개체입니다.  
  
7.  삭제된 각 파티션에 대해 6단계를 반복합니다.  
  
## 참고 항목  
 [매개 변수가 있는 행 필터](../../../relational-databases/replication/merge/parameterized-row-filters.md)   
 [매개 변수가 있는 필터를 사용하는 병합 게시의 스냅숏](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  