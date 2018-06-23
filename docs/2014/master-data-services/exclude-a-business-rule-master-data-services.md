---
title: 비즈니스 규칙 제외(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- business rules [Master Data Services], excluding
ms.assetid: bdbc9df0-23f7-40b9-8aba-4445c1482580
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: d64a01cf9df6865790b39510ad5c6222d8d6fd87
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36183459"
---
# <a name="exclude-a-business-rule-master-data-services"></a>비즈니스 규칙 제외(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 비즈니스 규칙을 영구적으로 삭제하지는 않되 규칙에 대해 데이터 유효성을 검사하지 않으려면 규칙을 제외합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](administrators-master-data-services.md)를 참조하세요.  
  
### <a name="to-exclude-a-business-rule"></a>비즈니스 규칙을 제외하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  메뉴 모음에서 **관리** 를 가리키고 **비즈니스 규칙**을 클릭합니다.  
  
3.  **비즈니스 규칙 유지 관리** 페이지의 **모델** 목록에서 모델을 선택합니다.  
  
4.  **엔터티** 목록에서 엔터티를 선택합니다.  
  
5.  **멤버 유형을** 목록에서 멤버 유형을 선택 합니다.  
  
6.  **특성** 목록에서 특성을 선택하거나 기본값인 **모두**를 그대로 사용합니다.  
  
7.  비즈니스 규칙에 대 한 행에서 눈금에서의 확인란을 선택는 **제외** 열입니다. 값은 **상태** 열이 **제외 보류 중**합니다.  
  
8.  **비즈니스 규칙 게시**를 클릭합니다.  
  
9. 확인 대화 상자에서 **확인**을 클릭합니다. 값은 **상태** 열이 **제외 된**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [비즈니스 규칙 삭제 &#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-business-rule-master-data-services.md)   
 [비즈니스 규칙 만들기 및 게시&#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)   
 [비즈니스 규칙 &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  