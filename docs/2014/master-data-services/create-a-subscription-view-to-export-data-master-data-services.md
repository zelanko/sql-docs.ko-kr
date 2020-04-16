---
title: 구독 보기 만들기(마스터 데이터 서비스) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- subscription views [Master Data Services], creating
- creating subscription views [Master Data Services]
ms.assetid: a5e28961-af16-414a-9845-d2e06aac5214
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: c4a2f747192b1cddefeac256d4470a2b345305de
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2020
ms.locfileid: "65479944"
---
# <a name="create-a-subscription-view-master-data-services"></a>구독 뷰 만들기(Master Data Services)
  시스템을 구독하여 사용할 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스에서 데이터 보기를 만들려는 경우 구독 보기를 만듭니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **통합 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자 &#40;마스터 데이터 서비스&#41;](administrators-master-data-services.md)을 참조하십시오.  
  
### <a name="to-create-a-subscription-view"></a>구독 뷰를 만들려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **통합 관리**를 클릭합니다.  
  
2.  메뉴 모음에서 **뷰 만들기**를 클릭합니다.  
  
3.  구독 **보기** 페이지에서 **구독 보기 추가를 클릭합니다.**  
  
4.  구독 **보기 만들기** 창에서 **구독 보기 이름** 상자에서 뷰의 이름을 입력합니다.  
  
5.  **모델** 목록에서 모델을 선택합니다.  
  
6.  **버전** 또는 **버전 플래그** 옵션을 선택한 다음 해당 목록에서 선택합니다.  
  
    > [!TIP]  
    >  버전 플래그를 기반으로 구독 뷰를 만듭니다. 버전을 잠그는 경우에는 구독 뷰를 업데이트하지 않고 플래그를 열린 버전에 다시 할당할 수 있습니다.  
  
7.  **엔터티** 또는 **파생 계층 옵션을** 선택한 다음 해당 목록에서 선택합니다.  
  
8.  **형식** 목록에서 구독 뷰 형식을 선택합니다.  
  
9. **형식** 목록에서 **명시적 수준** 또는 **파생 수준** 을 선택한 경우에는 뷰에 포함할 계층의 수준 수를 입력합니다.  
  
10. **저장**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 &#40;마스터 데이터 서비스&#41;내보내기](overview-exporting-data-master-data-services.md)   
 [마스터 데이터 서비스&#41;&#40;구독 보기 삭제](delete-a-subscription-view-master-data-services.md)   
 [버전 플래그 만들기&#40;Master Data Services&#41;](create-a-version-flag-master-data-services.md)  
  
  
