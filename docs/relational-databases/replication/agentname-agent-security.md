---
title: "&lt;AgentName&gt; 에이전트 보안 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.agentnameagentsecurity.f1"
ms.assetid: d34c7ef8-cf77-4ffd-887f-3c4214dfd71e
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# &lt;AgentName&gt; 에이전트 보안
   **\< AgentName> 에이전트 보안** 페이지를 사용 하는 계정을 지정할 수 있습니다 (트랜잭션 및 스냅숏 복제의 경우)에 대 한 배포 에이전트 또는 병합 에이전트 (병합 복제의 경우) 실행 하 고 복제 토폴로지의 컴퓨터에 대 한 연결을 확인 합니다. 에이전트 및 복제 보안을 위한 모범 사례에 필요한 사용 권한에 대 한 자세한 내용은 참조 [복제 에이전트 보안 모델](../../relational-databases/replication/security/replication-agent-security-model.md) 및 [복제 보안에 대 한 유용한 정보](../../relational-databases/replication/security/replication-security-best-practices.md)합니다.  
  
## 옵션  
 속성 단추를 클릭 (**...**)에 액세스 하려면 각 구독자에 대 한 행에는 **배포 에이전트 보안** 또는 **병합 에이전트 보안** 대화 상자입니다. 해당 에이전트에서 사용하는 계정에 필요한 사용 권한에 대한 자세한 내용을 보려면 대화 상자에서 **도움말** 을 클릭합니다.  
  
 대화 상자에서 설정을 입력하면 구독자에 대한 연결 정보가 표에 표시됩니다.  
  
 **구독자 에이전트**  
 각 구독자의 이름입니다.  
  
 **배포자에 대한 연결**  
 트랜잭션 및 스냅숏 복제에 대해 표시됩니다. 배포자에 대한 연결이 설정되는 컨텍스트입니다. 로컬 연결은 항상 에이전트가 실행되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정의 컨텍스트를 사용하여 설정됩니다.  
  
-   밀어넣기 구독의 경우 로컬 연결은 연결 이므로 배포자에이 필드는: **Impersonate ' \< 도메인>\\< 로그인\>'** 또는 **Impersonate ' \< 컴퓨터>\\< 로그인\>'** 에 대 한 밀어넣기 구독입니다.  
  
-   끌어오기 구독의 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 컨텍스트로 연결할 수도 있습니다. 필드를 표시 하는 다음 중 하나: **사용 하 여 로그인 ' \< 로그인>'**, **Impersonate ' \< 도메인>\\< 로그인\>'** 또는 **Impersonate ' \< 컴퓨터>\\< 로그인\>'**합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에서는 Windows 계정의 컨텍스트를 사용하여 모든 연결을 설정할 것을 권장합니다.  
  
 **게시자 및 배포자에 연결**  
 병합 복제에 대해 표시됩니다. 게시자 및 배포자에 대한 연결이 설정되는 컨텍스트입니다. 로컬 연결은 항상 에이전트가 실행되는 Windows 계정의 컨텍스트를 사용하여 설정됩니다.  
  
-   밀어넣기 구독의 경우 로컬 연결은 연결 이므로 게시자 및 배포자에이 필드는: **Impersonate ' \< 도메인>\\< 로그인\>'** 또는 **Impersonate ' \< 컴퓨터>\\< 로그인\>'** 에 대 한 밀어넣기 구독입니다.  
  
-   끌어오기 구독의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 컨텍스트로 연결할 수도 있습니다. 필드를 표시 하는 다음 중 하나: **사용 하 여 로그인 ' \< 로그인>'**, **Impersonate ' \< 도메인>\\< 로그인\>'** 또는 **Impersonate ' \< 컴퓨터>\\< 로그인\>'**합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에서는 Windows 계정의 컨텍스트를 사용하여 모든 연결을 설정할 것을 권장합니다.  
  
 **구독자에 대한 연결**  
 구독자에 대한 연결이 설정되는 컨텍스트입니다. 로컬 연결은 항상 에이전트가 실행되는 Windows 계정의 컨텍스트를 사용하여 설정됩니다.  
  
-   끌어오기 구독의 경우 로컬 연결은 연결 이므로 구독자에이 필드는: **Impersonate ' \< 도메인>\\< 로그인\>'** 또는 **Impersonate ' \< 컴퓨터>\\< 로그인\>'** 에 대 한 밀어넣기 구독입니다.  
  
-   밀어넣기 구독의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 컨텍스트로 연결할 수도 있습니다. 필드를 표시 하는 다음 중 하나: **사용 하 여 로그인 ' \< 로그인>'**, **Impersonate ' \< 도메인>\\< 로그인\>'** 또는 **Impersonate ' \< 컴퓨터>\\< 로그인\>'**합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에서는 Windows 계정의 컨텍스트를 사용하여 모든 연결을 설정할 것을 권장합니다.  
  
## 참고 항목  
 [끌어오기 구독 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [밀어넣기 구독 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [복제의 로그인 및 암호 관리](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [복제 에이전트 보안 모델](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [보안 및 보호 & #40입니다. 복제 및 #41;](../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  