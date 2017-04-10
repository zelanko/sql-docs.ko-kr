---
title: "게시 속성, 스냅숏 | Microsoft Docs"
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
  - "sql13.rep.newpubwizard.pubproperties.snapshotformat.f1"
ms.assetid: 8e9133b1-fc37-4a85-8a7c-d5eaf172fbef
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# 게시 속성, 스냅숏
  **게시 속성** 대화 상자의 **스냅숏** 페이지를 사용하여 스냅숏 형식, 스냅숏 폴더 위치 및 스냅숏 적용 전후 실행할 스크립트를 설정할 수 있습니다. 스냅숏 폴더를 공유로 지정해야 하며 파일을 읽고 폴더에 쓰는 에이전트에 대한 충분한 권한이 있어야 합니다. 폴더를 적절 하 게 보호 하는 방법에 대 한 자세한 내용은 참조 [스냅숏 폴더 보안](../../relational-databases/replication/security/secure-the-snapshot-folder.md)합니다.  
  
> [!NOTE]  
>  게시 속성을 변경하려면 게시에 대한 새 스냅숏이 필요합니다. 자세한 내용은 참조 [변경 게시 및 아티클 속성](../../relational-databases/replication/publish/change-publication-and-article-properties.md)합니다.  
  
## 옵션  
 **스냅숏 형식**  
 스냅숏 형식에 대해 네이티브 모드 또는 문자 모드를 선택합니다.  
  
-   선택 **네이티브 SQL Server-모든 구독자가 SQL Server를 실행 하는 서버 여야** 모든 구독자의 인스턴스인 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)]합니다. 네이티브 스냅숏 형식을 사용할 때 최상의 성능을 제공합니다.  
  
-   선택 **문자-게시자 또는 구독자가 SQL Server 실행 하지 않는 경우 필요** 구독자에서 실행 중인 경우 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 또는 비-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자입니다.  
  
 **스냅숏 파일 위치**  
 스냅숏 파일을 저장할 위치를 선택합니다. 파일을 기본 위치에 저장할 수 있으며 기본 위치 대신 대체 위치에 저장할 수도 있습니다. 대체 위치에 저장된 파일을 압축할 수 있습니다.  
  
-   게시자에 대해 기본 스냅숏 폴더를 사용하려면 **기본 폴더에 파일 보관** 을 선택합니다. 스냅숏 폴더 위치는이 대화 상자에서 읽기 전용에서 게시자에 대 한 변경만 수 때문에 **배포자 속성** 대화 상자입니다. 자세한 내용은 참조 [#40; & 기본 스냅숏 위치를 지정 합니다. SQL Server Management Studio & #41;](../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)합니다.  
  
-   기본 위치 대신 대체 위치를 지정하려면 **다음 폴더에 파일 보관** 을 선택합니다. 입력란에 경로를 입력하거나 **찾아보기** 를 클릭하고 위치를 탐색합니다. 대체 스냅숏 위치의 파일을 압축하려면 **이 폴더에 있는 스냅숏 파일 압축** 을 선택합니다. 대체 위치는 다른 서버, 네트워크 드라이브 또는 이동식 미디어(CD-ROM 또는 이동식 디스크 등)가 될 수 있습니다. 자세한 내용은 [Alternate Snapshot Folder Locations](../../relational-databases/replication/alternate-snapshot-folder-locations.md) 및 [Compressed Snapshots](../../relational-databases/replication/compressed-snapshots.md)를 참조하세요.  
  
 **추가 스크립트 실행**  
 구독자에 스냅숏 적용 전후에 실행할 스크립트를 지정합니다. **스냅숏 형식** 이 **문자**인 경우에는 스크립트를 지정할 수 없습니다.  
  
 스크립트는 선택 사항이지만 명령을 실행하고 구독자에 관리 변경 내용을 적용하는 편리한 방법을 제공합니다. 스크립트를 실행 하는 방법에 대 한 자세한 내용은 참조 [실행 스크립트 전과 후의 스냅숏 적용](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)합니다.  
  
-   **스냅숏 적용 전 다음 스크립트 실행** 입력란에 경로를 입력하거나 **찾아보기** 를 클릭하여 스크립트의 위치를 지정합니다.  
  
-   **스냅숏 적용 후 다음 스크립트 실행** 입력란에 경로를 입력하거나 **찾아보기** 를 클릭하여 스크립트의 위치를 지정합니다.  
  
## 참고 항목  
 [게시 만들기](../../relational-databases/replication/publish/create-a-publication.md)   
 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [초기 스냅숏 만들기 및 적용](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [스냅숏으로 구독 초기화](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  