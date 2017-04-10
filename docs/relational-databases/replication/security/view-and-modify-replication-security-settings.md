---
title: "복제 보안 설정 보기 및 수정 | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "복제 보안 설정 수정"
  - "복제 [SQL Server], 보안"
  - "보안 [SQL Server 복제], 설정 보기"
  - "복제 보안 설정 보기"
  - "보안 [SQL Server 복제], 설정 수정"
ms.assetid: 67d79532-1482-4de1-ac9f-4a23d162c85e
caps.latest.revision: 47
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 47
---
# 복제 보안 설정 보기 및 수정
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 복제 보안 설정을 보고 수정하는 방법에 대해 설명합니다. 예를 들어 게시자에 대한 로그 판독기 에이전트의 연결을 SQL Server 인증에서 Windows 통합 인증으로 변경해야 하거나 Windows 계정 암호가 변경되었을 때 에이전트 작업을 실행하는 데 사용된 자격 증명을 변경해야 할 경우가 있습니다. 각 에이전트에 필요한 사용 권한에 대 한 정보를 참조 하십시오. [복제 에이전트 보안 모델](../../../relational-databases/replication/security/replication-agent-security-model.md)합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 복제 보안 설정을 보고 수정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
-   **후속 작업:**  [복제 보안 설정 수정 후](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   사용되는 저장 프로시저는 에이전트의 유형과 서버 연결의 유형에 따라 다릅니다.  
  
-   사용하는 RMO 클래스 및 속성은 에이전트 유형 및 서버 연결 유형에 따라 달라집니다.  
  
###  <a name="Security"></a> 보안  
 보안을 위해 암호의 실제 값은 복제 저장 프로시저에 의해 반환된 결과 집합에서 마스킹됩니다.  
  
####  <a name="Permissions"></a> 사용 권한  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 다음 대화 상자에서 보안 설정을 확인하고 수정합니다.  
  
1.  **의** 복제 **폴더에서 사용할 수 있는** 복제 암호 업데이트 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. 복제 토폴로지의 서버에서 Windows 계정이나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 계정의 암호를 변경할 경우 해당 계정을 사용하는 각 에이전트의 암호를 업데이트하지 말고 이 대화 상자를 사용하세요. 두 개 이상의 서버에 있는 에이전트에서 같은 계정을 사용할 경우 각 서버에 연결하고 암호를 변경해야 합니다. 해당 암호를 사용하는 복제가 있는 모든 위치에서 암호가 업데이트됩니다. 연결된 서버와 같은 다른 위치에서는 암호가 업데이트되지 않습니다.  
  
2.   **에이전트 보안** 의 페이지는 **게시 속성-\< 게시>** 대화 상자입니다. 이 대화 상자에 액세스하는 방법은 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
3.   **구독 속성-\< 구독>** 대화 상자입니다. 이 대화 상자에 액세스하는 방법은 [View and Modify Push Subscription Properties](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md) 및 [View and Modify Pull Subscription Properties](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)을 참조하세요.  
  
4.   **배포자 속성-\< 배포자>** 및 **배포 데이터베이스 속성-\< 데이터베이스>** 대화 상자입니다. 이러한 대화 상자에 액세스하는 방법은 [View and Modify Distributor and Publisher Properties](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)을 참조하세요.  
  
5.   **게시자 속성-\< 게시자>** 대화 상자입니다. 이 대화 상자에 액세스하는 방법은 [View and Modify Distributor and Publisher Properties](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)을 참조하세요.  
  
#### 하나 이상의 에이전트에서 사용하는 계정의 암호를 변경하려면  
  
1.  SQL Server 계정을 사용하는 경우 이 대화 상자에서 SQL Server 계정 암호도 변경합니다. Windows 계정을 사용하는 경우에는 Windows에서 해당 암호부터 변경합니다. 자세한 내용은 Windows 설명서를 참조하세요.  
  
    > [!NOTE]  
    >  복제 암호를 변경한 후 해당 암호를 사용하는 각 에이전트를 중지한 다음 다시 시작해야 에이전트에 변경 내용이 적용됩니다.  
  
2.  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 서버에 연결한 다음 해당 서버 노드를 확장합니다.  
  
3.  마우스 오른쪽 단추로 클릭는 **복제** 폴더를 마우스 클릭 한 다음 **복제 암호 업데이트**합니다.  
  
4.  **복제 암호 업데이트** 대화 상자에서 계정과 새 암호를 지정합니다.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 스냅숏 에이전트의 보안 설정을 변경하려면  
  
1.  에 **에이전트 보안** 의 페이지는 **게시 속성-\< 게시>** 대화 상자를 클릭는 **보안 설정을** 단추 옆에 **스냅숏 에이전트** 텍스트 상자입니다.  
  
2.  **스냅숏 에이전트 보안** 대화 상자에서 에이전트가 실행될 계정을 지정합니다.  
  
    -   **에이전트 계정** 입력란에 새 Windows 계정을 입력합니다.  
  
    -   **암호** 및 **암호 확인** 입력란에 강력한 새 암호를 입력합니다.  
  
3.  에이전트가 배포자에서 게시자로 연결해야 하는 컨텍스트를 지정합니다. **다음 SQL Server 로그인 사용**을 선택하면 로그인도 지정해야 합니다.  
  
    -   **로그인** 입력란에 로그인을 입력합니다.  
  
    -   **암호** 및 **암호 확인** 입력란에 강력한 새 암호를 입력합니다.  
  
    > [!NOTE]  
    >  연결 컨텍스트에 지정 된 게시자가 Oracle 게시자 인 경우는 **배포자 속성-\< 배포자>**대화 상자입니다. 컨텍스트를 변경할 프로시저에 대한 내용은 아래를 참조하세요.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 로그 판독기 에이전트의 보안 설정을 변경하려면  
  
1.  에 **에이전트 보안** 의 페이지는 **게시 속성-\< 게시>** 대화 상자를 클릭는 **보안 설정을** 단추 옆에 **로그 판독기 에이전트** 텍스트 상자입니다.  
  
2.  **로그 판독기 에이전트 보안** 대화 상자에서 에이전트가 실행될 계정을 지정합니다.  
  
    -   **에이전트 계정** 입력란에 새 Windows 계정을 입력합니다.  
  
    -   **암호** 및 **암호 확인** 입력란에 강력한 새 암호를 입력합니다.  
  
3.  에이전트가 배포자에서 게시자로 연결해야 하는 컨텍스트를 지정합니다. **다음 SQL Server 로그인 사용**을 선택하면 로그인도 지정해야 합니다.  
  
    -   **로그인** 입력란에 로그인을 입력합니다.  
  
    -   **암호** 및 **암호 확인** 입력란에 강력한 새 암호를 입력합니다.  
  
    > [!NOTE]  
    >  연결 컨텍스트에 지정 된 게시자가 Oracle 게시자 인 경우는 **배포자 속성-\< 배포자>**대화 상자입니다. 다음 프로시저를 사용하여 컨텍스트를 변경합니다.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  게시된 각 데이터베이스에 대해 하나의 로그 판독기 에이전트가 있습니다. 하나의 게시에 있는 에이전트의 보안 설정을 변경하면 게시 데이터베이스에 있는 모든 게시의 설정에 영향을 미치게 됩니다.  
  
#### Oracle 게시에 대한 게시자에 스냅숏 에이전트 및 로그 판독기 에이전트를 연결하는 컨텍스트를 변경하려면  
  
1.  에 **게시자** 의 페이지는 **배포자 속성-\< 배포자>** 대화 상자에서 속성 단추를 클릭 (**...**) 게시자 옆에 있습니다.  
  
2.  **에이전트에서 게시자 연결** 섹션에서 사용자가 구성한 복제 관리 사용자 스키마에서 사용하는 로그인 및 암호를 지정합니다. 자세한 내용은 참조 [Oracle 게시자를 구성](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)합니다.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 밀어넣기 구독에 대한 배포 에이전트의 보안 설정을 변경하려면  
  
1.   **구독 속성-\< 구독>** 대화 상자는 다음 변경 내용이 게시자에서 가능 합니다.  
  
    -   배포 에이전트가 실행 및 배포자에 연결 하는 계정을 변경 하려면는 **에이전트 프로세스 계정** 행을 다음 속성을 클릭 (**...**) 행에는 단추입니다. **배포 에이전트 보안** 대화 상자에서 계정과 암호를 지정합니다.  
  
    -   배포 에이전트가 구독자에 연결 하는 컨텍스트를 변경 하려면는 **구독자 연결** 행을 다음 속성을 클릭 (**...**) 행에는 단추입니다. **연결 정보 입력** 대화 상자에서 컨텍스트를 지정합니다.  
  
         지연 업데이트 구독을 사용할 경우 큐 판독기 에이전트도 구독자에 연결하기 위해 여기에서 지정한 컨텍스트를 사용합니다.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 끌어오기 구독에 대한 배포 에이전트의 보안 설정을 변경하려면  
  
1.  에 **구독 속성-\< 구독>** 대화 상자, 구독자에서 다음과 같이 변경 가능 합니다.  
  
    -   배포 에이전트가 실행 및 구독자에 연결 하는 계정을 변경 하려면는 **에이전트 프로세스 계정** 행을 다음 속성을 클릭 (**...**) 행에는 단추입니다. **배포 에이전트 보안** 대화 상자에서 계정과 암호를 지정합니다.  
  
         지연 업데이트 구독을 사용할 경우 큐 판독기 에이전트도 구독자에 연결하기 위해 여기에서 지정한 컨텍스트를 사용합니다.  
  
    -   배포 에이전트가 배포자에 연결 하는 컨텍스트를 변경 하려면는 **배포자 연결** 행을 다음 속성을 클릭 (**...**) 행에는 단추입니다. **연결 정보 입력** 대화 상자에서 컨텍스트를 지정합니다.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 밀어넣기 구독에 대한 병합 에이전트의 보안 설정을 변경하려면  
  
1.   **구독 속성-\< 구독>** 대화 상자는 다음 변경 내용이 게시자에서 가능 합니다.  
  
    -   병합 에이전트가 실행 및 게시자 및 배포자에 연결 하는 계정을 변경 하려면는 **에이전트 프로세스 계정** 행을 다음 속성을 클릭 (**...**) 행에는 단추입니다. **병합 에이전트 보안** 대화 상자에서 계정과 암호를 지정합니다.  
  
    -   병합 에이전트가 구독자에 연결 하는 컨텍스트를 변경 하려면는 **구독자 연결** 행을 다음 속성을 클릭 (**...**) 행에는 단추입니다. **연결 정보 입력** 대화 상자에서 컨텍스트를 지정합니다.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 끌어오기 구독에 대한 병합 에이전트의 보안 설정을 변경하려면  
  
1.  에 **구독 속성-\< 구독>** 대화 상자, 구독자에서 다음과 같이 변경 가능 합니다.  
  
    -   병합 에이전트가 실행 및 구독자에 연결 하는 계정을 변경 하려면는 **에이전트 프로세스 계정** 행을 다음 속성을 클릭 (**...**) 행에는 단추입니다. **병합 에이전트 보안** 대화 상자에서 계정과 암호를 지정합니다.  
  
    -   병합 에이전트가 게시자 및 배포자에 연결 하는 컨텍스트를 변경 하려면는 **게시자 연결** 행을 다음 속성을 클릭 (**...**) 행에는 단추입니다. **연결 정보 입력** 대화 상자에서 컨텍스트를 지정합니다.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 큐 판독기 에이전트가 실행되는 계정을 변경하려면  
  
1.  에 **일반** 의 페이지는 **배포자 속성-\< 배포자>** 대화 상자에서 속성을 클릭 (**...**) 배포 데이터베이스 옆에 있는 단추입니다.  
  
2.  에 **배포 데이터베이스 속성-\< 데이터베이스>** 대화 상자를 클릭는 **보안 설정을** 단추 옆에 **에이전트 프로세스 계정** 텍스트 상자입니다.  
  
3.  **큐 판독기 에이전트 보안** 대화 상자에서 에이전트를 실행하고 배포자에 에이전트를 연결하는 계정을 지정합니다.  
  
    -   **프로세스 계정** 입력란에 새 Windows 계정을 입력합니다.  
  
    -   **암호** 및 **암호 확인** 입력란에 강력한 새 암호를 입력합니다.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  각 배포 데이터베이스에 대해 하나의 큐 판독기 에이전트가 있습니다. 에이전트에 대한 보안 설정을 변경하면 이 배포 데이터베이스를 사용하는 모든 게시자의 모든 게시 설정이 영향을 받습니다.  
  
#### 게시자에 큐 판독기 에이전트를 연결하는 컨텍스트를 변경하려면  
  
1.  에 **게시자** 의 페이지는 **배포자 속성-\< 배포자>** 대화 상자에서 속성 단추를 클릭 (**...**) 게시자 옆에 있습니다.  
  
2.  **에이전트에서 게시자 연결** 섹션에서 **에이전트 연결 모드** 옵션에 대해 **에이전트 프로세스 계정 가장** 또는 **SQL Server 인증** 의 값을 지정합니다. **SQL Server 인증**을 지정하면 **로그인** 및 **암호**값도 지정해야 합니다.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  각 배포 데이터베이스에 대해 하나의 큐 판독기 에이전트가 있습니다. 에이전트에 대한 보안 설정을 변경하면 이 배포 데이터베이스를 사용하는 모든 게시자의 모든 게시 설정이 영향을 받습니다.  
  
#### 구독자에 큐 판독기 에이전트를 연결하는 컨텍스트를 변경하려면  
  
-   큐 판독기 에이전트는 배포 에이전트가 구독에 연결할 때 사용하는 것과 동일한 연결 컨텍스트를 사용합니다. 자세한 내용은 배포 에이전트에 대한 위의 절차를 참조하세요.  
  
#### 끌어오기 구독 즉시 업데이트에 대한 보안 설정을 변경하려면  
  
1.  에 **구독 속성-\< 구독>** 대화 상자는 구독자에서 클릭는 **게시자 연결** 행을 다음 속성을 클릭 (**...**) 행에서 단추입니다.  
  
2.  **연결 정보 입력** 대화 상자에서 다음 옵션 중 하나를 선택합니다.  
  
    -   **연결된 서버나 원격 서버의 로그인 사용**. 원격 서버 또는 사용 하 여 게시자와 구독자 간의 연결 된 서버를 정의 하는 경우이 옵션을 선택 합니다. [sp_addserver (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), [sp_addlinkedserver (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], 또는 다른 방법입니다.  
  
    -   **다음 로그인 및 암호로 SQL Server 인증 사용**. 구독자와 게시자 간에 원격 서버 또는 연결된 서버를 정의하지 않은 경우 이 옵션을 선택하세요. 복제 시 연결된 서버가 자동으로 생성됩니다. 지정한 계정은 게시자에 이미 있어야 합니다.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  이 프로시저는 구독자에서 변경 내용이 발생하면 복제 트리거가 구독자에서 게시자로 연결할 때 사용하는 메서드를 변경합니다. 즉시 업데이트 구독에 대한 배포 에이전트와 관련된 설정 또한 변경할 수 있습니다. 자세한 내용은 이 항목 앞부분의 절차를 참조하세요.  
>   
>  이 프로시저는 끌어오기 구독에만 적용됩니다. 밀어넣기 구독의 경우 저장된 프로시저를 사용 하 여 [sp_link_publication (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md)합니다.  
  
#### 관리 연결의 암호를 게시자에서 배포자로 변경하려면  
  
1.  에 **게시자** 의 페이지는 **배포자 속성-\< 배포자>** 대화 상자에 강력한 암호를 입력 합니다는 **암호** 및 **암호 확인** 텍스트 상자입니다.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
3.  에 **일반** 의 페이지는 **게시자 속성-\< 게시자>** 대화 상자에 강력한 암호를 입력 합니다는 **암호** 및 **암호 확인** 텍스트 상자입니다.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
> [!IMPORTANT]  
>  가능한 경우 다음의 모든 절차에서 런타임에 사용자에게 보안 자격 증명을 입력하라는 메시지를 표시하세요. 스크립트 파일에 자격 증명을 저장하는 경우에는 무단으로 액세스하지 못하도록 파일에 보안을 설정해야 합니다.  
  
#### 복제 서버에서 저장된 암호의 모든 인스턴스를 변경하려면  
  
1.  Master 데이터베이스의 복제 토폴로지에 있는 서버에서 실행 [sp_changereplicationserverpasswords](../../../relational-databases/system-stored-procedures/sp-changereplicationserverpasswords-transact-sql.md)합니다. 지정 된 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 계정 또는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 암호를 변경할 **@login** 및 계정이 나 로그인에 대 한 새 암호 **@password**합니다. 이렇게 하면 토폴로지의 다른 서버에 연결할 때 서버의 모든 에이전트에서 사용되는 암호의 모든 인스턴스가 변경됩니다.  
  
    > [!NOTE]  
    >  로그인 및 암호 (예: 배포자 또는 구독자)을 토폴로지의 특정 서버에 대 한 연결에 대 한 지정이 서버의 이름을 변경 하려면 **@server**합니다.  
  
2.  암호를 업데이트해야 하는 복제 토폴로지의 모든 서버에서 1단계를 반복합니다.  
  
    > [!NOTE]  
    >  복제 암호를 변경한 후 해당 암호를 사용하는 각 에이전트를 중지한 다음 다시 시작해야 에이전트에 변경 내용이 적용됩니다.  
  
#### 스냅숏 에이전트의 보안 설정을 변경하려면  
  
1.  게시자에서 실행 [sp_helppublication_snapshot](../../../relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql.md), 로 지정 하 여 **@publication**합니다. 이렇게 하면 스냅숏 에이전트에 대한 현재 보안 설정이 반환됩니다.  
  
2.  게시자에서 실행 [sp_changepublication_snapshot](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md), 로 지정 하 여 **@publication** 하나 이상의 다음 보안 설정을 변경 하려면:  
  
    -   Windows 계정을 변경 하려면 에이전트를 실행 하는 경우 또는이 계정에 대 한 암호만 지정 **@job_login** 및 **@job_password**합니다.  
  
    -   게시자에 연결할 때 사용 되는 보안 모드를 변경 하려면 값을 지정 **1** 또는 **0** 에 대 한 **@publisher_security_mode**합니다.  
  
    -   게시자에 연결할 때 사용 되는 보안 모드를 변경 하는 경우 **1** 에 **0** 변경 하는 경우 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인이이 연결에 사용 되는, 지정 **@publisher_login** 및 **@publisher_password**합니다.  
  
    > [!IMPORTANT]  
    >  모든 매개 변수에 대해 제공 된 값 원격 배포자로 게시자를 구성할 경우 포함 하 여 *job_login* 및 *job_password*, 를 일반 텍스트로 배포자에 보내집니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 참조 [#40; 및 데이터베이스 엔진에 암호화 된 연결 사용 SQL Server 구성 관리자 및 #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)합니다.  
  
#### 로그 판독기 에이전트의 보안 설정을 변경하려면  
  
1.  게시자에서 실행 [sp_helplogreader_agent](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md), 로 지정 하 여 **@publisher**합니다. 이렇게 하면 로그 판독기 에이전트에 대한 현재 보안 설정이 반환됩니다.  
  
2.  게시자에서 실행 [sp_changelogreader_agent](../../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md), 로 지정 하 여 **@publication** 하나 이상의 다음 보안 설정을 변경 하려면:  
  
    -   Windows 계정을 변경 하려면 에이전트를 실행 하는 경우 또는이 계정에 대 한 암호만 지정 **@job_login** 및 **@job_password**합니다.  
  
    -   게시자에 연결할 때 사용 되는 보안 모드를 변경 하려면 값을 지정 **1** 또는 **0** 에 대 한 **@publisher_security_mode**합니다.  
  
    -   게시자에 연결할 때 사용 되는 보안 모드를 변경 하는 경우 **1** 에 **0** 변경 하는 경우 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인이이 연결에 사용 되는, 지정 **@publisher_login** 및 **@publisher_password**합니다.  
  
    > [!NOTE]  
    >  에이전트 로그인 또는 암호를 변경한 후 에이전트를 중지하고 다시 시작해야 변경 내용이 적용됩니다.  
  
    > [!IMPORTANT]  
    >  모든 매개 변수에 대해 제공 된 값 원격 배포자로 게시자를 구성할 경우 포함 하 여 *job_login* 및 *job_password*, 를 일반 텍스트로 배포자에 보내집니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 참조 [#40; 및 데이터베이스 엔진에 암호화 된 연결 사용 SQL Server 구성 관리자 및 #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)합니다.  
  
#### 밀어넣기 구독에 대한 배포 에이전트의 보안 설정을 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_helpsubscription](../../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md), 로 지정 하 여 **@publication** 및 **@subscriber**합니다. 이렇게 하면 배포자에서 실행되는 배포 에이전트에 대한 보안 설정을 포함하는 구독 속성이 반환됩니다.  
  
2.  게시 데이터베이스의 게시자에서 실행 [sp_changesubscription](../../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md), 로 지정 하 여 **@publication**, **@subscriber**, **@subscriber_db**, 값이 **모든** 에 대 한 **@article**, 에 대 한 보안 속성의 이름을 **@property**, 및에 대 한 속성의 새 값 **@value**합니다.  
  
3.  변경할 다음 각 보안 속성에 대해 2단계를 반복합니다.  
  
    -   에이전트를 실행 하거나 Windows 계정을 변경 하려면이 계정에 대 한 암호의 값을 지정 **distrib_job_password** 에 대 한 **@property** 및 새 암호를 **@value**합니다. 계정 자체를 변경할 때는 값을 지정 하는 2 단계를 반복 **distrib_job_login** 에 대 한 **@property** 및에 대 한 새 Windows 계정을 **@value**합니다.  
  
    -   구독자에 연결할 때 사용 되는 보안 모드를 변경 하려면 값을 지정 **subscriber_security_mode** 에 대 한 **@property** 값 **1** (Windows 통합 인증) 또는 **0** (SQL Server 인증)에 대 한 **@value**합니다.  
  
    -   구독자 보안 모드를 SQL Server 인증으로 변경 하는 경우 또는 SQL Server 인증에 대 한 로그인 정보를 변경 하는 경우에 값을 지정 **subscriber_password** 에 대 한 **@property** 및 새 암호를 **@value**합니다. 2 단계를 반복, 값을 지정 하면 **subscriber_login** 에 대 한 **@property** 하 고 새 로그인을 **@value**합니다.  
  
    > [!NOTE]  
    >  에이전트 로그인 또는 암호를 변경한 후 에이전트를 중지하고 다시 시작해야 변경 내용이 적용됩니다.  
  
    > [!IMPORTANT]  
    >  모든 속성에 제공 된 값 원격 배포자로 게시자를 구성할 경우 포함 하 여 **distrib_job_login** 및 **distrib_job_password**, 를 일반 텍스트로 배포자에 보내집니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 참조 [#40; 및 데이터베이스 엔진에 암호화 된 연결 사용 SQL Server 구성 관리자 및 #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)합니다.  
  
#### 끌어오기 구독에 대한 배포 에이전트의 보안 설정을 변경하려면  
  
1.  구독자에서 실행 [sp_helppullsubscription](../../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md), 로 지정 하 여 **@publication**합니다. 이렇게 하면 구독자에서 실행되는 배포 에이전트에 대한 보안 설정을 포함하는 구독 속성이 반환됩니다.  
  
2.  구독 데이터베이스의 구독자에서 실행 [sp_change_subscription_properties](../../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md), 로 지정 하 여 **@publisher**, **@publisher_db**, **@publication**, 에 대 한 보안 속성의 이름을 **@property**, 및에 대 한 속성의 새 값 **@value**합니다.  
  
3.  변경할 다음 각 보안 속성에 대해 2단계를 반복합니다.  
  
    -   에이전트를 실행 하거나 Windows 계정을 변경 하려면이 계정에 대 한 암호의 값을 지정 **distrib_job_password** 에 대 한 **@property** 및 새 암호를 **@value**합니다. 계정 자체를 변경할 때는 값을 지정 하는 2 단계를 반복 **distrib_job_login** 에 대 한 **@property** 및에 대 한 새 Windows 계정을 **@value**합니다.  
  
    -   배포자에 연결할 때 사용 되는 보안 모드를 변경 하려면 값을 지정 **distributor_security_mode** 에 대 한 **@property** 값 **1** (Windows 통합 인증) 또는 **0** (SQL Server 인증)에 대 한 **@value**합니다.  
  
    -   SQL Server 인증으로 배포자 보안 모드를 변경할 때 또는 SQL Server 인증에 대 한 로그인 정보를 변경 하는 경우에 값을 지정 **distributor_password** 에 대 한 **@property** 및 새 암호를 **@value**합니다. 2 단계를 반복, 값을 지정 하면 **distributor_login** 에 대 한 **@property** 하 고 새 로그인을 **@value**합니다.  
  
    > [!NOTE]  
    >  에이전트 로그인 또는 암호를 변경한 후 에이전트를 중지하고 다시 시작해야 변경 내용이 적용됩니다.  
  
#### 밀어넣기 구독에 대한 병합 에이전트의 보안 설정을 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_helpmergesubscription](../../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md), 로 지정 하 여 **@publication**, **@subscriber**, 및 **@subscriber_db**합니다. 이렇게 하면 배포자에서 실행되는 병합 에이전트에 대한 보안 설정을 포함하는 구독 속성이 반환됩니다.  
  
2.  게시 데이터베이스의 게시자에서 실행 [sp_changemergesubscription](../../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md), 로 지정 하 여 **@publication**, **@subscriber**, **@subscriber_db**, 에 대 한 보안 속성의 이름을 **@property**, 및에 대 한 속성의 새 값 **@value**합니다.  
  
3.  변경할 다음 각 보안 속성에 대해 2단계를 반복합니다.  
  
    -   에이전트가 실행 되는, 또는 단순히 Windows 계정을 변경 하려면이 계정에 대 한 암호의 값을 지정 **merge_job_password** 에 대 한 **@property** 및 새 암호를 **@value**합니다. 계정 자체를 변경할 때는 값을 지정 하는 2 단계를 반복 **merge_job_login** 에 대 한 **@property** 및에 대 한 새 Windows 계정을 **@value**합니다.  
  
    -   구독자에 연결할 때 사용 되는 보안 모드를 변경 하려면 값을 지정 **subscriber_security_mode** 에 대 한 **@property** 값 **1** (Windows 통합 인증) 또는 **0** (SQL Server 인증)에 대 한 **@value**합니다.  
  
    -   구독자 보안 모드를 SQL Server 인증으로 변경 하는 경우 또는 SQL Server 인증에 대 한 로그인 정보를 변경 하는 경우에 값을 지정 **subscriber_password** 에 대 한 **@property** 및 새 암호를 **@value**합니다. 2 단계를 반복, 값을 지정 하면 **subscriber_login** 에 대 한 **@property** 하 고 새 로그인을 **@value**합니다.  
  
    -   게시자에 연결할 때 사용 되는 보안 모드를 변경 하려면 값을 지정 **publisher_security_mode** 에 대 한 **@property** 값 **1** (Windows 통합 인증) 또는 **0** (SQL Server 인증)에 대 한 **@value**합니다.  
  
    -   게시자 보안 모드를 SQL Server 인증으로 변경 하는 경우 또는 SQL Server 인증에 대 한 로그인 정보를 변경 하는 경우에 값을 지정 **publisher_password** 에 대 한 **@property** 및 새 암호를 **@value**합니다. 2 단계를 반복, 값을 지정 하면 **publisher_login** 에 대 한 **@property** 하 고 새 로그인을 **@value**합니다.  
  
    > [!NOTE]  
    >  에이전트 로그인 또는 암호를 변경한 후 에이전트를 중지하고 다시 시작해야 변경 내용이 적용됩니다.  
  
    > [!IMPORTANT]  
    >  모든 속성에 제공 된 값 원격 배포자로 게시자를 구성할 경우 포함 하 여 **merge_job_login** 및 **merge_job_password**, 를 일반 텍스트로 배포자에 보내집니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 참조 [#40; 및 데이터베이스 엔진에 암호화 된 연결 사용 SQL Server 구성 관리자 및 #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)합니다.  
  
#### 끌어오기 구독에 대한 병합 에이전트의 보안 설정을 변경하려면  
  
1.  구독자에서 실행 [sp_helpmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md), 로 지정 하 여 **@publication**합니다. 이렇게 하면 구독자에서 실행되는 병합 에이전트에 대한 보안 설정을 포함하는 구독 속성이 반환됩니다.  
  
2.  구독 데이터베이스의 구독자에서 실행 [sp_change_subscription_properties](../../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md), 로 지정 하 여 **@publisher**, **@publisher_db**, **@publication**, 에 대 한 보안 속성의 이름을 **@property**, 및에 대 한 속성의 새 값 **@value**합니다.  
  
3.  변경할 다음 각 보안 속성에 대해 2단계를 반복합니다.  
  
    -   이 계정에 대 한 암호의 값을 지정 하거나 에이전트가 실행 되는 Windows 계정을 변경 하려면 **merge_job_password** 에 대 한 **@property** 및 새 암호를 **@value**합니다. 계정 자체를 변경할 때는 값을 지정 하는 2 단계를 반복 **merge_job_login** 에 대 한 **@property** 및에 대 한 새 Windows 계정을 **@value**합니다.  
  
    -   배포자에 연결할 때 사용 되는 보안 모드를 변경 하려면 값을 지정 **distributor_security_mode** 에 대 한 **@property** 값 **1** (Windows 통합 인증) 또는 **0** (SQL Server 인증)에 대 한 **@value**합니다.  
  
    -   SQL Server 인증으로 배포자 보안 모드를 변경할 때 또는 SQL Server 인증에 대 한 로그인 정보를 변경 하는 경우에 값을 지정 **distributor_password** 에 대 한 **@property** 및 새 암호를 **@value**합니다. 2 단계를 반복, 값을 지정 하면 **distributor_login** 에 대 한 **@property** 하 고 새 로그인을 **@value**합니다.  
  
    -   게시자에 연결할 때 사용 되는 보안 모드를 변경 하려면 값을 지정 **publisher_security_mode** 에 대 한 **@property** 값 **1** (Windows 통합 인증) 또는 **0** (SQL Server 인증)에 대 한 **@value**합니다.  
  
    -   SQL Server 인증으로 게시자 보안 모드를 변경할 때 또는 SQL Server 인증에 대 한 로그인 정보를 변경 하는 경우에 값을 지정 **publisher_password** 에 대 한 **@property** 및 새 암호를 **@value**합니다. 2 단계를 반복, 값을 지정 하면 **publisher_login** 에 대 한 **@property** 하 고 새 로그인을 **@value**합니다.  
  
    > [!NOTE]  
    >  에이전트 로그인 또는 암호를 변경한 후 에이전트를 중지하고 다시 시작해야 변경 내용이 적용됩니다.  
  
#### 구독자에 대한 필터링된 스냅숏을 생성하도록 스냅숏 에이전트의 보안 설정을 변경하려면  
  
1.  게시자에서 실행 [sp_helpdynamicsnapshot_job](../../../relational-databases/system-stored-procedures/sp-helpdynamicsnapshot-job-transact-sql.md), 로 지정 하 여 **@publication**합니다. 결과 집합의 값을 확인 **job_name** 변경할 구독자의 파티션에 대 한 합니다.  
  
2.  게시자에서 실행 [sp_changedynamicsnapshot_job](../../../relational-databases/system-stored-procedures/sp-changedynamicsnapshot-job-transact-sql.md), 로 지정 하 여 **@publication**, 에 1 단계에서 얻은 값 **@dynamic_snapshot_jobname**, 및에 대 한 새 암호 **@job_password** 또는 로그인과 암호에는 에이전트가 실행 되는 Windows 계정에 대 한 **@job_login** 및 **@job_password**합니다.  
  
    > [!IMPORTANT]  
    >  모든 매개 변수에 대해 제공 된 값 원격 배포자로 게시자를 구성할 경우 포함 하 여 *job_login* 및 *job_password*, 를 일반 텍스트로 배포자에 보내집니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 참조 [#40; 및 데이터베이스 엔진에 암호화 된 연결 사용 SQL Server 구성 관리자 및 #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)합니다.  
  
#### 큐 판독기 에이전트의 보안 설정을 변경하려면  
  
1.  배포자에서 실행 [sp_helpqreader_agent](../../../relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql.md)합니다. 이렇게 하면 큐 판독기 에이전트가 실행되는 현재 Windows 계정이 반환됩니다.  
  
    -   배포자에서 실행 [sp_changeqreader_agent](../../../relational-databases/system-stored-procedures/sp-changeqreader-agent-transact-sql.md), Windows 계정 설정에 대 한 지정 **@job_login** 및 **@job_passwsord**합니다.  
  
    > [!NOTE]  
    >  에이전트 로그인 또는 암호를 변경한 후 에이전트를 중지하고 다시 시작해야 변경 내용이 적용됩니다. 각 배포 데이터베이스에 대해 하나의 큐 판독기 에이전트가 있습니다. 에이전트에 대한 보안 설정을 변경하면 이 배포 데이터베이스를 사용하는 모든 게시자의 모든 게시 설정이 영향을 받습니다.  
  
2.  큐 판독기 에이전트는 구독에 대한 배포 에이전트와 동일한 연결 컨텍스트를 사용하여 구독자에 연결합니다.  
  
#### 게시자에 연결할 때 즉시 업데이트 구독자에서 사용되는 보안 모드를 변경하려면  
  
1.  구독 데이터베이스의 구독자에서 실행 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md)합니다. 지정 **@publisher**, **@publication**, 에 대 한 게시 데이터베이스의 이름 **@publisher_db**, 는 다음 값 중 하나에 대 한 고 **@security_mode**:  
  
    -   **0** - 게시자에서 업데이트할 때 SQL Server 인증을 사용합니다. 이 옵션을 사용하려면 **@login** 및 **@password**에 대해 게시자에 유효한 로그인을 지정해야 합니다.  
  
    -   **1** - 게시자에 연결할 때 구독자에서 변경 작업을 수행하는 사용자의 보안 컨텍스트를 사용합니다. 참조 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) 이 보안 모드와 관련 된 제한에 대 한 합니다.  
  
    -   **2** 기존를 사용 하려면 사용자 정의 연결 된 서버 로그인 사용 하 여 만든 [sp_addlinkedserver (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)합니다.  
  
#### 원격 배포자에 대한 암호를 변경하려면  
  
1.  배포 데이터베이스의 배포자에서 실행 [sp_changedistributor_password](../../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md), 이 로그인에 대해 새 암호를 지정 하면 **@password**합니다.  
  
    > [!IMPORTANT]  
    >  에 대 한 암호를 변경 하지 마십시오 **distributor_admin** 직접.  
  
2.  이 원격 배포자를 사용 하는 모든 게시자에서 실행 [sp_changedistributor_password](../../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md), 에 1 단계에서 암호를 지정 하면 **@password**합니다.  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 저장해야 하는 경우 [Windows .NET Framework에서 제공하는](http://go.microsoft.com/fwlink/?LinkId=34733) 암호화 서비스 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 를 사용합니다.  
  
#### 복제 서버에 저장된 암호의 모든 인스턴스를 변경하려면  
  
1.  사용 하 여 복제 서버에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 1 단계에서 만든 연결을 사용 하 여 클래스입니다.  
  
3.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeReplicationServerPasswords%2A> 메서드. 다음 매개 변수를 지정합니다.  
  
    -   *security_mode* - <xref:Microsoft.SqlServer.Replication.ReplicationSecurityMode> 암호의 모든 인스턴스는 변경 되는 인증 유형을 지정 하는 값입니다.  
  
    -   *로그인* -로그인 암호의 모든 인스턴스는 변경 합니다.  
  
    -   *암호* -새 암호 값입니다.  
  
        > [!IMPORTANT]  
        >  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 저장해야 하는 경우 Windows .NET Framework에서 제공하는 [암호화 서비스](http://go.microsoft.com/fwlink/?LinkId=34733) 를 사용합니다.  
  
        > [!NOTE]  
        >  구성원만는 **sysadmin** 고정된 서버 역할에서이 메서드를 호출할 수 있습니다.  
  
4.  복제 토폴로지에서 암호를 업데이트해야 하는 모든 서버에 대해 1 - 3단계를 반복합니다.  
  
#### 트랜잭션 게시에 대한 밀어넣기 구독의 배포 에이전트 보안 설정을 변경하려면  
  
1.  사용 하 여 게시자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.TransSubscription> 클래스입니다.  
  
3.  설정의 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, 및 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> 구독 및 설정에 대해 1 단계에서 만든 연결에 대 한 속성의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성입니다.  
  
4.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 3단계에서 구독 속성이 올바르게 정의되지 않았거나 구독이 없는 것입니다.  
  
5.  인스턴스의 다음 보안 속성 중 하나 이상을 설정 <xref:Microsoft.SqlServer.Replication.TransSubscription>:  
  
    -   에이전트가 실행 되는 Windows 계정에 대 한 자격 증명을 변경 하려면는 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 및 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 필드의 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>합니다.  
  
    -   구독자에 연결할 때 에이전트가 사용 하는 인증 유형으로 Windows 통합 인증을 지정 하려면는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 필드는 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 속성을 **true**합니다.  
  
    -   구독자에 연결할 때 에이전트가 사용 하는 인증 유형으로 SQL Server 인증을 지정 하려면는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 필드는 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 속성을 **false**, 구독자 로그인 자격 증명을 지정 하 고는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 및 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 필드.  
  
        > [!NOTE]  
        >  에이전트에 배포자는 항상 연결에 지정 된 Windows 자격 증명을 사용 하 여 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>합니다. 이 계정은 Windows 인증을 사용하여 원격 연결을 만들 때도 사용됩니다.  
  
6.  (선택 사항) 값을 지정한 경우 **true** 에 대 한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, 호출의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드를 서버에 변경 내용을 적용 합니다. 값을 지정한 경우 **false** 에 대 한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (기본값) 이면 변경 내용이 서버에 즉시 보내집니다.  
  
#### 트랜잭션 게시에 대한 끌어오기 구독의 배포 에이전트 보안 설정을 변경하려면  
  
1.  사용 하 여 구독자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 클래스입니다.  
  
3.  설정의 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, 및 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 구독 및 설정에 대해 1 단계에서 만든 연결에 대 한 속성의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성입니다.  
  
4.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 3단계에서 구독 속성이 올바르게 정의되지 않았거나 구독이 없는 것입니다.  
  
5.  인스턴스의 다음 보안 속성 중 하나 이상을 설정 <xref:Microsoft.SqlServer.Replication.TransPullSubscription>:  
  
    -   에이전트가 실행 되는 Windows 계정에 대 한 자격 증명을 변경 하려면는 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 및 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 필드의 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>합니다.  
  
    -   배포자에 연결할 때 에이전트가 사용 하는 인증 유형으로 Windows 통합 인증을 지정 하려면는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 필드는 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 속성을 **true**합니다.  
  
    -   배포자에 연결할 때 에이전트가 사용 하는 인증 유형으로 SQL Server 인증을 지정 하려면는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 필드는 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 속성을 **false**, 에 대 한 배포자 로그인 자격 증명을 지정 하 고는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 및 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 필드입니다.  
  
        > [!NOTE]  
        >  에이전트에 구독자는 항상 연결에 지정 된 Windows 자격 증명을 사용 하 여 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>합니다. 이 계정은 Windows 인증을 사용하여 원격 연결을 만들 때도 사용됩니다.  
  
6.  (선택 사항) 값을 지정한 경우 **true** 에 대 한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, 호출의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드를 서버에 변경 내용을 적용 합니다. 값을 지정한 경우 **false** 에 대 한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (기본값) 이면 변경 내용이 서버에 즉시 보내집니다.  
  
#### 병합 게시에 대한 끌어오기 구독의 병합 에이전트 보안 설정을 변경하려면  
  
1.  사용 하 여 구독자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 클래스입니다.  
  
3.  설정의 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, 및 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 구독 및 설정에 대해 1 단계에서 만든 연결에 대 한 속성의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성입니다.  
  
4.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 3단계에서 구독 속성이 올바르게 정의되지 않았거나 구독이 없는 것입니다.  
  
5.  인스턴스의 다음 보안 속성 중 하나 이상을 설정 <xref:Microsoft.SqlServer.Replication.MergePullSubscription>:  
  
    -   에이전트가 실행 되는 Windows 계정에 대 한 자격 증명을 변경 하려면는 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 및 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 필드의 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>합니다.  
  
    -   배포자에 연결할 때 에이전트가 사용 하는 인증 유형으로 Windows 통합 인증을 지정 하려면는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 필드는 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 속성을 **true**합니다.  
  
    -   배포자에 연결할 때 에이전트가 사용 하는 인증 유형으로 SQL Server 인증을 지정 하려면는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 필드는 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 속성을 **false**, 에 대 한 배포자 로그인 자격 증명을 지정 하 고는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 및 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 필드입니다.  
  
    -   게시자에 연결할 때 에이전트가 사용 하는 인증 유형으로 Windows 통합 인증을 지정 하려면는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 필드는 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> 속성을 **true**합니다.  
  
    -   게시자에 연결할 때 에이전트가 사용 하는 인증 유형으로 SQL Server 인증을 지정 하려면는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 필드는 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> 속성을 **false**, 에 대 한 게시자 로그인 자격 증명을 지정 하 고는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 및 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 필드.  
  
        > [!NOTE]  
        >  에이전트에 구독자는 항상 연결에 지정 된 Windows 자격 증명을 사용 하 여 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>합니다. 이 계정은 Windows 인증을 사용하여 원격 연결을 만들 때도 사용됩니다.  
  
6.  (선택 사항) 값을 지정한 경우 **true** 에 대 한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, 호출의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드를 서버에 변경 내용을 적용 합니다. 값을 지정한 경우 **false** 에 대 한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (기본값) 이면 변경 내용이 서버에 즉시 보내집니다.  
  
#### 병합 게시에 대한 밀어넣기 구독의 병합 에이전트 보안 설정을 변경하려면  
  
1.  사용 하 여 게시자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 클래스입니다.  
  
3.  설정의 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, 및 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> 구독 및 설정에 대해 1 단계에서 만든 연결에 대 한 속성의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성입니다.  
  
4.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 3단계에서 구독 속성이 올바르게 정의되지 않았거나 구독이 없는 것입니다.  
  
5.  인스턴스의 다음 보안 속성 중 하나 이상을 설정 <xref:Microsoft.SqlServer.Replication.MergeSubscription>:  
  
    -   에이전트가 실행 되는 Windows 계정에 대 한 자격 증명을 변경 하려면는 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 및 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 필드의 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>합니다.  
  
    -   구독자에 연결할 때 에이전트가 사용 하는 인증 유형으로 Windows 통합 인증을 지정 하려면는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 필드는 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 속성을 **true**합니다.  
  
    -   구독자에 연결할 때 에이전트가 사용 하는 인증 유형으로 SQL Server 인증을 지정 하려면는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 필드는 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 속성을 **false**, 구독자 로그인 자격 증명을 지정 하 고는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 및 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 필드.  
  
    -   게시자에 연결할 때 에이전트가 사용 하는 인증 유형으로 Windows 통합 인증을 지정 하려면는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 필드는 <xref:Microsoft.SqlServer.Replication.MergeSubscription.PublisherSecurity%2A> 속성을 **true**합니다.  
  
    -   게시자에 연결할 때 에이전트가 사용 하는 인증 유형으로 SQL Server 인증을 지정 하려면는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 필드는 <xref:Microsoft.SqlServer.Replication.MergeSubscription.PublisherSecurity%2A> 속성을 **false**, 에 대 한 게시자 로그인 자격 증명을 지정 하 고는 <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext.SqlStandardLogin%2A> 및 <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext.SqlStandardPassword%2A> 필드.  
  
        > [!NOTE]  
        >  에이전트에 배포자는 항상 연결에 지정 된 Windows 자격 증명을 사용 하 여 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>합니다. 이 계정은 Windows 인증을 사용하여 원격 연결을 만들 때도 사용됩니다.  
  
6.  (선택 사항) 값을 지정한 경우 **true** 에 대 한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, 호출의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드를 서버에 변경 내용을 적용 합니다. 값을 지정한 경우 **false** 에 대 한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (기본값) 이면 변경 내용이 서버에 즉시 보내집니다.  
  
#### 트랜잭션 게시자에 연결할 때 즉시 업데이트 구독자에서 사용하는 로그인 정보를 변경하려면  
  
1.  사용 하 여 구독자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 구독 데이터베이스에 대 한 클래스입니다. 지정 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.Name%2A> 및 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 에 대해 1 단계에서 만든 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>합니다.  
  
3.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 개체의 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 2단계에서 데이터베이스 속성이 잘못 정의되었거나 구독 데이터베이스가 없는 것입니다.  
  
4.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LinkPublicationForUpdateableSubscription%2A> 메서드를 다음 매개 변수를 전달 합니다.  
  
    -   *게시자* -게시자의 이름입니다.  
  
    -   *PublisherDB* -게시 데이터베이스의 이름입니다.  
  
    -   *게시* -즉시 업데이트 구독자가 구독 하는 게시의 이름입니다.  
  
    -   *배포자* -배포자의 이름입니다.  
  
    -   *PublisherSecurity* - <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext> 연결에 대 한 게시자 및 로그인 자격 증명에 연결할 때 즉시 업데이트 구독자에서 사용 하는 보안 모드의 유형을 지정 하는 개체입니다.  
  
###  <a name="PShellExample"></a> 예(RMO)  
 이 예에서는 제공된 로그인 값을 확인하고 서버에서 복제로 저장된 SQL Server 로그인 또는 제공된 Windows 로그인의 모든 암호를 변경합니다.  
  
 [!code-csharp[HowTo#rmo_ChangeServerPasswords](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changeserverpasswords)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeServerPasswords](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changeserverpasswords)]  
  
##  <a name="FollowUp"></a> 후속 작업: 복제 보안 설정 수정 후  
 에이전트 로그인 또는 암호를 변경한 후 에이전트를 중지하고 다시 시작해야 변경 내용이 적용됩니다.  
  
## 참고 항목  
 [복제 관리 개체 개념](../../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [복제 스크립트 & #40; 업그레이드 복제 TRANSACT-SQL 프로그래밍 & #41;](../../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)   
 [복제의 로그인 및 암호 관리](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [복제 에이전트 보안 모델](../../../relational-databases/replication/security/replication-agent-security-model.md)   
 [복제 보안을 위한 최선의 구현 방법](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [보안 및 보호 & #40입니다. 복제 및 #41;](../../../relational-databases/replication/security/security-and-protection-replication.md)   
 [복제 시스템 저장 프로시저 개념](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  