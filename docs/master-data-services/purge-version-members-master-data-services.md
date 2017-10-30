---
title: "버전 멤버 삭제(Master Data Services) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: adecce2d-46bb-49ff-8be9-0b31b8dd3cb6
caps.latest.revision: 7
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 56cccc3f368f17118dece215275fbe23822e9040
ms.contentlocale: ko-kr
ms.lasthandoff: 09/07/2017

---
# <a name="purge-version-members-master-data-services"></a>버전 멤버 삭제(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 멤버를 삭제해도 멤버가 비활성화(일시 삭제) 상태로만 전환됩니다. 멤버의 데이터는 데이터베이스에 계속 남아 있습니다. 이 항목에서는 모델 버전에서 일시 삭제된 모든 멤버를 영구적으로 삭제하는 방법을 설명합니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 이 절차를 수행하려면 다음 조건을 충족해야 합니다.  
  
-   버전 관리 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
## <a name="to-purge-soft-deleted-members"></a>일시 삭제된 멤버를 삭제하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **버전 관리**를 클릭합니다.  
  
2.  **버전 관리** 페이지에서 삭제하려는 버전의 모델을 선택합니다. 모델 버전 목록이 표시됩니다.  
  
3.  삭제할 버전의 행을 선택합니다.  
  
4.  **멤버 삭제**를 클릭합니다.  
  
5.  확인 메시지에서 "확인"을 클릭합니다.  
  
## <a name="additional-methods-to-purge-members"></a>멤버를 삭제하는 추가 방법  
 버전 멤버를 삭제하면 선택한 버전과 관련된 모든 엔터티에서 일시 삭제된 멤버가 영구적으로 삭제됩니다. 이 방법을 사용하는 대신 멤버를 더욱 구체적으로 삭제하려는 경우에는 엔터티 기준 준비 기능을 사용하여 엔터티의 특정 멤버만 영구적으로 삭제하면 됩니다. 또한 탐색기 기능 영역에 대한 권한이 있는 엔터티 관리자는 엔터티 탐색기 페이지에서 엔터티 버전을 삭제할 수 있습니다.  
  
 자세한 내용은 [리프 멤버 준비 테이블&#40;Master Data Services&#41;](../master-data-services/leaf-member-staging-table-master-data-services.md)을 참조하세요.  
  
  

