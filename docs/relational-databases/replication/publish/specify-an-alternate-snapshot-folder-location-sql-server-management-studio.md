---
title: "대체 스냅숏 폴더 위치 지정(SQL Server Management Studio) | Microsoft Docs"
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
  - "스냅숏 [SQL Server 복제], 대체 폴더 위치"
  - "스냅숏 복제 [SQL Server], 대체 폴더 위치"
  - "대체 스냅숏 폴더 [SQL Server 복제]"
ms.assetid: 9293f0eb-5531-47ec-b6e2-0392823ce5cc
caps.latest.revision: 42
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 42
---
# 대체 스냅숏 폴더 위치 지정(SQL Server Management Studio)
  대체 스냅숏 위치를 지정 된 **스냅숏** 의 페이지는 **게시 속성-\< 게시>** 대화 상자입니다. 이 대화 상자에 액세스하는 방법은 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
### 대체 스냅숏 위치를 지정하려면  
  
1.  에 **스냅숏** 의 페이지는 **게시 속성-\< 게시>** 대화 상자:  
  
    1.  **다음 폴더에 파일 보관**을 선택한 다음 **찾아보기** 를 클릭하여 디렉터리로 이동하거나 스냅숏 파일을 저장할 디렉터리 경로를 입력합니다.  
  
        > [!NOTE]  
        >  스냅숏 에이전트는 지정한 디렉터리에 대해 쓰기 권한이 있어야 하며 배포 에이전트 또는 병합 에이전트는 읽기 권한이 있어야 합니다. 끌어오기 구독을 사용 하는 경우 지정 해야 하는 공유 디렉터리 범용 명명 규칙 (UNC) 경로와 같은 \\\computername\snapshot 합니다. 자세한 내용은 참조 [스냅숏 폴더 보안](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)합니다.  
  
    2.  두 위치 모두에 스냅숏 파일을 쓸 필요가 없으면 **기본 폴더에 파일 보관** 의 선택을 취소합니다.  
  
     스냅숏 파일을 압축하려면 **이 폴더에 있는 스냅숏 파일 압축**을 선택합니다. 압축은 일반적으로 느린 대역폭 연결에 사용되며 CD-ROM 등의 이동식 미디어와 같은 대체 스냅숏 위치로 사용됩니다.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## 참고 항목  
 [대체 스냅숏 폴더 위치](../../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [스냅숏 속성 및 #40; 구성 복제 TRANSACT-SQL 프로그래밍 & #41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [기본 스냅숏 위치 & #40;를 지정 합니다. SQL Server Management Studio & #41;](../../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)   
 [게시 및 아티클 속성 변경](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [스냅숏으로 구독 초기화](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  