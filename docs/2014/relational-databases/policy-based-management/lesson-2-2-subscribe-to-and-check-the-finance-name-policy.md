---
title: Finance Name 정책 구독 및 확인 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 126b4c4c-2a1c-4701-a0ad-8de23fbd7306
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3bbf6c9640882ffca2bbdbf82b2ef2667c394096
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66090692"
---
# <a name="subscribe-to-and-check-the-finance-name-policy"></a>Finance Name 정책 구독 및 확인
  이 태스크에서는 Finance 데이터베이스에서 Finance 정책 범주를 구독하도록 구성한 다음 Finance Name 정책을 테스트합니다.  
  
### <a name="to-subscribe-to-the-finance-policy-category"></a>Finance 정책 범주를 구독하려면  
  
1.  개체 탐색기에서 **데이터베이스**를 확장 하 고,를 `Finance`마우스 오른쪽 단추로 클릭 하 고 **정책**을 가리킨 다음 **범주**를 클릭 합니다.  
  
2.  범주에 대 한 구독 확인란을 선택 합니다. **** `Finance`  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-test-the-enforcement-of-the-finance-name-policy"></a>Finance Name 정책 적용을 테스트하려면  
  
1.  
  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 쿼리 창을 엽니다. 
  **Finance Name** 정책을 위반하는 테이블을 만들려고 하는 다음 문을 실행합니다. 테이블 이름이 **fintbl**로 시작하지 않으므로 해당 테이블이 정책을 위반합니다.  
  
    ```  
    USE Finance ;  
    GO  
    CREATE TABLE NewTable  
    (Col1 int) ;  
    GO  
  
    ```  
  
     정책에서 테이블 생성을 금지하고 정책 이름을 제공하는 정보 메시지를 반환합니다.  
  
2.  올바른 이름을 제공하려면 다음과 같이 코드를 수정하고 문을 다시 실행합니다.  
  
    ```  
    USE Finance ;  
    GO  
    CREATE TABLE fintblNewTable  
    (Col1 int) ;  
    GO  
  
    ```  
  
     이번에는 테이블이 만들어집니다.  
  
### <a name="to-apply-the-policy-to-the-whole-server"></a>전체 서버에 정책을 적용하려면  
  
1.  현재 Finance 데이터베이스만 Finance 정책 범주를 구독합니다. 전체 서버에 정책 범주를 적용하는 것이 더 간단한 경우가 많습니다. 개체 탐색기에서 **관리**를 확장하고 **정책 관리**를 마우스 오른쪽 단추로 클릭한 다음 **범주 관리**를 클릭합니다.  
  
2.  
  **정책 범주 관리** 대화 상자에서 Finance 범주를 찾고 Finance 범주에 대해 **데이터베이스 구독 위임** 확인란을 선택합니다.  
  
3.  
  [!INCLUDE[clickOK](../../includes/clickok-md.md)] 이제 Finance 범주가 모든 데이터베이스에 적용되지만 만든 조건으로 인해 Finance Name 정책이 Finance 데이터베이스로 제한됩니다. 이는 대상 정책에 대해 복합적으로 연결된 조건을 많은 서버에 올바르게 적용되는 방식으로 사용하는 방법을 보여 줍니다.  
  
## <a name="summary"></a>요약  
 이 자습서에서는 정책 기반 관리 조건, 정책 및 정책 그룹을 만드는 방법과 필터를 적용하고 정책 기반 관리 대상의 조건 준수 여부를 검사하는 방법을 살펴보았습니다.  
  
## <a name="next"></a>다음  
 이 자습서를 마칩니다. 시작 부분으로 돌아가려면 [자습서: 정책 기반 관리를 사용하여 서버 관리](tutorial-administering-servers-by-using-policy-based-management.md)를 참조하세요.  
  
 자습서 목록은 [SQL Server 2014에 대 한 자습서](../../tutorials/tutorials-for-sql-server-2014.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [정책 기반 관리를 사용하여 서버 관리](administer-servers-by-using-policy-based-management.md)  
  
  
