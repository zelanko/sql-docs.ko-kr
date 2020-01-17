---
title: 게시 아티클 추가 및 삭제(SSMS)
description: SSMS(SQL Server Management Studio)를 사용하여 게시에 아티클을 추가하고 삭제하는 방법을 설명합니다.
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], dropping
- deleting articles
- dropping articles
- adding articles
- articles [SQL Server replication], adding
ms.assetid: d5a3e536-62d2-4473-a178-877ba52f7d7f
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 682f0af6b7ac2c6dffc8d0e1988ef2973b2f7b51
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321315"
---
# <a name="add-articles-to-and-drop-articles-from-a-publication"></a>게시에 대한 아티클 추가 및 삭제
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  새 게시 마법사에서 게시를 만들 때 처음으로 게시에 아티클을 추가합니다. 이 마법사를 사용하는 방법에 대한 자세한 내용은 [게시 만들기](../../../relational-databases/replication/publish/create-a-publication.md)를 참조하세요.  
  
 게시를 만든 후 **게시 속성 - \<Publication>** 대화 상자의 **아티클** 페이지에서 아티클을 추가 및 삭제합니다. 이 대화 상자에 액세스하는 방법은 [게시 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요. 아티클을 추가 및 삭제할 때 고려할 사항은 [기존 게시에 대한 아티클 추가 및 삭제](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)를 참조하세요.  
  
### <a name="to-add-an-article-after-a-publication-is-created"></a>게시를 만든 후 아티클을 추가하려면  
  
1.  **게시 속성 - \<Publication>** 대화 상자의 **아티클** 페이지에서 **선택 표시된 개체만 목록에 표시** 확인란의 선택을 취소합니다. 이렇게 하면 게시 데이터베이스에서 게시되지 않은 개체를 볼 수 있습니다.  
  
2.  추가할 각 아티클 옆에 있는 확인란을 선택합니다.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-delete-an-article"></a>아티클을 삭제하려면  
  
1.  **게시 속성 - \<Publication>** 대화 상자의 **아티클** 페이지에서 삭제할 각 아티클 옆에 있는 확인란의 선택을 취소합니다.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)   
 [데이터 및 데이터베이스 개체 게시](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
