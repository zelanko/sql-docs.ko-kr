---
title: 비즈니스 규칙에 대해 버전 유효성 검사(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- validating versions [Master Data Services]
- validating versions [Master Data Services], about validating versions
- versions [Master Data Services], validating
- business rules [Master Data Services], applying to all members
ms.assetid: 5aee7901-6d05-41d4-8bbb-c6f26791d1df
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: e33526df02cff22adbd56bfbfc2f25cef1c1c052
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65482317"
---
# <a name="validate-a-version-against-business-rules-master-data-services"></a>비즈니스 규칙에 대해 버전 유효성 검사(Master Data Services)
  
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 버전의 유효성을 검사하여 모델 버전의 모든 멤버에 비즈니스 규칙을 적용할 수 있습니다.  
  
 이 절차는 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 애플리케이션을 사용하여 데이터의 유효성을 검사하는 방법을 설명합니다. MDS 데이터베이스에 대한 권한이 있는 경우 대신 저장 프로시저를 사용할 수 있습니다. 자세한 내용은 [유효성 검사 저장 프로시저&#40;Master Data Services&#41;](validation-stored-procedure-master-data-services.md)를 참조하세요.  
  
> [!NOTE]  
>  모든 멤버가 유효성 검사를 통과해야 버전을 커밋할 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   
  **버전 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md)에 액세스하지 않고 그룹에서 사용자를 추가하고 제거할 수 있습니다.  
  
-   버전의 상태가 **열림** 또는 **잠금**이어야 합니다.  
  
-   
  **버전 유효성 검사** 페이지에 **유효성 검사 성공**상태가 아닌 멤버가 있어야 합니다.  
  
### <a name="to-validate-a-version"></a>버전의 유효성을 검사하려면  
  
1.  
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **버전 관리**를 클릭합니다.  
  
2.  
  **버전 관리** 페이지의 메뉴 모음에서 **버전 유효성 검사**를 클릭합니다.  
  
3.  
  **버전 유효성 검사** 페이지에서 유효성을 검사하려는 모델과 버전을 선택합니다.  
  
4.  
  **유효성 검사**를 클릭합니다.  
  
5.  확인 대화 상자에서 **확인**을 클릭합니다.  
  
    > [!NOTE]  
    >  진행률 표시기가 더 이상 표시되지 않으면 버전의 유효성 검사가 완료된 것입니다.  
  
## <a name="next-steps"></a>다음 단계  
  
-   [버전 &#40;MDS(Master Data Services) 잠그기&#41;](../../2014/master-data-services/lock-a-version-master-data-services.md)  
  
## <a name="see-also"></a>참고 항목  
 [유효성 검사 상태 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/validation-statuses-master-data-services.md)   
 [유효성 검사 저장 프로시저 &#40;MDS(Master Data Services)&#41;](validation-stored-procedure-master-data-services.md)   
 [버전 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/versions-master-data-services.md)   
 [비즈니스 규칙 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/business-rules-master-data-services.md)   
 [비즈니스 규칙에 대해 특정 멤버의 유효성을 검사 &#40;MDS(Master Data Services)&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
  
