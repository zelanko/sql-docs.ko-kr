---
title: "기본 스냅숏 위치 지정(SQL Server Management Studio) | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], default locations
- default snapshot locations
ms.assetid: 27c5d9ad-a915-4c59-a8b7-82e3af61ac4d
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e6cda346b9dfdbc0a5693ce263456ee7f10076a2
ms.lasthandoff: 04/11/2017

---
# <a name="specify-the-default-snapshot-location-sql-server-management-studio"></a>기본 스냅숏 위치 지정(SQL Server Management Studio)
  배포 구성 마법사의 **스냅숏 폴더** 페이지에서 기본 스냅숏 위치를 지정합니다. 이 마법사 사용에 대한 자세한 내용은 [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md)을 참조하세요. 배포자로 구성되어 있지 않은 서버에서 게시를 만드는 경우 새 게시 마법사의 **스냅숏 폴더** 페이지에서 기본 스냅숏 위치를 지정합니다. 이 마법사를 사용하는 방법에 대한 자세한 내용은 [게시 만들기](../../relational-databases/replication/publish/create-a-publication.md)를 참조하세요.  
  
 **배포자 속성 - \<Distributor>** 대화 상자의 **게시자** 페이지에서 기본 스냅숏 위치를 수정합니다. 자세한 내용은 [배포자 및 게시자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)을 참조하세요. **게시 속성 - \<게시>** 대화 상자에서 각 게시에 대한 스냅숏 폴더를 설정합니다. 자세한 내용은 [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
### <a name="to-modify-the-default-snapshot-location"></a>기본 스냅숏 위치를 수정하려면  
  
1.  **배포자 속성 - \<Distributor>** 대화 상자의 **게시자** 페이지에서 기본 스냅숏 위치를 변경할 게시자의 속성 단추(**…**)를 클릭합니다.  
  
2.  **게시자 속성 - \<Publisher>** 대화 상자에서 **기본 스냅숏 폴더** 속성에 대한 값을 입력합니다.  
  
    > [!NOTE]  
    >  스냅숏 에이전트는 지정한 디렉터리에 대해 쓰기 권한이 있어야 하며 배포 에이전트 또는 병합 에이전트는 읽기 권한이 있어야 합니다. 끌어오기 구독을 사용하는 경우 공유 디렉터리를 \\\computername\snapshot과 같이 UNC(범용 명명 규칙) 경로로 지정해야 합니다. 자세한 내용은 [스냅숏 폴더 보안 설정](../../relational-databases/replication/security/secure-the-snapshot-folder.md)을 참조하세요.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목:  
 [대체 스냅숏 폴더 위치](../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [스냅숏으로 구독 초기화](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
