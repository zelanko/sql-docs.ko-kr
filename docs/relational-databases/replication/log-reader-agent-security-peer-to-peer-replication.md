---
title: "로그 판독기 에이전트 보안(피어 투 피어 복제) | Microsoft Docs"
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
  - "sql13.rep.p2pwizard.LRA.f1"
ms.assetid: 6575e2a8-16bb-449c-bdca-4a4202d0972f
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# 로그 판독기 에이전트 보안(피어 투 피어 복제)
  **로그 판독기 에이전트 보안** 페이지를 사용하여 각 피어에서 로그 판독기 에이전트를 실행 및 연결하는 계정을 지정할 수 있습니다. 에이전트 및 복제 보안을 위한 모범 사례에 필요한 사용 권한에 대 한 자세한 내용은 참조 [복제 에이전트 보안 모델](../../relational-databases/replication/security/replication-agent-security-model.md) 및 [복제 보안에 대 한 유용한 정보](../../relational-databases/replication/security/replication-security-best-practices.md)합니다.  
  
> [!NOTE]  
>  트랜잭션 복제를 사용하여 게시된 각 데이터베이스에 대해 하나의 로그 판독기 에이전트가 있습니다. 데이터베이스에 대한 로그 판독기 에이전트가 이미 구성된 경우(이 마법사의 이전 실행에서 게시에 대해 구성했거나 동일한 데이터베이스의 다른 트랜잭션 게시에 대해 구성한 경우) 이 마법사를 통해 데이터베이스가 사용하는 자격 증명을 변경할 수 없습니다. 새 자격 증명을 지정하면 이 자격 증명은 무시됩니다. 자격 증명을 변경하려면 **게시 속성** 대화 상자를 사용하십시오. 자세한 내용은 [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)을(를) 참조하세요.  
  
## 옵션  
 속성 단추를 클릭 (**...**)에 액세스 하려면 각 피어에 대 한 행에는 **로그 판독기 에이전트 보안** 대화 상자입니다. 에이전트가 사용하는 계정에 필요한 사용 권한에 대한 자세한 내용을 보려면 시작한 **로그 판독기 에이전트 보안** 대화 상자에서 **도움말** 을 클릭합니다.  
  
 대화 상자에서 설정을 입력하면 구독자에 대한 연결 정보가 표에 표시됩니다.  
  
 **게시자 에이전트**  
 각 피어 서버 인스턴스의 이름입니다.  
  
 **피어 데이터베이스**  
 각 피어에서 게시 데이터베이스 및 구독 데이터베이스 역할을 하는 데이터베이스입니다.  
  
 **배포자에 대한 연결**  
 배포자에 대한 연결이 설정되는 컨텍스트입니다. 로컬 배포자에는 항상 연결의 컨텍스트를 사용 하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 되므로이 필드는 에이전트가 실행 되는 Windows 계정 **Impersonate ' \< 도메인>\\< 로그인\>'** 또는 **Impersonate ' \< 컴퓨터>\\< 로그인\>'**합니다.  
  
 **게시자에 대한 연결**  
 게시자에 대한 연결을 설정하는 컨텍스트입니다. 게시자에 대한 연결은 에이전트를 실행하는 Windows 계정의 컨텍스트 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 사용하여 설정할 수 있습니다. 필드를 표시 하는 다음 중 하나: **사용 하 여 로그인 ' \< 로그인>'**, **Impersonate ' \< 도메인>\\< 로그인\>'** 또는 **Impersonate ' \< 컴퓨터>\\< 로그인\>'**합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에서는 Windows 계정의 컨텍스트를 사용하여 모든 연결을 설정할 것을 권장합니다.  
  
## 참고 항목  
 [피어 투 피어 토폴로지 & #40; 관리 복제 TRANSACT-SQL 프로그래밍 & #41;](../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [피어 투 피어 트랜잭션 복제](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  