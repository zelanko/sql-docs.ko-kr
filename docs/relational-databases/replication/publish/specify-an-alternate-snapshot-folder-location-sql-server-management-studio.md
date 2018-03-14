---
title: "대체 스냅숏 폴더 위치 지정(SQL Server Management Studio) | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], alternate folder locations
- snapshot replication [SQL Server], alternate folder locations
- alternate snapshot folders [SQL Server replication]
ms.assetid: 9293f0eb-5531-47ec-b6e2-0392823ce5cc
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 37d0e876882b742ccb79db74bc9d8534f2d1b33b
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="specify-an-alternate-snapshot-folder-location-sql-server-management-studio"></a>대체 스냅숏 폴더 위치 지정(SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **게시 속성 - \<Publication>** 대화 상자의 **스냅숏** 페이지에 대체 스냅숏 위치를 지정합니다. 이 대화 상자에 액세스하는 방법은 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
### <a name="to-specify-an-alternate-snapshot-location"></a>대체 스냅숏 위치를 지정하려면  
  
1.  **게시 속성 - \<게시>** 대화 상자의 **스냅숏** 페이지에서 다음을 수행합니다.  
  
    1.  **다음 폴더에 파일 보관**을 선택한 다음 **찾아보기** 를 클릭하여 디렉터리로 이동하거나 스냅숏 파일을 저장할 디렉터리 경로를 입력합니다.  
  
        > [!NOTE]  
        >  스냅숏 에이전트는 지정한 디렉터리에 대해 쓰기 권한이 있어야 하며 배포 에이전트 또는 병합 에이전트는 읽기 권한이 있어야 합니다. 끌어오기 구독을 사용하는 경우 공유 디렉터리를 \\\computername\snapshot과 같이 UNC(범용 명명 규칙) 경로로 지정해야 합니다. 자세한 내용은 [스냅숏 폴더 보안 설정](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)을 참조하세요.  
  
    2.  두 위치 모두에 스냅숏 파일을 쓸 필요가 없으면 **기본 폴더에 파일 보관** 의 선택을 취소합니다.  
  
     스냅숏 파일을 압축하려면 **이 폴더에 있는 스냅숏 파일 압축**을 선택합니다. 압축은 일반적으로 느린 대역폭 연결에 사용되며 CD-ROM 등의 이동식 미디어와 같은 대체 스냅숏 위치로 사용됩니다.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [대체 스냅숏 폴더 위치](../../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [스냅숏 속성 구성&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [기본 스냅숏 위치 지정&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)   
 [게시 및 아티클 속성 변경](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [스냅숏으로 구독 초기화](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
