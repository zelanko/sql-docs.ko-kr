---
title: 게시 속성, 게시 액세스 목록 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.pubproperties.publicationaccesslist.f1
ms.assetid: 9587bb9e-c66c-4e70-8171-09b943ec2d50
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a9e94541f6c71da9ac40ecd34aacb11d7392b2df
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48224154"
---
# <a name="publication-properties-publication-access-list"></a>게시 속성, 게시 액세스 목록
  **게시 속성** 대화 상자의 **게시 액세스 목록** 페이지를 사용하여 PAL(게시 액세스 목록)에서 로그인, 계정 및 그룹을 추가 및 제거할 수 있습니다. PAL은 게시자의 보안을 유지하는 기본 메커니즘입니다. 게시를 만들면 복제에서 게시에 대한 PAL을 만듭니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 액세스 제어 목록과 기능이 비슷한 PAL에는 게시에 대한 액세스가 부여된 로그인, 계정 및 그룹이 있습니다.  
  
 구독자가 게시자 또는 배포자에 연결하여 게시에 대한 액세스를 요청하면 구독자의 로그인을 PAL의 인증 정보와 비교합니다. 이 방법은 클라이언트 도구가 게시자에서 직접 수정 작업을 수행하는 데 게시자 및 배포자 로그인을 사용하지 못하도록 하여 게시자에 대한 보안을 강화합니다. 자세한 내용은 [게시자 보안 설정](security/secure-the-publisher.md)을 참조하세요.  
  
## <a name="options"></a>변수  
 **추가**  
 새 항목을 목록에 추가합니다. 게시자 및 배포자에서 이미 정의한 로그인, 계정 또는 그룹 이름만 추가할 수 있습니다. 두 서버 모두에서 도메인 계정이 사용되거나 로컬 계정이 생성되면 로그인, 계정 또는 그룹 이름이 두 서버에 정의됩니다.  
  
 **제거**  
 선택한 항목을 목록에서 제거합니다.  
  
 **모두 제거**  
 목록에서 항목을 모두 제거합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Create a Publication](publish/create-a-publication.md)   
 [게시 속성 보기 및 수정](publish/view-and-modify-publication-properties.md)   
 [데이터 및 데이터베이스 개체 게시](publish/publish-data-and-database-objects.md)  
  
  
