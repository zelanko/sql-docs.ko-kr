---
title: "배포자 속성, 게시자 | Microsoft Docs"
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
  - "sql13.rep.configdistwizard.distproperties.publishers.f1"
helpviewer_keywords: 
  - "배포자 속성 대화 상자"
ms.assetid: 31c81898-11ca-4d2f-afea-2fbc71e19ce4
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# 배포자 속성, 게시자
  **배포자 속성** 대화 상자의 **게시자** 페이지를 사용하여 게시자가 이 배포자를 사용하도록 허용할 수 있습니다. 해당 게시자와 연결된 속성을 설정할 수도 있습니다. 현재 서버를 원격 배포자로 사용하도록 게시자를 설정해도 해당 서버가 게시자가 되지는 않습니다. 게시자에 연결하여 이를 게시자로 구성하고, 이 서버를 배포자로 선택해야 합니다. 새 게시 마법사를 통해 게시자를 구성하고 배포자를 선택할 수 있습니다.  
  
## 옵션  
 **게시자**  
 이 배포자를 사용하도록 허용할 서버를 선택합니다. 속성 단추를 클릭 **(...)** 보고 추가 속성을 설정 하는 게시자 옆에 있는 합니다.  
  
 **추가**  
 허용 하려는 서버가 목록, 클릭 **추가** 추가 하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자 또는 Oracle 게시자를 사용할 수 있는 게시자 목록입니다. 추가한 서버가 이 배포자를 원격 배포자로 사용하는 첫 번째 서버이면 관리 연결 암호를 입력하라는 메시지가 표시됩니다.  
  
 **관리 연결 암호**  
 지정 하는 데 사용 또는 사용 하 여 원격 배포자와 게시자 간의 연결 복제에 대 한 암호를 사용 하면 업데이트 된 **distributor_admin** 로그인:  
  
-   배포자가 로컬 배포자로만 사용되는 경우 이 암호는 임의로 생성되고 자동으로 구성됩니다.  
  
-   배포자에 원격 게시자가 있으면 이 페이지 또는 배포 구성 마법사의 **배포자 암호** 페이지에서 암호를 이미 입력한 것입니다.  
  
-   이 배포자에 대해 원격 게시자를 처음으로 설정하는 경우 암호를 입력하라는 메시지가 표시됩니다.  
  
 배포자에 대 한 보안에 자세한 내용은 참조 [배포자 보안 설정](../../relational-databases/replication/security/secure-the-distributor.md)합니다.  
  
## 참고 항목  
 [배포 구성](../../relational-databases/replication/configure-distribution.md)   
 [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [게시 만들기](../../relational-databases/replication/publish/create-a-publication.md)   
 [게시자 및 배포자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)  
  
  