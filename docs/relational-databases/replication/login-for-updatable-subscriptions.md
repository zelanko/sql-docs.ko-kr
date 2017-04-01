---
title: "업데이트할 수 있는 구독에 대한 로그인 | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.updatablesubscriptionslogin.f1"
ms.assetid: 301ea227-0455-40ba-9009-d38f8676b325
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 18
---
# 업데이트할 수 있는 구독에 대한 로그인
  즉시 업데이트를 선택한 경우에 대 한 **복제** 에 **업데이트할 수 있는 구독** 페이지가 마법사는 게시자에 연결 된 구독자를 대상으로 계정을 지정 해야 합니다. 
  
 연결은은 구독자에서 발생 하 고 변경 내용을 게시자에 전파 되는 트리거에 사용 됩니다. 이 계정을 선택한 경우에 반드시 **변경 내용 대기 및 가능 시 커밋** 에 **업데이트할 수 있는 구독** 페이지입니다. 기본적으로 새 구독 마법사는 필요한 경우 즉시 업데이트로 전환할 수 있는 지연 업데이트를 구성 합니다.  
  
> **중요!!** 연결 이어야만 대해 지정 된 계정 권한이 삽입, 업데이트 및 삭제 뷰에서 데이터를 복제 하려면 게시 데이터베이스에 만듭니다. 추가 사용 권한을 배정 하지 해야 합니다. 폼에 이름이 지정 된 게시 데이터베이스의 뷰에 대 한 권한을 부여 **syncobj_***\< HexadecimalNumber>* 각 구독자에서 구성한 계정에 있습니다.  
  
 연결 유형에 대해 3가지 옵션을 사용할 수 있습니다.  
  
-   이미 정의한 연결된 서버나 원격 서버  
  
-   복제가 만드는 연결된 서버 - 이 마법사에서 지정하는 자격 증명으로 연결합니다.  
  
-   복제가 만드는 연결된 서버 - 구독자에서 변경 내용을 적용하는 사용자의 자격 증명으로 연결합니다.  
  
 처음 두 가지 옵션은 이 마법사에서 지정할 수 있습니다. 마지막 옵션을 다시 지정를 사용 하 여 [sp_link_publication (& a) #40; TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md); 값을 지정 **1** 매개 변수에 대해 **@security_mode**합니다.  
  
## 옵션  
 **다음 SQL Server 인증을 사용하여 연결되는 연결된 서버 만들기**  
 복제가 만드는 연결된 된 서버에 지정 된 자격 증명을 사용 하 여는 **로그인** 및 **암호** 필드입니다.  
  
 **로그인**  
 입력 한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이 항목에 설명 된 사용 권한만 있는 로그인 합니다.  
  
 **암호**  
 에 지정 된 로그인에 대 한 강력한 암호를 입력 **로그인**합니다.  
    
 **이미 정의한 연결된 서버나 원격 서버 사용**  
 이 옵션을 사용하려면 이미 정의한 연결된 서버나 원격 서버가 필요합니다. 자세한 내용은 참조 [연결 된 서버 &#40; 데이터베이스 엔진 &#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md) 및 [원격 서버](../../database-engine/configure-windows/remote-servers.md)합니다. 연결된 서버나 원격 서버에 사용된 로그인에 강력한 암호가 있고 이 항목에 설명된 사용 권한만 있는지 확인합니다.  
  
## 참고 항목  
 [트랜잭션 게시에 대해 업데이트할 수 있는 구독 만들기](https://msdn.microsoft.com/library/ms152769.aspx)   
 [복제 보안 설정 보기 및 수정](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [트랜잭션 복제를 위한 업데이트 가능 구독](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)  
  
  