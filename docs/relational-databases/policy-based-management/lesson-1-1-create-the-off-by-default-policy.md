---
title: "Off By Default 정책 만들기 | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-query-tuning
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 98fde3c5-297c-4d95-981e-95700bbf5ccd
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ad1ef04caea4fc15cc53fced05ab5861d54ad7eb
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-1-1---create-the-off-by-default-policy"></a>1-1단원 - Off By Default 정책 만들기
이 태스크에서는 노출 영역 구성 패싯을 기반으로 하는 Mail Off라는 조건을 만듭니다. 그리고 나서 Off By Default라는 정책을 만듭니다.  
  
### <a name="to-create-the-mail-off-condition"></a>Mail Off 조건을 만들려면  
  
1.  개체 탐색기에서 **관리**, **정책 관리**, **패싯**을 차례로 확장하고 **노출 영역 구성**을 마우스 오른쪽 단추로 클릭한 다음 **새 조건**을 클릭합니다.  
  
2.  **새 조건 만들기** 대화 상자의 **이름** 상자에 **Mail Off**를 입력합니다.  
  
3.  **패싯** 상자에서 **노출 영역 구성** 패싯이 선택되어 있는지 확인합니다.  
  
4.  **식** 영역의 **필드** 상자에서 **@DatabaseMailEnabled**를 선택하고, **연산자** 상자에서 **=**를 선택한 다음 **값**에서 **False**를 선택합니다.  
  
5.  **설명** 페이지에서 조건에 대한 설명을 입력한 다음 **확인** 을 클릭하여 조건을 만듭니다.  
  
### <a name="to-create-the-off-by-default-policy"></a>Off By Default 정책을 만들려면  
  
1.  개체 탐색기에서 **노출 영역 구성**을 마우스 오른쪽 단추로 클릭한 다음 **새 정책**을 클릭합니다.  
  
2.  **새 정책 만들기** 대화 상자의 **이름** 상자에 **Off By Default**를 입력합니다.  
  
3.  **사용** 확인란을 선택하지 않은 상태로 둡니다. **사용** 확인란은 자동화된 정책에 적용되며 이 정책은 요청 시 실행됩니다.  
  
4.  **조건 확인** 확인란에서 **노출 영역 구성** 영역까지 아래로 스크롤한 다음 **Mail Off** 를 확인할 조건으로 선택합니다.  
  
5.  이 정책은 서버 범위 정책이므로 **적용 대상** 상자는 비어 있습니다.  
  
6.  **평가 모드** 확인란에서 **요청 시** 를 평가 모드로 선택합니다.  
  
7.  **서버 제한** 확인란에서 **없음**을 선택합니다.  
  
8.  **설명** 페이지에서 정책에 대한 설명을 입력합니다.  
  
9. **추가 도움말 하이퍼링크** 영역에 정책에 대한 웹 페이지의 하이퍼링크를 제공할 수 있습니다. **표시할 텍스트** 상자에 하이퍼링크에 대해 표시할 텍스트를 입력합니다.  
  
10. **주소** 상자에 회사의 IT 부서에 대한 홈페이지와 같이 도움말 페이지에 대한 하이퍼링크를 입력합니다.  
  
11. 웹 페이지를 열어 주소를 확인하려면 **링크 테스트**를 클릭합니다.  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[Off By Default 정책을 실행하도록 서버 구성](../../relational-databases/policy-based-management/lesson-1-2-configure-a-server-to-run-the-off-by-default-policy.md)  
  
  
  

