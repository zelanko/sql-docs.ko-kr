---
title: "사용자 또는 그룹 삭제(Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deleting groups [Master Data Services]
- groups [Master Data Services], deleting
- users [Master Data Services], deleting
- deleting users [Master Data Services]
ms.assetid: 0bbf9d2c-b826-48bb-8aa9-9905db6e717f
caps.latest.revision: "7"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: decc1a6e675be52a81d9ac8e28b167c86fb0b1e3
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="delete-users-or-groups-master-data-services"></a>사용자 또는 그룹 삭제(Master Data Services)
  사용자나 그룹이 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에 액세스할 수 없게 하려면 해당 사용자나 그룹을 삭제합니다.  
  
 사용자와 그룹을 삭제할 때 다음 동작에 유의하십시오.  
  
-   [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에 대한 액세스 권한이 있는 그룹의 멤버인 사용자를 삭제하는 경우 Active Directory 또는 로컬 그룹에서 제거할 때까지는 해당 사용자가 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 에 액세스할 수 있습니다.  
  
-   그룹을 삭제하는 경우 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 에 액세스한 그룹의 모든 사용자를 삭제할 때까지 **사용자** 목록에 해당 사용자가 표시됩니다.  
  
-   보안에 대한 변경 내용은 20분 동안 MDS [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] 에 전파되지 않습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **사용자 및 그룹 권한** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
### <a name="to-delete-users-or-groups"></a>사용자나 그룹을 삭제하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **사용자 및 그룹 권한**을 클릭합니다.  
  
2.  사용자를 삭제하려면 **사용자** 페이지에 남아 있습니다. 그룹을 삭제하려면 메뉴 모음에서 **그룹 관리**를 클릭합니다.  
  
3.  표에서 삭제하려는 사용자나 그룹의 행을 선택합니다.  
  
4.  **선택한 사용자 삭제** 또는 **선택한 그룹 삭제**를 클릭합니다.  
  
5.  확인 대화 상자에서 **확인**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [보안&#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)  
  
  
