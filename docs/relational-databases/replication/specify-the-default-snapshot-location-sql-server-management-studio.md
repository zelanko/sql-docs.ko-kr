---
title: "기본 스냅숏 위치 지정(SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "스냅숏 [SQL Server 복제], 기본 위치"
  - "기본 스냅숏 위치"
ms.assetid: 27c5d9ad-a915-4c59-a8b7-82e3af61ac4d
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# 기본 스냅숏 위치 지정(SQL Server Management Studio)
  배포 구성 마법사의 **스냅숏 폴더** 페이지에서 기본 스냅숏 위치를 지정합니다. 이 마법사를 사용 하는 방법에 대 한 자세한 내용은 참조 [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md)합니다. 배포자로 구성되어 있지 않은 서버에서 게시를 만드는 경우 새 게시 마법사의 **스냅숏 폴더** 페이지에서 기본 스냅숏 위치를 지정합니다. 이 마법사를 사용 하는 방법에 대 한 자세한 내용은 참조 [발행물 만들기](../../relational-databases/replication/publish/create-a-publication.md)합니다.  
  
 기본 스냅숏 위치를 수정 된 **게시자** 의 페이지는 **배포자 속성-\< 배포자>** 대화 상자입니다. 자세한 내용은 참조 [보기 및 수정 게시자 및 배포자 속성](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)합니다. 설정에서 각 게시에 대 한 스냅숏 폴더는 **게시 속성-\< 게시>** 대화 상자입니다. 자세한 내용은 [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
### 기본 스냅숏 위치를 수정하려면  
  
1.  에 **게시자** 의 페이지는 **배포자 속성-\< 배포자>** 대화 상자에서 속성 단추를 클릭 (**...**) 기본 스냅숏 위치를 변경 하려면 게시자에 대 한 합니다.  
  
2.  에 **게시자 속성-\< 게시자>** 대화 상자에 대 한 값을 입력 합니다는 **기본 스냅숏 폴더** 속성입니다.  
  
    > [!NOTE]  
    >  스냅숏 에이전트는 지정한 디렉터리에 대해 쓰기 권한이 있어야 하며 배포 에이전트 또는 병합 에이전트는 읽기 권한이 있어야 합니다. 끌어오기 구독을 사용 하는 경우 지정 해야 하는 공유 디렉터리 범용 명명 규칙 (UNC) 경로와 같은 \\\computername\snapshot 합니다. 자세한 내용은 참조 [스냅숏 폴더 보안](../../relational-databases/replication/security/secure-the-snapshot-folder.md)합니다.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## 참고 항목  
 [대체 스냅숏 폴더 위치](../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [스냅숏으로 구독 초기화](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  