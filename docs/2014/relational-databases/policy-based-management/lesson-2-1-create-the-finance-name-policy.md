---
title: Finance Name 정책 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 56b2c852-fd69-4cd2-9b5d-977467b94fd9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ec01dd697e04b5d4b5d8d943a855a62adac48f60
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66090622"
---
# <a name="create-the-finance-name-policy"></a>Finance Name 정책 만들기
  이 태스크에서는 Finance라는 데이터베이스를 만든 다음 모든 테이블이 **fintbl**로 시작하도록 지정하는 조건을 만듭니다. 그런 다음 Finance 데이터베이스의 테이블에 대한 명명 표준을 적용하는 정책 및 정책 범주를 만듭니다.  
  
### <a name="to-create-the-finance-database"></a>Finance  데이터베이스를 만들려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 쿼리 창을 열고 다음 문을 실행합니다.  
  
    ```  
    CREATE DATABASE Finance ;  
    GO  
    ```  
  
2.  개체 탐색기에서 **데이터베이스**를 클릭한 다음 F5 키를 눌러 데이터베이스 목록을 새로 고칩니다.  
  
### <a name="to-create-the-finance-tables-condition"></a>Finance  Tables  조건을 만들려면  
  
1.  개체 탐색기에서 **관리**, **정책 관리**를 차례로 확장하고 **조건**을 마우스 오른쪽 단추로 클릭한 다음 **새 조건**을 클릭합니다.  
  
2.  **새 조건 만들기** 대화 상자의 **이름** 상자에 **Finance Tables**를 입력합니다.  
  
3.  **패싯** 목록에서 **여러 부분으로 구성된 이름**을 선택합니다.  
  
4.  **식** 영역의 **필드** 상자에서 **@Name**을 선택하고, **연산자** 상자에서 **Like**를 선택하고, **값** 상자에 **'fintbl%'** 를 입력하여 모든 테이블 이름이 **fintbl**로 시작하도록 지정합니다.  
  
5.  **설명** 페이지에서 **Finance table names must begin with fintbl**을 입력한 다음 **확인** 을 클릭하여 조건을 만듭니다.  
  
### <a name="to-create-the-finance-name-policy"></a>Finance  Name  정책을 만들려면  
  
1.  개체 탐색기에서 **정책**을 마우스 오른쪽 단추로 클릭한 다음 **새 정책**을 클릭합니다.  
  
2.  **새 정책 만들기** 대화 상자의 **이름** 상자에 **Finance Name**을 입력합니다.  
  
3.  **조건 확인** 목록에서 **Finance Tables**를 선택합니다. 이는 **여러 부분으로 구성된 이름** 영역에 있습니다.  
  
4.  **대상** 영역에 이 정책을 적용할 수 있는 데이터베이스 개체의 목록이 표시됩니다. **매 테이블**확인란을 선택합니다.  
  
5.  **매 데이터베이스** 영역에서 **매**를 확장한 다음 **새 조건**을 클릭합니다.  
  
6.  **새 조건 만들기** 대화 상자의 **이름** 상자에 **Finance Database**를 입력합니다.  
  
7.  **식** 상자에서 **@Name = 'Finance'** 를 포함하도록 식을 완성한 다음 **확인**을 클릭하여 조건 페이지를 닫습니다.  
  
    > [!NOTE]  
    >  **값** 상자에서 Tab 키를 눌러 **확인** 단추를 활성화해야 할 수도 있습니다.  
  
8.  **평가 모드** 목록에서 **변경 시: 방지**를 선택합니다. 이렇게 하면 Finance 데이터베이스에 대한 데이터베이스 트리거를 만들어 정책을 적용합니다.  
  
9. **사용** 목록을 선택합니다. **사용** 상자는 **요청 시** 정책에 적용되지 않습니다.  
  
10. **서버 제한** 목록에서 **없음**을 선택합니다.  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-create-the-finance-policy-category"></a>Finance  정책 범주를 만들려면  
  
1.  개체 탐색기에서 **관리**를 확장하고 **정책 관리**를 마우스 오른쪽 단추로 클릭한 다음 **범주 관리**를 클릭합니다.  
  
2.  에 **정책 범주 관리** 대화 상자의 **이름**, 형식 `Finance` 의 선택을 취소 확인 하 고 빈 상자 **데이터베이스 구독 위임**합니다. **데이터베이스 구독 위임** 을 선택하면 해당 인스턴스에 있는 모든 데이터베이스가 이 정책 범주에 속하는 정책을 구독하게 됩니다. 따라서 Finance 데이터베이스만 Finance Name 정책을 구독해야 합니다.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [Finance Name 정책 구독 및 확인](lesson-2-2-subscribe-to-and-check-the-finance-name-policy.md)  
  
  
