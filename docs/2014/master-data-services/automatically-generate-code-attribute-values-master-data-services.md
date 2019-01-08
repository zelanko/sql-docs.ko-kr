---
title: 코드 특성 값 자동 생성(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 19b354ee-2906-4cc7-ba2f-32b4543bddcf
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: bc686928863395217fa564ff04b7c26a52c1f1bb
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52782405"
---
# <a name="automatically-generate-code-attribute-values-master-data-services"></a>코드 특성 값 자동 생성(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 새 멤버를 만들 때마다 코드 값에 정수가 자동 할당되도록 하려면 엔터티의 코드 특성에 대해 값을 자동으로 생성합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](administrators-master-data-services.md)를 참조하세요.  
  
-   엔터티가 있어야 합니다. 자세한 내용은 [엔터티 만들기&#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md)를 참조하세요.  
  
### <a name="to-automatically-generate-code-values"></a>코드 값을 자동으로 생성하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 탐색기** 페이지의 메뉴 모음에서 **관리** 를 가리키고 **엔터티**를 클릭합니다.  
  
3.  **엔터티 유지 관리** 페이지의 **모델** 목록에서 모델을 선택합니다.  
  
4.  코드를 생성하려는 엔터티의 행을 선택합니다.  
  
5.  **선택한 엔터티 편집**을 클릭합니다.  
  
6.  **코드 값 자동으로 만들기** 확인란을 선택합니다.  
  
7.  **시작 값** 상자에 증가를 시작할 숫자를 입력합니다. 멤버가 이미 있는 경우 가장 높은 기존 값을 기반으로 코드가 설정됩니다. 예를 들어 가장 높은 기존 코드 값이 299인 경우 다음 멤버의 코드 값은 300으로 설정됩니다.  
  
8.  **엔터티 저장**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [코드 자동 생성&#40;Master Data Services&#41;](../../2014/master-data-services/automatic-code-creation-master-data-services.md)   
 [코드 외의 특성 값 자동 생성&#40;Master Data Services&#41;](../../2014/master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)  
  
  
