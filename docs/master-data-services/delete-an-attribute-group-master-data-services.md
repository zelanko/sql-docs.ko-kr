---
description: 특성 그룹 삭제(Master Data Services)
title: 특성 그룹 삭제
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting attribute groups [Master Data Services]
- attribute groups [Master Data Services], deleting
ms.assetid: f915e89b-629d-4725-aea6-a7f051978244
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 91abdbbec357c5d5b7b629c5619b221c14bc0d15
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500599"
---
# <a name="delete-an-attribute-group-master-data-services"></a>특성 그룹 삭제(Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 **의** 탐색기 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]기능 영역에 탭을 더 이상 표시하지 않아도 되는 경우 특성 그룹을 삭제할 수 있습니다.  
  
-   **참고** 특성 그룹이 있는 경우 특성 그룹에 속하지 않은 특성은 **탐색기**에 표시되지 않습니다. 특성 그룹이 없는 경우 모든 특성이 표시됩니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자 &#40;MDS(Master Data Services)&#41;](../master-data-services/administrators-master-data-services.md)를 참조 하세요.  
  
### <a name="to-delete-an-attribute-group"></a>특성 그룹을 삭제하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 관리** 페이지의 표에서 모델을 선택 하 고 **엔터티**를 클릭 합니다.  
  
3.  **엔터티 관리** 페이지의 표에서 특성 그룹을 편집하려는 엔터티에 대한 행을 선택합니다.  
  
4.  **특성 그룹**을 클릭합니다.  
  
5.  **특성 그룹 관리** 페이지에 있는 **멤버 유형** 드롭다운 목록에서 멤버 유형을 선택하여 삭제하려는 그룹의 형식에 따라 **리프**, **통합**또는 **컬렉션**을 확장합니다.  
  
6.  삭제할 특성 그룹을 클릭합니다.  
  
7.  **삭제**를 클릭합니다.  
  
8.  확인 대화 상자에서 **확인**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [특성 그룹 &#40;MDS(Master Data Services)&#41;](../master-data-services/attribute-groups-master-data-services.md)   
 [특성 그룹 만들기&#40;Master Data Services&#41;](../master-data-services/create-an-attribute-group-master-data-services.md)  
  
  
