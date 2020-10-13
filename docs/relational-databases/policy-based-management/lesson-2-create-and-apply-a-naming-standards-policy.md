---
title: '2단원: 명명 표준 정책 만들기 및 적용'
description: 이 자습서에서는 SQL Server에서 정책 기반 관리를 위한 명명 표준 정책을 만들고 적용하는 방법을 설명합니다.
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.technology: security
ms.prod_service: database-engine
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 87e51f4e-156c-4def-8572-76a15075d75e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 246c9d419d6f9b8fdbaae2619ef45df4d9465c36
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91892433"
---
# <a name="lesson-2-create-and-apply-a-naming-standards-policy"></a>2단원: 명명 표준 정책 만들기 및 적용
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
일부 정책 기반 관리 정책 유형은 해당 정책과의 향후 호환성을 적용하는 트리거를 만들 수 있습니다. 이 단원에서는 테이블 명명 규칙을 적용하는 정책을 만듭니다. 그런 다음 해당 정책을 위반하는 테이블을 만들어 정책을 테스트합니다.  


## <a name="prerequisites"></a>사전 요구 사항
이 자습서를 완료하려면 SQL Server Management Studio, SQL Server를 실행하는 서버에 대한 액세스가 필요합니다.

- [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md)를 설치합니다.
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)을 설치합니다.
  
## <a name="create-the-finance-database"></a>Finance 데이터베이스 만들기  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 쿼리 창을 열고 다음 문을 실행합니다.  
  
    ```sql  
    CREATE DATABASE Finance ;  
    GO  
    ```  
  
2.  개체 탐색기에서 **데이터베이스**를 클릭한 다음 F5 키를 눌러 데이터베이스 목록을 새로 고칩니다.  

## <a name="create-the-finance-tables-condition"></a>Finance Tables 조건 만들기 

1.  개체 탐색기에서 **관리**, **정책 관리**를 차례로 확장하고 **조건**을 마우스 오른쪽 단추로 클릭한 다음 **새 조건**을 클릭합니다. 

   ![새 조건](Media/lesson-2-create-and-apply-a-naming-standards-policy/new-condition.png)
  
2.  **새 조건 만들기** 대화 상자의 **이름** 상자에 **Finance Tables**를 입력합니다.  
    1. **패싯** 목록에서 **여러 부분으로 구성된 이름**을 선택합니다. 
    1. **식** 영역의 **필드** 상자에서 **\@이름**을 선택하고, **연산자** 상자에서 **Like**를 선택하고, **값** 상자에 ```'fintbl%'```를 입력하여 모든 테이블 이름이 **fintbl**로 시작하도록 지정합니다.
    1. **설명** 페이지에서 **Finance table names must begin with fintbl**을 입력한 다음 **확인** 을 클릭하여 조건을 만듭니다.  

    ![Finance Tables 조건](Media/lesson-2-create-and-apply-a-naming-standards-policy/finance-tables-condition.png)
 
## <a name="create-the-finance-name-policy"></a>Finance Name 정책 만들기  
  
1.  개체 탐색기에서 **정책**을 마우스 오른쪽 단추로 클릭한 다음 **새 정책**을 클릭합니다.  

   ![새 정책](Media/lesson-2-create-and-apply-a-naming-standards-policy/new-policy.png)
  
2.  **새 정책 만들기** 대화 상자의 **이름** 상자에 **Finance Name**을 입력합니다.
    1. **조건 확인** 목록에서 **Finance Tables**를 선택합니다. 이는 **여러 부분으로 구성된 이름** 영역에 있습니다. 
    1. **대상** 영역에 이 정책을 적용할 수 있는 데이터베이스 개체의 목록이 표시됩니다. **매 테이블**확인란을 선택합니다.
    1. **사용** 목록을 선택합니다. **사용** 상자는 **요청 시** 정책에 적용되지 않습니다.
    1. **평가 모드** 목록에서 **변경 시: 방지**를 선택합니다. 이렇게 하면 Finance 데이터베이스에 대한 데이터베이스 트리거를 만들어 정책을 적용합니다. 
    1. **서버 제한** 목록에서 **없음**을 선택합니다. 
    1. **설명** 페이지에서 ‘Table names in the Finance database must contain 'fintbl%'’을 추가합니다. 
    1. **일반** 페이지로 돌아가 **매 데이터베이스** 영역에서 **매**를 확장한 다음, **새 조건**을 클릭합니다.

    ![새 Finance Name 정책 만들기](Media/lesson-2-create-and-apply-a-naming-standards-policy/create-new-policy-finance-name.png)
  
6.  **새 조건 만들기** 대화 상자의 **이름** 상자에 **Finance Database**를 입력합니다.
    1. **식** 상자에서 @Name = 'Finance'를 포함하도록 식을 완성한 다음 **확인**을 클릭하여 조건 페이지를 닫습니다. 
  
    ![새 ‘Fnance 데이터베이스’ 조건 만들기](Media/lesson-2-create-and-apply-a-naming-standards-policy/create-new-condition.png)

    > [!NOTE]  
    > **값** 상자에서 Tab 키를 눌러 **확인** 단추를 활성화해야 할 수도 있습니다.  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="create-the-finance-policy-category"></a>Finance 정책 범주 만들기  
  
1.  개체 탐색기에서 **관리**를 확장하고 **정책 관리**를 마우스 오른쪽 단추로 클릭한 다음 **범주 관리**를 클릭합니다.  

   ![범주 관리](Media/lesson-2-create-and-apply-a-naming-standards-policy/manage-categories.png)
  
2.  **정책 범주 관리** 대화 상자의 **이름**에서 빈 상자에 **Finance** 를 입력한 다음 **데이터베이스 구독 위임**의 선택을 취소합니다. **데이터베이스 구독 위임** 을 선택하면 해당 인스턴스에 있는 모든 데이터베이스가 이 정책 범주에 속하는 정책을 구독하게 됩니다. 따라서 Finance 데이터베이스만 Finance Name 정책을 구독해야 합니다.  

    ![정책 범주 관리](Media/lesson-2-create-and-apply-a-naming-standards-policy/manage-policy-categories.png)
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="subscribe-to-the-finance-policy-category"></a>Finance 정책 범주 구독  
  
1.  개체 탐색기에서 **데이터베이스**를 확장하고 **Finance**를 마우스 오른쪽 단추로 클릭한 다음 **정책**을 가리키고 **범주**를 클릭합니다. 

   ![Finance 정책 범주](Media/lesson-2-create-and-apply-a-naming-standards-policy/finance-categories.png)
  
2.  **Finance** 범주에 대한 **구독** 확인란을 선택합니다.  

   ![finance 정책에 가입됨](Media/lesson-2-create-and-apply-a-naming-standards-policy/subscribe-to-finance.png)
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="test-the-enforcement-of-the-finance-name-policy"></a>Finance Name 정책 적용 테스트  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 쿼리 창을 엽니다. **Finance Name** 정책을 위반하는 테이블을 만들려고 하는 다음 문을 실행합니다. 테이블 이름이 **fintbl**로 시작하지 않으므로 해당 테이블이 정책을 위반합니다.  
  
    ```sql  
    USE Finance ;  
    GO  
    CREATE TABLE NewTable  
    (Col1 int) ;  
    GO    
    ```  
  
    정책에서 테이블 생성을 금지하고 정책 이름을 제공하는 정보 메시지를 반환합니다. 

   ```
     Policy 'Finance Name' has been violated by 'SQLSERVER:\SQL\SQL\SQL2017\Databases\Finance\Tables\dbo.NewTable'.
     This transaction will be rolled back.
     Policy condition: '@Name LIKE 'fintbl%''
     Policy description: 'Tables names in the Finance database must contain 'fintbl%''.
     Additional help: '' : ''
     Statement: 'CREATE TABLE NewTable  
         (Col1 int)'.
     Msg 515, Level 16, State 2, Procedure msdb.sys.sp_syspolicy_execute_policy, Line 69 [Batch Start Line 2]
     Cannot insert the value NULL into column 'target_query_expression', table 'msdb.dbo.syspolicy_policy_execution_history_details_internal'; column does not allow nulls. INSERT fails.
     The statement has been terminated.
   ``` 
  
2.  올바른 이름을 제공하려면 다음과 같이 코드를 수정하고 문을 다시 실행합니다.  
  
    ```sql  
    USE Finance ;  
    GO  
    CREATE TABLE fintblNewTable  
    (Col1 int) ;  
    GO    
    ```  
  
    이번에는 테이블이 만들어집니다.  
  
## <a name="apply-the-policy-to-the-whole-server"></a>전체 서버에 정책 적용  
  
1.  현재 Finance 데이터베이스만 Finance 정책 범주를 구독합니다. 전체 서버에 정책 범주를 적용하는 것이 더 간단한 경우가 많습니다. 개체 탐색기에서 **관리**를 확장하고 **정책 관리**를 마우스 오른쪽 단추로 클릭한 다음 **범주 관리**를 클릭합니다.  
  
2.  **정책 범주 관리** 대화 상자에서 Finance 범주를 찾고 Finance 범주에 대해 **데이터베이스 구독 위임** 확인란을 선택합니다.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] 이제 Finance 범주가 모든 데이터베이스에 적용되지만 만든 조건으로 인해 Finance Name 정책이 Finance 데이터베이스로 제한됩니다. 이는 대상 정책에 대해 복합적으로 연결된 조건을 많은 서버에 올바르게 적용되는 방식으로 사용하는 방법을 보여 줍니다.  
  
## <a name="summary"></a>요약  
이 자습서에서는 정책 기반 관리 조건, 정책 및 정책 그룹을 만드는 방법과 필터를 적용하고 정책 기반 관리 대상의 조건 준수 여부를 검사하는 방법을 살펴보았습니다.  
  
## <a name="next"></a>다음  
이 자습서를 마칩니다. 자습서의 시작 부분으로 돌아가려면 [자습서: 정책 기반 관리를 사용하여 서버 관리](../../relational-databases/policy-based-management/tutorial-administering-servers-by-using-policy-based-management.md)를 참조하세요.  
  
자습서 목록을 보려면 [SQL Server 2016 자습서](../../sql-server/tutorials-for-sql-server-2016.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[정책 기반 관리를 사용하여 서버 관리](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)