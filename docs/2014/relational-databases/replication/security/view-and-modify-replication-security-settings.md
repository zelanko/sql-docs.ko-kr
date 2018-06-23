---
title: 복제 보안 설정 보기 및 수정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- modifying replication security settings
- replication [SQL Server], security
- security [SQL Server replication], viewing settings
- viewing replication security settings
- security [SQL Server replication], modifying settings
ms.assetid: 67d79532-1482-4de1-ac9f-4a23d162c85e
caps.latest.revision: 46
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: a3f07f5c5cce04561121a03a0c5634c352ae2b36
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36091273"
---
# <a name="view-and-modify-replication-security-settings"></a>복제 보안 설정 보기 및 수정
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 복제 보안 설정을 보고 수정하는 방법에 대해 설명합니다. 예를 들어 게시자에 대한 로그 판독기 에이전트의 연결을 SQL Server 인증에서 Windows 통합 인증으로 변경해야 하거나 Windows 계정 암호가 변경되었을 때 에이전트 작업을 실행하는 데 사용된 자격 증명을 변경해야 할 경우가 있습니다. 각 에이전트에 필요한 사용 권한에 대한 자세한 내용은 [복제 에이전트 보안 모델](replication-agent-security-model.md)을 참조하세요.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 복제 보안 설정을 보고 수정하려면**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
-   **Follow Up:**  [After you modify replication security settings](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   사용되는 저장 프로시저는 에이전트의 유형과 서버 연결의 유형에 따라 다릅니다.  
  
-   사용하는 RMO 클래스 및 속성은 에이전트 유형 및 서버 연결 유형에 따라 달라집니다.  
  
###  <a name="Security"></a> 보안  
 보안을 위해 암호의 실제 값은 복제 저장 프로시저에 의해 반환된 결과 집합에서 마스킹됩니다.  
  
####  <a name="Permissions"></a> Permissions  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 다음 대화 상자에서 보안 설정을 확인하고 수정합니다.  
  
1.  **의** 복제 **폴더에서 사용할 수 있는** 복제 암호 업데이트 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. 복제 토폴로지의 서버에서 Windows 계정이나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 계정의 암호를 변경할 경우 해당 계정을 사용하는 각 에이전트의 암호를 업데이트하지 말고 이 대화 상자를 사용하세요. 두 개 이상의 서버에 있는 에이전트에서 같은 계정을 사용할 경우 각 서버에 연결하고 암호를 변경해야 합니다. 해당 암호를 사용하는 복제가 있는 모든 위치에서 암호가 업데이트됩니다. 연결된 서버와 같은 다른 위치에서는 암호가 업데이트되지 않습니다.  
  
2.  **게시 속성 - \<Publication>** 대화 상자의 **에이전트 보안** 페이지. 이 대화 상자에 액세스하는 방법은 [게시 속성 보기 및 수정](../publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
3.  **구독 속성 - \<Subscription>** 대화 상자. 이 대화 상자에 액세스하는 방법은 [밀어넣기 구독 속성 보기 및 수정](../view-and-modify-push-subscription-properties.md) 및 [끌어오기 구독 속성 보기 및 수정](../view-and-modify-pull-subscription-properties.md)을 참조하세요.  
  
4.  **배포자 속성 - \<Distributor>** 및 **배포 데이터베이스 속성 - \<Database>** 대화 상자. 이러한 대화 상자에 액세스하는 방법은 [View and Modify Distributor and Publisher Properties배포자 및 게시자 속성 보기 및 수정](../view-and-modify-distributor-and-publisher-properties.md)을 참조하세요.  
  
5.  **게시자 속성 - \<Publisher>** 대화 상자. 이 대화 상자에 액세스하는 방법은 [게시자 및 배포자 속성 보기 및 수정](../view-and-modify-distributor-and-publisher-properties.md)을 참조하세요.  
  
#### <a name="to-change-the-password-for-an-account-used-by-one-or-more-agents"></a>하나 이상의 에이전트에서 사용하는 계정의 암호를 변경하려면  
  
1.  SQL Server 계정을 사용하는 경우 이 대화 상자에서 SQL Server 계정 암호도 변경합니다. Windows 계정을 사용하는 경우에는 Windows에서 해당 암호부터 변경합니다. 자세한 내용은 Windows 설명서를 참조하십시오.  
  
    > [!NOTE]  
    >  복제 암호를 변경한 후 해당 암호를 사용하는 각 에이전트를 중지한 다음 다시 시작해야 에이전트에 변경 내용이 적용됩니다.  
  
2.  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 서버에 연결한 다음 해당 서버 노드를 확장합니다.  
  
3.  **복제** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **복제 암호 업데이트**를 클릭합니다.  
  
4.  **복제 암호 업데이트** 대화 상자에서 계정과 새 암호를 지정합니다.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-snapshot-agent"></a>스냅숏 에이전트의 보안 설정을 변경하려면  
  
1.  **게시 속성 - \<게시>** 대화 상자의 **에이전트 보안** 페이지에서 **스냅숏 에이전트** 입력란 옆에 있는 **보안 설정** 단추를 클릭합니다.  
  
2.  **스냅숏 에이전트 보안** 대화 상자에서 에이전트가 실행될 계정을 지정합니다.  
  
    -   **에이전트 계정** 입력란에 새 Windows 계정을 입력합니다.  
  
    -   **암호** 및 **암호 확인** 입력란에 강력한 새 암호를 입력합니다.  
  
3.  에이전트가 배포자에서 게시자로 연결해야 하는 컨텍스트를 지정합니다. **다음 SQL Server 로그인 사용**을 선택하면 로그인도 지정해야 합니다.  
  
    -   **로그인** 입력란에 로그인을 입력합니다.  
  
    -   **암호** 및 **암호 확인** 입력란에 강력한 새 암호를 입력합니다.  
  
    > [!NOTE]  
    >  게시자가 Oracle 게시자이면 **배포자 속성 - \<Distributor>** 대화 상자에서 연결 컨텍스트를 지정합니다. 컨텍스트를 변경할 프로시저에 대한 내용은 아래를 참조하세요.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-log-reader-agent"></a>로그 판독기 에이전트의 보안 설정을 변경하려면  
  
1.  **게시 속성 - \<게시>** 대화 상자의 **에이전트 보안** 페이지에서 **로그 판독기 에이전트** 입력란 옆에 있는 **보안 설정** 단추를 클릭합니다.  
  
2.  **로그 판독기 에이전트 보안** 대화 상자에서 에이전트가 실행될 계정을 지정합니다.  
  
    -   **에이전트 계정** 입력란에 새 Windows 계정을 입력합니다.  
  
    -   **암호** 및 **암호 확인** 입력란에 강력한 새 암호를 입력합니다.  
  
3.  에이전트가 배포자에서 게시자로 연결해야 하는 컨텍스트를 지정합니다. **다음 SQL Server 로그인 사용**을 선택하면 로그인도 지정해야 합니다.  
  
    -   **로그인** 입력란에 로그인을 입력합니다.  
  
    -   **암호** 및 **암호 확인** 입력란에 강력한 새 암호를 입력합니다.  
  
    > [!NOTE]  
    >  게시자가 Oracle 게시자이면 **배포자 속성 - \<Distributor>** 대화 상자에서 연결 컨텍스트를 지정합니다. 다음 프로시저를 사용하여 컨텍스트를 변경합니다.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  게시된 각 데이터베이스에 대해 하나의 로그 판독기 에이전트가 있습니다. 하나의 게시에 있는 에이전트의 보안 설정을 변경하면 게시 데이터베이스에 있는 모든 게시의 설정에 영향을 미치게 됩니다.  
  
#### <a name="to-change-the-context-under-which-the-snapshot-agent-and-log-reader-agent-for-an-oracle-publication-make-connections-to-the-publisher"></a>Oracle 게시에 대한 게시자에 스냅숏 에이전트 및 로그 판독기 에이전트를 연결하는 컨텍스트를 변경하려면  
  
1.  **배포자 속성 - \<Distributor>** 대화 상자의 **게시자** 페이지에서 게시자 옆에 있는 속성 단추(**...**)를 클릭합니다.  
  
2.  **에이전트에서 게시자 연결** 섹션에서 사용자가 구성한 복제 관리 사용자 스키마에서 사용하는 로그인 및 암호를 지정합니다. 자세한 내용은 [Oracle 게시자 구성](../non-sql/configure-an-oracle-publisher.md)을 참조하세요.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-push-subscription"></a>밀어넣기 구독에 대한 배포 에이전트의 보안 설정을 변경하려면  
  
1.  게시자의 **구독 속성 - \<Subscription>** 대화 상자에서 다음과 같이 변경할 수 있습니다.  
  
    -   배포 에이전트를 실행하고 배포자에 배포 에이전트를 연결하는 계정을 변경하려면 **에이전트 프로세스 계정** 행을 클릭한 다음 행에 있는 속성 단추 (**...**)를 클릭합니다. **배포 에이전트 보안** 대화 상자에서 계정과 암호를 지정합니다.  
  
    -   구독자에 배포 에이전트를 연결하는 컨텍스트를 변경하려면 **구독자 연결** 행을 클릭한 다음 행에 있는 속성 단추 (**...**)를 클릭합니다. **연결 정보 입력** 대화 상자에서 컨텍스트를 지정합니다.  
  
         지연 업데이트 구독을 사용할 경우 큐 판독기 에이전트도 구독자에 연결하기 위해 여기에서 지정한 컨텍스트를 사용합니다.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-pull-subscription"></a>끌어오기 구독에 대한 배포 에이전트의 보안 설정을 변경하려면  
  
1.  구독자의 **구독 속성 - \<Subscription>** 대화 상자에서 다음과 같이 변경할 수 있습니다.  
  
    -   배포 에이전트를 실행하고 구독자에 배포 에이전트를 연결하는 계정을 변경하려면 **에이전트 프로세스 계정** 행을 클릭한 다음 행에 있는 속성 단추 (**...**)를 클릭합니다. **배포 에이전트 보안** 대화 상자에서 계정과 암호를 지정합니다.  
  
         지연 업데이트 구독을 사용할 경우 큐 판독기 에이전트도 구독자에 연결하기 위해 여기에서 지정한 컨텍스트를 사용합니다.  
  
    -   배포자에 배포 에이전트를 연결하는 컨텍스트를 변경하려면 **배포자 연결** 행을 클릭한 다음 행에 있는 속성 단추 (**...**)를 클릭합니다. **연결 정보 입력** 대화 상자에서 컨텍스트를 지정합니다.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-push-subscription"></a>밀어넣기 구독에 대한 병합 에이전트의 보안 설정을 변경하려면  
  
1.  게시자의 **구독 속성 - \<Subscription>** 대화 상자에서 다음과 같이 변경할 수 있습니다.  
  
    -   병합 에이전트를 실행하고 게시자 및 배포자에 병합 에이전트를 연결하는 계정을 변경하려면 **에이전트 프로세스 계정** 행을 클릭한 다음 행에 있는 속성 단추 (**...**)를 클릭합니다. **병합 에이전트 보안** 대화 상자에서 계정과 암호를 지정합니다.  
  
    -   구독자에 병합 에이전트를 연결하는 컨텍스트를 변경하려면 **구독자 연결** 행을 클릭한 다음 행에 있는 속성 단추 (**...**)를 클릭합니다. **연결 정보 입력** 대화 상자에서 컨텍스트를 지정합니다.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-pull-subscription"></a>끌어오기 구독에 대한 병합 에이전트의 보안 설정을 변경하려면  
  
1.  구독자의 **구독 속성 - \<Subscription>** 대화 상자에서 다음과 같이 변경할 수 있습니다.  
  
    -   병합 에이전트를 실행하고 구독자에 병합 에이전트를 연결하는 계정을 변경하려면 **에이전트 프로세스 계정** 행을 클릭한 다음 행에 있는 속성 단추 (**...**)를 클릭합니다. **병합 에이전트 보안** 대화 상자에서 계정과 암호를 지정합니다.  
  
    -   게시자 및 배포자에 병합 에이전트를 연결하는 컨텍스트를 변경하려면 **게시자 연결** 행을 클릭한 다음 행에 있는 속성 단추 (**...**)를 클릭합니다. **연결 정보 입력** 대화 상자에서 컨텍스트를 지정합니다.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-the-account-under-which-the-queue-reader-agent-runs"></a>큐 판독기 에이전트가 실행되는 계정을 변경하려면  
  
1.  **배포자 속성 - \<Distributor>** 대화 상자의 **일반** 페이지에서 배포 데이터베이스 옆에 있는 속성(**…**) 단추를 클릭합니다.  
  
2.  **배포 데이터베이스 속성 - \<Database>** 대화 상자에서 **에이전트 프로세스 계정** 입력란 옆에 있는 **보안 설정** 단추를 클릭합니다.  
  
3.  **큐 판독기 에이전트 보안** 대화 상자에서 에이전트를 실행하고 배포자에 에이전트를 연결하는 계정을 지정합니다.  
  
    -   **프로세스 계정** 입력란에 새 Windows 계정을 입력합니다.  
  
    -   **암호** 및 **암호 확인** 입력란에 강력한 새 암호를 입력합니다.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  각 배포 데이터베이스에 대해 하나의 큐 판독기 에이전트가 있습니다. 에이전트에 대한 보안 설정을 변경하면 이 배포 데이터베이스를 사용하는 모든 게시자의 모든 게시 설정이 영향을 받습니다.  
  
#### <a name="to-change-the-context-under-which-the-queue-reader-agent-makes-connections-to-the-publisher"></a>게시자에 큐 판독기 에이전트를 연결하는 컨텍스트를 변경하려면  
  
1.  **배포자 속성 - \<Distributor>** 대화 상자의 **게시자** 페이지에서 게시자 옆에 있는 속성 단추(**...**)를 클릭합니다.  
  
2.  **에이전트에서 게시자 연결** 섹션에서 **에이전트 연결 모드** 옵션에 대해 **에이전트 프로세스 계정 가장** 또는 **SQL Server 인증** 의 값을 지정합니다. **SQL Server 인증**을 지정하면 **로그인** 및 **암호**값도 지정해야 합니다.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  각 배포 데이터베이스에 대해 하나의 큐 판독기 에이전트가 있습니다. 에이전트에 대한 보안 설정을 변경하면 이 배포 데이터베이스를 사용하는 모든 게시자의 모든 게시 설정이 영향을 받습니다.  
  
#### <a name="to-change-the-context-under-which-the-queue-reader-agent-makes-connections-to-the-subscriber"></a>구독자에 큐 판독기 에이전트를 연결하는 컨텍스트를 변경하려면  
  
-   큐 판독기 에이전트는 배포 에이전트가 구독에 연결할 때 사용하는 것과 동일한 연결 컨텍스트를 사용합니다. 자세한 내용은 배포 에이전트에 대한 위의 절차를 참조하세요.  
  
#### <a name="to-change-security-settings-for-an-immediate-updating-pull-subscription"></a>끌어오기 구독 즉시 업데이트에 대한 보안 설정을 변경하려면  
  
1.  구독자의 **구독 속성 - \<Subscription>** 대화 상자에서 **게시자 연결** 행을 클릭한 다음 행에 있는 속성(**…**) 단추를 클릭합니다.  
  
2.  **연결 정보 입력** 대화 상자에서 다음 옵션 중 하나를 선택합니다.  
  
    -   **연결된 서버나 원격 서버의 로그인 사용**. [sp_addserver&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addserver-transact-sql), [sp_addlinkedserver&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql), [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 또는 다른 메서드를 사용하여 구독자와 게시자 간에 원격 서버 또는 연결된 서버를 정의한 경우 이 옵션을 선택합니다.  
  
    -   **다음 로그인 및 암호로 SQL Server 인증 사용**. 구독자와 게시자 간에 원격 서버 또는 연결된 서버를 정의하지 않은 경우 이 옵션을 선택하세요. 복제 시 연결된 서버가 자동으로 생성됩니다. 지정한 계정은 게시자에 이미 있어야 합니다.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  이 프로시저는 구독자에서 변경 내용이 발생하면 복제 트리거가 구독자에서 게시자로 연결할 때 사용하는 메서드를 변경합니다. 즉시 업데이트 구독에 대한 배포 에이전트와 관련된 설정 또한 변경할 수 있습니다. 자세한 내용은 이 항목 앞부분의 절차를 참조하세요.  
>   
>  이 프로시저는 끌어오기 구독에만 적용됩니다. 밀어넣기 구독의 경우 저장 프로시저 [sp_link_publication&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql)을 사용합니다.  
  
#### <a name="to-change-the-password-for-the-administrative-connection-from-the-publisher-to-the-distributor"></a>관리 연결의 암호를 게시자에서 배포자로 변경하려면  
  
1.  **배포자 속성 - \<Distributor>** 대화 상자의 **게시자** 페이지에서 **암호** 및 **암호 확인** 입력란에 강력한 암호를 입력합니다.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
3.  **게시자 속성 - \<Publisher>** 대화 상자의 **일반** 페이지에서 **암호** 및 **암호 확인** 입력란에 강력한 암호를 입력합니다.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
> [!IMPORTANT]  
>  가능한 경우 다음의 모든 절차에서 런타임에 사용자에게 보안 자격 증명을 입력하라는 메시지를 표시하세요. 스크립트 파일에 자격 증명을 저장하는 경우에는 무단으로 액세스하지 못하도록 파일에 보안을 설정해야 합니다.  
  
#### <a name="to-change-all-instances-of-a-stored-password-at-a-replication-server"></a>복제 서버에서 저장된 암호의 모든 인스턴스를 변경하려면  
  
1.  master 데이터베이스의 복제 토폴로지에 있는 서버에서 [sp_changereplicationserverpasswords](/sql/relational-databases/system-stored-procedures/sp-changereplicationserverpasswords-transact-sql)를 실행합니다. **@login**에 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 계정 또는 암호를 변경할 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인을 지정하고 **@password**에 계정이나 로그인에 대한 새 암호를 지정합니다. 이렇게 하면 토폴로지의 다른 서버에 연결할 때 서버의 모든 에이전트에서 사용되는 암호의 모든 인스턴스가 변경됩니다.  
  
    > [!NOTE]  
    >  토폴로지의 특정 서버에 대한 연결(예: 배포자 또는 구독자)의 로그인과 암호만 변경하려면 **@server**를 참조하세요.  
  
2.  암호를 업데이트해야 하는 복제 토폴로지의 모든 서버에서 1단계를 반복합니다.  
  
    > [!NOTE]  
    >  복제 암호를 변경한 후 해당 암호를 사용하는 각 에이전트를 중지한 다음 다시 시작해야 에이전트에 변경 내용이 적용됩니다.  
  
#### <a name="to-change-security-settings-for-the-snapshot-agent"></a>스냅숏 에이전트의 보안 설정을 변경하려면  
  
1.  게시자에서 [sp_helppublication_snapshot](/sql/relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql)을 실행하고 **@publication**를 참조하세요. 이렇게 하면 스냅숏 에이전트에 대한 현재 보안 설정이 반환됩니다.  
  
2.  게시자에서 [sp_changepublication_snapshot](/sql/relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql)을 실행하고 **@publication** 및 다음 중 변경할 보안 설정을 하나 이상 지정합니다.  
  
    -   에이전트가 실행되는 Windows 계정을 변경하거나 이 계정에 대한 암호만 변경하려면 **@job_login** 및 **@job_password**를 참조하세요.  
  
    -   게시자에 연결할 때 사용되는 보안 모드를 변경하려면 **@publisher_security_mode** 옵션에 대해 **1** 또는 **@publisher_security_mode**를 참조하세요.  
  
    -   게시자 연결할 때 사용되는 보안 모드를 **@publisher_security_mode** 에서 **1** 으로 변경하는 경우 또는 이 연결에 사용되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인을 변경하는 경우에는 **@publisher_login** 및 **@publisher_password**를 참조하세요.  
  
    > [!IMPORTANT]  
    >  게시자를 원격 배포자로 구성할 경우 *job_login* 및 *job_password*를 비롯한 모든 매개 변수에 제공된 값이 일반 텍스트로 배포자에게 전송됩니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
#### <a name="to-change-security-settings-for-the-log-reader-agent"></a>로그 판독기 에이전트의 보안 설정을 변경하려면  
  
1.  게시자에서 [sp_helplogreader_agent](/sql/relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql)을 실행하고 **@publisher**를 참조하세요. 이렇게 하면 로그 판독기 에이전트에 대한 현재 보안 설정이 반환됩니다.  
  
2.  게시자에서 [sp_changelogreader_agent](/sql/relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql)을 실행하고 **@publication** 및 다음 중 변경할 보안 설정을 하나 이상 지정합니다.  
  
    -   에이전트가 실행되는 Windows 계정을 변경하거나 이 계정에 대한 암호만 변경하려면 **@job_login** 및 **@job_password**를 참조하세요.  
  
    -   게시자에 연결할 때 사용되는 보안 모드를 변경하려면 **@publisher_security_mode** 옵션에 대해 **1** 또는 **@publisher_security_mode**를 참조하세요.  
  
    -   게시자 연결할 때 사용되는 보안 모드를 **@publisher_security_mode** 에서 **1** 으로 변경하는 경우 또는 이 연결에 사용되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인을 변경하는 경우에는 **@publisher_login** 및 **@publisher_password**를 참조하세요.  
  
    > [!NOTE]  
    >  에이전트 로그인 또는 암호를 변경한 후 에이전트를 중지하고 다시 시작해야 변경 내용이 적용됩니다.  
  
    > [!IMPORTANT]  
    >  게시자를 원격 배포자로 구성할 경우 *job_login* 및 *job_password*를 비롯한 모든 매개 변수에 제공된 값이 일반 텍스트로 배포자에게 전송됩니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-push-subscription"></a>밀어넣기 구독에 대한 배포 에이전트의 보안 설정을 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql)을 실행하고 **@publication** 및 **@subscriber**를 참조하세요. 이렇게 하면 배포자에서 실행되는 배포 에이전트에 대한 보안 설정을 포함하는 구독 속성이 반환됩니다.  
  
2.  게시 데이터베이스의 게시자에서 [sp_changesubscription](/sql/relational-databases/system-stored-procedures/sp-changesubscription-transact-sql)을 실행하고 **@publication**또는 RMO(복제 관리 개체)를 사용하여 **@subscriber**또는 RMO(복제 관리 개체)를 사용하여 **@subscriber_db**를 지정하고, **@article** 또는 **@article**값을, **@property**에 보안 속성의 이름을, **@value**를 참조하세요.  
  
3.  변경할 다음 각 보안 속성에 대해 2단계를 반복합니다.  
  
    -   에이전트가 실행되는 Windows 계정을 변경하거나 이 계정에 대한 암호만 변경하려면 **@property** 또는 **@property** 값을 지정하고 **@value**를 참조하세요. 계정 자체를 변경하는 경우 **@property** 또는 **@property** 값을, **@value**를 참조하세요.  
  
    -   구독자에 연결하는 데 사용되는 보안 모드를 변경하려면 **@property** 또는 **@property** 값, **@publisher_security_mode** 에 **1** (Windows 통합 인증) 또는 **@value**를 참조하세요.  
  
    -   구독자 보안 모드를 SQL Server 인증으로 변경하거나 SQL Server 인증에 대한 로그인 정보를 변경하는 경우 **@property** 또는 **@property** 값을 지정하고 **@value**를 참조하세요. 2단계를 반복하고 **@property** 또는 **@property** 값을, **@value**를 참조하세요.  
  
    > [!NOTE]  
    >  에이전트 로그인 또는 암호를 변경한 후 에이전트를 중지하고 다시 시작해야 변경 내용이 적용됩니다.  
  
    > [!IMPORTANT]  
    >  원격 배포자로 게시자를 구성할 경우 **distrib_job_login** 및 **distrib_job_password**를 포함하여 모든 속성에 제공된 값이 일반 텍스트로 배포자에 보내집니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-pull-subscription"></a>끌어오기 구독에 대한 배포 에이전트의 보안 설정을 변경하려면  
  
1.  구독자에서 [sp_helppullsubscription](/sql/relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql)을 실행하고 **@publication**를 참조하세요. 이렇게 하면 구독자에서 실행되는 배포 에이전트에 대한 보안 설정을 포함하는 구독 속성이 반환됩니다.  
  
2.  구독 데이터베이스의 구독자에서 [sp_change_subscription_properties](/sql/relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql)을 실행하고 **@publisher**또는 RMO(복제 관리 개체)를 사용하여 **@publisher_db**또는 RMO(복제 관리 개체)를 사용하여 **@publication**값을, **@property**에 보안 속성의 이름을, **@value**를 참조하세요.  
  
3.  변경할 다음 각 보안 속성에 대해 2단계를 반복합니다.  
  
    -   에이전트가 실행되는 Windows 계정을 변경하거나 이 계정에 대한 암호만 변경하려면 **@property** 또는 **@property** 값을 지정하고 **@value**를 참조하세요. 계정 자체를 변경하는 경우 **@property** 또는 **@property** 값을, **@value**를 참조하세요.  
  
    -   배포자에 연결하는 데 사용되는 보안 모드를 변경하려면 **@property** 또는 **@property** 값, **@publisher_security_mode** 에 **1** (Windows 통합 인증) 또는 **@value**를 참조하세요.  
  
    -   배포자 보안 모드를 SQL Server 인증으로 변경하거나 SQL Server 인증에 대한 로그인 정보를 변경하는 경우 **@property** 또는 **@property** 값을 지정하고 **@value**를 참조하세요. 2단계를 반복하고 **@property** 또는 **@property** 값을, **@value**를 참조하세요.  
  
    > [!NOTE]  
    >  에이전트 로그인 또는 암호를 변경한 후 에이전트를 중지하고 다시 시작해야 변경 내용이 적용됩니다.  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-push-subscription"></a>밀어넣기 구독에 대한 병합 에이전트의 보안 설정을 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_helpmergesubscription](/sql/relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql)을 실행하고 **@publication**또는 RMO(복제 관리 개체)를 사용하여 **@subscriber**및 **@subscriber_db**를 참조하세요. 이렇게 하면 배포자에서 실행되는 병합 에이전트에 대한 보안 설정을 포함하는 구독 속성이 반환됩니다.  
  
2.  게시 데이터베이스의 게시자에서 [sp_changemergesubscription](/sql/relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql)을 실행하고 **@publication**또는 RMO(복제 관리 개체)를 사용하여 **@subscriber**또는 RMO(복제 관리 개체)를 사용하여 **@subscriber_db**값을, **@property**에 보안 속성의 이름을, **@value**를 참조하세요.  
  
3.  변경할 다음 각 보안 속성에 대해 2단계를 반복합니다.  
  
    -   에이전트가 실행되는 Windows 계정을 변경하거나 이 계정에 대한 암호만 변경하려면 **@property** 또는 **@property** 값을 지정하고 **@value**를 참조하세요. 계정 자체를 변경하는 경우 **@property** 또는 **@property** 값을, **@value**를 참조하세요.  
  
    -   구독자에 연결하는 데 사용되는 보안 모드를 변경하려면 **@property** 또는 **@property** 값, **@publisher_security_mode** 에 **1** (Windows 통합 인증) 또는 **@value**를 참조하세요.  
  
    -   구독자 보안 모드를 SQL Server 인증으로 변경하거나 SQL Server 인증에 대한 로그인 정보를 변경하는 경우 **@property** 또는 **@property** 값을 지정하고 **@value**를 참조하세요. 2단계를 반복하고 **@property** 또는 **@property** 값을, **@value**를 참조하세요.  
  
    -   게시자에 연결할 때 사용되는 보안 모드를 변경하려면 **@property** 또는 **@property** 값, **@publisher_security_mode** 에 **1** (Windows 통합 인증) 또는 **@value**를 참조하세요.  
  
    -   게시자 보안 모드를 SQL Server 인증으로 변경하거나 SQL Server 인증에 대한 로그인 정보를 변경하는 경우 **@property** 또는 **@property** 값을 지정하고 **@value**를 참조하세요. 2단계를 반복하고 **@property** 또는 **@property** 값을, **@value**를 참조하세요.  
  
    > [!NOTE]  
    >  에이전트 로그인 또는 암호를 변경한 후 에이전트를 중지하고 다시 시작해야 변경 내용이 적용됩니다.  
  
    > [!IMPORTANT]  
    >  원격 배포자로 게시자를 구성할 경우 **merge_job_login** 및 **merge_job_password**를 포함하여 모든 속성에 제공된 값이 일반 텍스트로 배포자에 보내집니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-pull-subscription"></a>끌어오기 구독에 대한 병합 에이전트의 보안 설정을 변경하려면  
  
1.  구독자에서 [sp_helpmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql)을 실행하고 **@publication**를 참조하세요. 이렇게 하면 구독자에서 실행되는 병합 에이전트에 대한 보안 설정을 포함하는 구독 속성이 반환됩니다.  
  
2.  구독 데이터베이스의 구독자에서 [sp_change_subscription_properties](/sql/relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql)을 실행하고 **@publisher**또는 RMO(복제 관리 개체)를 사용하여 **@publisher_db**또는 RMO(복제 관리 개체)를 사용하여 **@publication**값을, **@property**에 보안 속성의 이름을, **@value**를 참조하세요.  
  
3.  변경할 다음 각 보안 속성에 대해 2단계를 반복합니다.  
  
    -   에이전트가 실행되는 Windows 계정을 변경하거나 이 계정에 대한 암호만 변경하려면 **@property** 또는 **@property** 값을 지정하고 **@value**를 참조하세요. When changing the account itself, repeat Step 2 specifying a value of **@property** 또는 **@property** 값을, **@value**를 참조하세요.  
  
    -   배포자에 연결하는 데 사용되는 보안 모드를 변경하려면 **@property** 또는 **@property** 값, **@publisher_security_mode** 에 **1** (Windows 통합 인증) 또는 **@value**를 참조하세요.  
  
    -   배포자 보안 모드를 SQL Server 인증으로 변경하거나 SQL Server 인증에 대한 로그인 정보를 변경하는 경우 **@property** 또는 **@property** 값을 지정하고 **@value**를 참조하세요. 2단계를 반복하고 **@property** 또는 **@property** 값을, **@value**를 참조하세요.  
  
    -   게시자에 연결할 때 사용되는 보안 모드를 변경하려면 **@property** 또는 **@property** 값, **@publisher_security_mode** 에 **1** (Windows 통합 인증) 또는 **@value**를 참조하세요.  
  
    -   게시자 보안 모드를 SQL Server 인증으로 변경하거나 SQL Server 인증에 대한 로그인 정보를 변경하는 경우 **@property** 또는 **@property** 값을 지정하고 **@value**를 참조하세요. 2단계를 반복하고 **@property** 또는 **@property** 값을, **@value**를 참조하세요.  
  
    > [!NOTE]  
    >  에이전트 로그인 또는 암호를 변경한 후 에이전트를 중지하고 다시 시작해야 변경 내용이 적용됩니다.  
  
#### <a name="to-change-security-settings-for-the-snapshot-agent-to-generate-a-filtered-snapshot-for-a-subscriber"></a>구독자에 대한 필터링된 스냅숏을 생성하도록 스냅숏 에이전트의 보안 설정을 변경하려면  
  
1.  게시자에서 [sp_helpdynamicsnapshot_job](/sql/relational-databases/system-stored-procedures/sp-helpdynamicsnapshot-job-transact-sql)을 실행하고 **@publication**를 참조하세요. 결과 집합에서 변경할 구독자 파티션의 **job_name** 값을 확인합니다.  
  
2.  게시자에서 [sp_changedynamicsnapshot_job](/sql/relational-databases/system-stored-procedures/sp-changedynamicsnapshot-job-transact-sql)을 실행하고 **@publication**을 지정하고 **@dynamic_snapshot_jobname**에 1단계에서 얻은 값을, **@job_password** 에 새 암호를, **@job_login** 및 **@job_password**를 참조하세요.  
  
    > [!IMPORTANT]  
    >  게시자를 원격 배포자로 구성할 경우 *job_login* 및 *job_password*를 비롯한 모든 매개 변수에 제공된 값이 일반 텍스트로 배포자에게 전송됩니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
#### <a name="to-change-security-settings-for-the-queue-reader-agent"></a>큐 판독기 에이전트의 보안 설정을 변경하려면  
  
1.  배포자에서 [sp_helpqreader_agent](/sql/relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql)를 실행합니다. 이렇게 하면 큐 판독기 에이전트가 실행되는 현재 Windows 계정이 반환됩니다.  
  
    -   배포자에서 [sp_changeqreader_agent](/sql/relational-databases/system-stored-procedures/sp-changeqreader-agent-transact-sql)를 실행하고 **@job_login** 및 **@job_passwsord**를 참조하세요.  
  
    > [!NOTE]  
    >  에이전트 로그인 또는 암호를 변경한 후 에이전트를 중지하고 다시 시작해야 변경 내용이 적용됩니다. 각 배포 데이터베이스에 대해 하나의 큐 판독기 에이전트가 있습니다. 에이전트에 대한 보안 설정을 변경하면 이 배포 데이터베이스를 사용하는 모든 게시자의 모든 게시 설정이 영향을 받습니다.  
  
2.  큐 판독기 에이전트는 구독에 대한 배포 에이전트와 동일한 연결 컨텍스트를 사용하여 구독자에 연결합니다.  
  
#### <a name="to-change-security-mode-used-by-an-immediate-updating-subscriber-when-connecting-to-the-publisher"></a>게시자에 연결할 때 즉시 업데이트 구독자에서 사용되는 보안 모드를 변경하려면  
  
1.  구독 데이터베이스의 구독자에서 [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql)을 실행합니다. **@publisher**, **@publication**, **@publisher_db**에 대한 게시 데이터베이스 이름을 지정하고 **@security_mode**에 다음 값 중 하나를 지정합니다.  
  
    -   **0** - 게시자에서 업데이트할 때 SQL Server 인증을 사용합니다. 이 옵션을 사용하려면 **@login** 및 **@password**를 참조하세요.  
  
    -   **1** - 게시자에 연결할 때 구독자에서 변경 작업을 수행하는 사용자의 보안 컨텍스트를 사용합니다. 이 보안 모드에 관한 제한 사항에 대해서는 [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql) 을 참조하세요.  
  
    -   **2** - [sp_addlinkedserver&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)를 사용하여 만든 기존의 사용자 정의 연결된 서버 로그인을 사용합니다.  
  
#### <a name="to-change-the-password-for-a-remote-distributor"></a>원격 배포자에 대한 암호를 변경하려면  
  
1.  배포 데이터베이스의 배포자에서 [sp_changedistributor_password](/sql/relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql)를 실행하고 **@password**를 참조하세요.  
  
    > [!IMPORTANT]  
    >  **distributor_admin** 의 암호를 직접 변경하지 마세요.  
  
2.  이 원격 배포자를 사용하는 모든 게시자에서 [sp_changedistributor_password](/sql/relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql)를 실행하고 **@password**를 참조하세요.  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 저장해야 하는 경우 [Windows .NET Framework에서 제공하는](http://go.microsoft.com/fwlink/?LinkId=34733) 암호화 서비스 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 를 사용합니다.  
  
#### <a name="to-change-all-instances-of-a-password-stored-on-a-replication-server"></a>복제 서버에 저장된 암호의 모든 인스턴스를 변경하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 복제 서버에 대한 연결을 만듭니다.  
  
2.  1단계에서 만든 연결을 사용하여 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 클래스의 인스턴스를 만듭니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeReplicationServerPasswords%2A> 메서드를 호출합니다. 다음 매개 변수를 지정합니다.  
  
    -   *security_mode* - 모든 암호 인스턴스를 변경할 때 사용할 인증 유형을 지정하는 <xref:Microsoft.SqlServer.Replication.ReplicationSecurityMode> 값  
  
    -   *login* - 변경 중인 암호의 모든 인스턴스에 대한 로그인  
  
    -   *password* - 새 암호 값  
  
        > [!IMPORTANT]  
        >  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 저장해야 하는 경우 Windows .NET Framework에서 제공하는 [암호화 서비스](http://go.microsoft.com/fwlink/?LinkId=34733) 를 사용합니다.  
  
        > [!NOTE]  
        >  `sysadmin` 고정 서버 역할의 멤버만 이 메서드를 호출할 수 있습니다.  
  
4.  복제 토폴로지에서 암호를 업데이트해야 하는 모든 서버에 대해 1 - 3단계를 반복합니다.  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-push-subscription-to-a-transactional-publication"></a>트랜잭션 게시에 대한 밀어넣기 구독의 배포 에이전트 보안 설정을 변경하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.TransSubscription> 클래스의 인스턴스를 만듭니다.  
  
3.  구독에 대한 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>및 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> 속성을 설정하고, 1단계에서 만든 연결을 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성에 대해 설정합니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체 속성을 가져옵니다. 이 메서드가 반환 하는 경우 `false`, 3 단계에서 구독 속성이 올바르게 정의 된 또는 구독이 없습니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.TransSubscription>인스턴스의 다음 보안 속성 중 하나 이상을 설정합니다.  
  
    -   에이전트가 실행되는 Windows 계정에 대한 자격 증명을 변경하려면 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 의 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 및 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>필드를 설정합니다.  
  
    -   구독자에 연결할 때 에이전트가 사용하는 인증 유형으로 Windows 통합 인증을 지정하려면 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 속성의 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 필드를 `true`로 설정합니다.  
  
    -   구독자에 연결할 때 에이전트가 사용 하는 인증 유형으로 SQL Server 인증을 지정 하려면는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 필드는 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 속성을 `false`는 에대한구독자로그인자격증명지정<xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 및 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 필드입니다.  
  
        > [!NOTE]  
        >  에이전트는 항상 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>에 지정된 Windows 자격 증명을 사용하여 배포자에 연결합니다. 이 계정은 Windows 인증을 사용하여 원격 연결을 만들 때도 사용됩니다.  
  
6.  (선택 사항) 값을 지정한 경우 `true` 에 대 한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, 호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드는 서버에서 변경 내용을 커밋 하도록 합니다. 값을 지정한 경우 `false` 에 대 한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (기본값) 이면 변경 내용이 서버에 즉시 전송 합니다.  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-pull-subscription-to-a-transactional-publication"></a>트랜잭션 게시에 대한 끌어오기 구독의 배포 에이전트 보안 설정을 변경하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 구독자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 클래스의 인스턴스를 만듭니다.  
  
3.  구독에 대한 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>및 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 속성을 설정하고, 1단계에서 만든 연결을 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성에 대해 설정합니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체 속성을 가져옵니다. 이 메서드가 반환 하는 경우 `false`, 3 단계에서 구독 속성이 올바르게 정의 된 또는 구독이 없습니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.TransPullSubscription>인스턴스의 다음 보안 속성 중 하나 이상을 설정합니다.  
  
    -   에이전트가 실행되는 Windows 계정에 대한 자격 증명을 변경하려면 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 의 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 및 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>필드를 설정합니다.  
  
    -   배포자에 연결할 때 에이전트가 사용하는 인증 유형으로 Windows 통합 인증을 지정하려면 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 속성의 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 필드를 `true`로 설정합니다.  
  
    -   배포자에 연결할 때 에이전트가 사용 하는 인증 유형으로 SQL Server 인증을 지정 하려면는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 필드는 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 속성을 `false`는 에대한배포자로그인자격증명지정<xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 및 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 필드입니다.  
  
        > [!NOTE]  
        >  에이전트는 항상 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>에 지정된 Windows 자격 증명을 사용하여 구독자에 연결합니다. 이 계정은 Windows 인증을 사용하여 원격 연결을 만들 때도 사용됩니다.  
  
6.  (선택 사항) 값을 지정한 경우 `true` 에 대 한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, 호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드는 서버에서 변경 내용을 커밋 하도록 합니다. 값을 지정한 경우 `false` 에 대 한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (기본값) 이면 변경 내용이 서버에 즉시 전송 합니다.  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-pull-subscription-to-a-merge-publication"></a>병합 게시에 대한 끌어오기 구독의 병합 에이전트 보안 설정을 변경하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 구독자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 클래스의 인스턴스를 만듭니다.  
  
3.  구독에 대한 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>및 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 속성을 설정하고, 1단계에서 만든 연결을 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성에 대해 설정합니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체 속성을 가져옵니다. 이 메서드가 반환 하는 경우 `false`, 3 단계에서 구독 속성이 올바르게 정의 된 또는 구독이 없습니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.MergePullSubscription>인스턴스의 다음 보안 속성 중 하나 이상을 설정합니다.  
  
    -   에이전트가 실행되는 Windows 계정에 대한 자격 증명을 변경하려면 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 의 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 및 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>필드를 설정합니다.  
  
    -   배포자에 연결할 때 에이전트가 사용하는 인증 유형으로 Windows 통합 인증을 지정하려면 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 속성의 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 필드를 `true`로 설정합니다.  
  
    -   배포자에 연결할 때 에이전트가 사용 하는 인증 유형으로 SQL Server 인증을 지정 하려면는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 필드는 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 속성을 `false`는 에대한배포자로그인자격증명지정<xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 및 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 필드입니다.  
  
    -   게시자에 연결할 때 에이전트가 사용 하는 인증 유형으로 Windows 통합 인증을 지정 하려면는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 필드는 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> 속성을 `true`합니다.  
  
    -   게시자에 연결할 때 에이전트가 사용 하는 인증 유형으로 SQL Server 인증을 지정 하려면는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 필드는 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> 속성을 `false`는 에대한게시자로그인자격증명지정<xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A>및 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 필드입니다.  
  
        > [!NOTE]  
        >  에이전트는 항상 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>에 지정된 Windows 자격 증명을 사용하여 구독자에 연결합니다. 이 계정은 Windows 인증을 사용하여 원격 연결을 만들 때도 사용됩니다.  
  
6.  (선택 사항) 값을 지정한 경우 `true` 에 대 한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, 호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드는 서버에서 변경 내용을 커밋 하도록 합니다. 값을 지정한 경우 `false` 에 대 한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (기본값) 이면 변경 내용이 서버에 즉시 전송 합니다.  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-push-subscription-to-a-merge-publication"></a>병합 게시에 대한 밀어넣기 구독의 병합 에이전트 보안 설정을 변경하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.MergeSubscription> 클래스의 인스턴스를 만듭니다.  
  
3.  구독에 대한 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>및 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> 속성을 설정하고, 1단계에서 만든 연결을 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성에 대해 설정합니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체 속성을 가져옵니다. 이 메서드가 반환 하는 경우 `false`, 3 단계에서 구독 속성이 올바르게 정의 된 또는 구독이 없습니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.MergeSubscription>인스턴스의 다음 보안 속성 중 하나 이상을 설정합니다.  
  
    -   에이전트가 실행되는 Windows 계정에 대한 자격 증명을 변경하려면 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 의 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 및 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>필드를 설정합니다.  
  
    -   구독자에 연결할 때 에이전트가 사용하는 인증 유형으로 Windows 통합 인증을 지정하려면 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 속성의 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 필드를 `true`로 설정합니다.  
  
    -   구독자에 연결할 때 에이전트가 사용 하는 인증 유형으로 SQL Server 인증을 지정 하려면는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 필드는 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 속성을 `false`는 에대한구독자로그인자격증명지정<xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 및 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 필드입니다.  
  
    -   게시자에 연결할 때 에이전트가 사용 하는 인증 유형으로 Windows 통합 인증을 지정 하려면는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 필드는 <xref:Microsoft.SqlServer.Replication.MergeSubscription.PublisherSecurity%2A> 속성을 `true`합니다.  
  
    -   게시자에 연결할 때 에이전트가 사용 하는 인증 유형으로 SQL Server 인증을 지정 하려면는 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 필드는 <xref:Microsoft.SqlServer.Replication.MergeSubscription.PublisherSecurity%2A> 속성을 `false`는 에대한게시자로그인자격증명지정<xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext.SqlStandardLogin%2A>및 <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext.SqlStandardPassword%2A> 필드입니다.  
  
        > [!NOTE]  
        >  에이전트는 항상 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>에 지정된 Windows 자격 증명을 사용하여 배포자에 연결합니다. 이 계정은 Windows 인증을 사용하여 원격 연결을 만들 때도 사용됩니다.  
  
6.  (선택 사항) 값을 지정한 경우 `true` 에 대 한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, 호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드는 서버에서 변경 내용을 커밋 하도록 합니다. 값을 지정한 경우 `false` 에 대 한 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (기본값) 이면 변경 내용이 서버에 즉시 전송 합니다.  
  
#### <a name="to-change-the-login-information-used-by-an-immediate-updating-subscriber-when-it-connects-to-the-transactional-publisher"></a>트랜잭션 게시자에 연결할 때 즉시 업데이트 구독자에서 사용하는 로그인 정보를 변경하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 구독자 연결을 만듭니다.  
  
2.  구독 데이터베이스에 대한 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 클래스의 인스턴스를 만듭니다. <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.Name%2A> 을 지정하고 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 에 1단계에서 만든 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>을 지정합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체 속성을 가져옵니다. 이 메서드가 반환 하는 경우 `false`, 2 단계에서 데이터베이스 속성이 잘못 정의 된 또는 구독 데이터베이스의 존재 하지 않습니다.  
  
4.  다음 매개 변수를 전달하는 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LinkPublicationForUpdateableSubscription%2A> 메서드를 호출합니다.  
  
    -   *Publisher* - 게시자 이름  
  
    -   *PublisherDB* - 게시 데이터베이스 이름  
  
    -   *Publication* - 즉시 업데이트 구독자가 구독하는 게시 이름  
  
    -   *Distributor* - 배포자 이름  
  
    -   *PublisherSecurity* - A <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext> 개체  
  
###  <a name="PShellExample"></a> 예(RMO)  
 이 예에서는 제공된 로그인 값을 확인하고 서버에서 복제로 저장된 SQL Server 로그인 또는 제공된 Windows 로그인의 모든 암호를 변경합니다.  
  
 [!code-csharp[HowTo#rmo_ChangeServerPasswords](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_changeserverpasswords)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeServerPasswords](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_changeserverpasswords)]  
  
##  <a name="FollowUp"></a> 후속 작업: 복제 보안 설정 수정 후  
 에이전트 로그인 또는 암호를 변경한 후 에이전트를 중지하고 다시 시작해야 변경 내용이 적용됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [Replication Management Objects Concepts](../concepts/replication-management-objects-concepts.md)   
 [복제 스크립트 업그레이드&#40;복제 Transact-SQL 프로그래밍&#41;](../administration/upgrade-replication-scripts-replication-transact-sql-programming.md)   
 [복제의 로그인 및 암호 관리](manage-logins-and-passwords-in-replication.md)   
 [복제 에이전트 보안 모델](replication-agent-security-model.md)   
 [Replication Security Best Practices](replication-security-best-practices.md)   
 [보안 및 보호&#40;복제&#41;](security-and-protection-replication.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)  
  
  
