---
title: "Oracle 게시자 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.newpubwizard.selectoraclepublisher.f1
ms.assetid: 019b7c49-dcca-445d-8969-5982a8ccbc1a
caps.latest.revision: "22"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f39e35c81fac3d34cb834ea267ba157a077e2a96
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="oracle-publisher"></a>Oracle 게시자
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 스냅숏과 트랜잭션 복제를 사용하여 Oracle 데이터베이스에서 데이터를 게시할 수 있습니다. 자세한 내용은 [Oracle 게시 개요](../../relational-databases/replication/non-sql/oracle-publishing-overview.md)를 참조하세요.  
  
 Oracle 게시자는 원격 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 배포자를 사용해야 합니다. 이 마법사는 필요한 Oracle 네트워킹 소프트웨어를 설치 및 테스트한 후 해당 서버에서 실행해야 합니다. 자세한 내용은 [Oracle 게시자 구성](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  다른 관리자가 Oracle 데이터베이스를 게시자로 구성한 경우 **다음** 을 클릭하면 Oracle 데이터베이스 연결 시 사용되는 복제 로그인 암호를 입력하라는 메시지가 표시됩니다. 암호를 입력하면[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 Oracle 데이터베이스에 연결된 서버 연결과 사용자 로그인 간 매핑을 만듭니다. 이후에 Oracle 데이터베이스에 연결할 때는 암호를 입력할 필요가 없습니다.  
  
## <a name="options"></a>옵션  
 **Oracle 게시자**  
 목록에서 Oracle 게시자를 선택합니다. 이 목록에는 마법사가 실행 중인 서버를 배포자로 사용하도록 이전에 구성된 Oracle 게시자가 포함되어 있습니다. 목록이 비어 있거나 사용할 Oracle 게시자가 목록에 없으면 **Oracle 게시자 추가**를 클릭합니다.  
  
 **Oracle 게시자 추가**  
 **배포자 속성** 대화 상자를 시작하려면 클릭합니다. 이 대화 상자에서 **추가**를 클릭한 다음 **Oracle 게시자 추가**를 클릭합니다. **서버에 연결** 대화 상자에서 Oracle 서버 이름과 복제 관리 사용자 스키마의 로그인 및 암호를 지정합니다. 자세한 내용은 [서버에 연결&#40;Oracle&#41;, 로그인](../../relational-databases/replication/connect-to-server-oracle-login.md)을 참조하세요.  
  
> [!NOTE]  
>  마법사가 실행 중인 서버가 배포자로 구성되어 있지 않으면 지금 배포자로 구성하라는 메시지가 표시됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Oracle 데이터베이스에서 게시 만들기](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)   
 [속성 참조&#40;복제&#41;](../../relational-databases/replication/properties-reference-replication.md)  
  
  
