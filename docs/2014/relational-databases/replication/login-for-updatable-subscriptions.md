---
title: 업데이트할 수 있는 구독에 대한 로그인 | Microsoft 문서
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.updatablesubscriptionslogin.f1
ms.assetid: 301ea227-0455-40ba-9009-d38f8676b325
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d8162c7654d99cd2ebab41d290c0a39c6c686686
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63058099"
---
# <a name="login-for-updatable-subscriptions"></a>업데이트할 수 있는 구독에 대한 로그인
  이 마법사의 **업데이트할 수 있는 구독** 페이지에서 **복제** 를 선택한 경우 즉시 업데이트 구독을 위해 게시자에 연결할 때 사용할 계정을 구독자에 지정해야 합니다. 이 연결은 구독자에서 발생되는 트리거에 사용되고 게시자로 변경 내용을 전파합니다. 기본적으로 새 구독 마법사는 필요에 따라 즉시 업데이트로 전환할 수 있는 기능을 사용하여 지연 업데이트를 구성하기 때문에 이 계정은 **업데이트할 수 있는 구독** 페이지에서 **변경 내용 대기 및 가능 시 커밋** 을 선택한 경우에도 필요합니다.  
  
> [!IMPORTANT]  
>  연결에 대해 지정된 계정에는 복제가 게시 데이터베이스에 만드는 뷰에서 데이터를 삽입, 업데이트 및 삭제할 수 있는 사용 권한만 부여하고 다른 추가 사용 권한은 부여하지 않습니다. 각 구독자에서 구성한 계정에 이름이 **syncobj_**_\<HexadecimalNumber>_ 형식으로 지정된 게시 데이터베이스의 뷰에 대한 사용 권한을 부여합니다.  
  
 연결 유형에 대해 3가지 옵션을 사용할 수 있습니다.  
  
-   이미 정의한 연결된 서버나 원격 서버  
  
-   복제가 만드는 연결된 서버 - 이 마법사에서 지정하는 자격 증명으로 연결합니다.  
  
-   복제가 만드는 연결된 서버 - 구독자에서 변경 내용을 적용하는 사용자의 자격 증명으로 연결합니다.  
  
 처음 두 가지 옵션은 이 마법사에서 지정할 수 있습니다. 마지막 옵션은 [sp_link_publication&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql)을 사용해서만 지정할 수 있습니다. 매개 변수 **@security_mode**에 **1** 값을 지정합니다.  
  
## <a name="options"></a>변수  
 **다음 SQL Server 인증을 사용하여 연결되는 연결된 서버 만들기**  
 복제는 **로그인** 및 **암호** 필드에 지정된 자격 증명을 사용하여 연결된 서버를 만듭니다.  
  
 **로그인**  
 이 항목에 설명된 사용 권한만 있는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 입력합니다.  
  
 **암호**  
 **로그인**에서 지정한 로그인에 대한 강력한 암호를 입력합니다.  
  
 **암호 확인**  
 암호를 다시 입력하여 올바로 입력되었는지 확인합니다.  
  
 **이미 정의한 연결된 서버나 원격 서버 사용**  
 이 옵션을 사용하려면 이미 정의한 연결된 서버나 원격 서버가 필요합니다. 자세한 내용은 [연결된 서버&#40;데이터베이스 엔진&#41;](../linked-servers/linked-servers-database-engine.md) 및 [원격 서버](../../database-engine/configure-windows/remote-servers.md)를 참조하세요. 연결된 서버나 원격 서버에 사용된 로그인에 강력한 암호가 있고 이 항목에 설명된 사용 권한만 있는지 확인합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Create an Updatable Subscription to a Transactional Publication](publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [복제 보안 설정 보기 및 수정](security/view-and-modify-replication-security-settings.md)   
 [트랜잭션 복제를 위한 업데이트 가능 구독](transactional/updatable-subscriptions-for-transactional-replication.md)   
 [게시 구독](subscribe-to-publications.md)  
  
  
