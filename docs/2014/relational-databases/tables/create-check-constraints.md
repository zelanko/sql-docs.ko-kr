---
title: CHECK 제약 조건 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- table constraints [SQL Server]
- attaching check constraints
- columns [SQL Server], constraints
- constraints [SQL Server], check
- CHECK constraints, attaching
ms.assetid: b8756304-9454-4d39-996a-64516831b7df
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7795ee6eca85a22bdd4e84c90ce49a9449ddff28
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85047136"
---
# <a name="create-check-constraints"></a>CHECK 제약 조건 만들기
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 하나 이상의 열에 사용할 수 있는 데이터 값을 지정할 수 있도록 테이블에 CHECK 제약 조건을 만들 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **새 CHECK 제약 조건을 만들려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-a-new-check-constraint"></a>새 CHECK 제약 조건을 만들려면  
  
1.  **개체 탐색기**에서 CHECK 제약 조건을 추가하려는 테이블을 확장하고, **제약 조건** 을 마우스 오른쪽 단추로 클릭한 후 **새 제약 조건**을 클릭합니다.  
  
2.  **CHECK 제약 조건** 대화 상자에서 **식** 필드를 클릭한 후, 줄임표 **(...)** 를 클릭합니다.  
  
3.  **CHECK 제약 조건 식** 대화 상자에서 CHECK 제약 조건에 대한 SQL 식을 입력합니다. 예를 들어 `SellEndDate` 테이블의 `Product` 열에 있는 항목을 `SellStartDate` 열에 있는 날짜보다 크거나 같은 값 또는 NULL 값으로 제한하려면 다음을 입력합니다.  
  
    ```  
    SellEndDate >= SellStartDate OR SellEndDate IS NULL  
    ```  
  
     또는, `zip` 열의 항목을 다섯 자리 숫자로 입력하도록 하려면 다음을 입력합니다.  
  
    ```  
    zip LIKE '[0-9][0-9][0-9][0-9][0-9]'  
    ```  
  
    > [!NOTE]  
    >  숫자가 아닌 제약 조건 값은 모두 작은따옴표(')로 묶어야 합니다.  
  
4.  **확인**을 클릭합니다.  
  
5.  **ID** 범주에서는 CHECK 제약 조건의 이름을 변경하고 해당 제약 조건에 대한 설명(확장 속성)을 추가할 수 있습니다.  
  
6.  **테이블 디자이너** 범주에서는 제약 조건을 적용하는 경우를 설정할 수 있습니다.  
  
    |**받는 사람:**|**다음 필드에서 예 선택:**|  
    |-------------|---------------------------------------------|  
    |제약 조건을 만들기 전에 존재한 데이터에 대한 제약 조건 테스트|**만들거나 활성화할 때 기존 데이터 검사**|  
    |이 테이블에서 복제 작업이 수행될 때마다 제약 조건 적용|**복제에 적용**|  
    |이 테이블의 행을 삽입하거나 업데이트할 때마다 제약 조건 적용|**INSERT 및 UPDATE에 적용**|  
  
7.  **닫기**를 클릭합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-a-new-check-constraint"></a>새 CHECK 제약 조건을 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    ALTER TABLE dbo.DocExc   
       ADD ColumnD int NULL   
       CONSTRAINT CHK_ColumnD_DocExc   
       CHECK (ColumnD > 10 AND ColumnD < 50);  
    GO  
    -- Adding values that will pass the check constraint  
    INSERT INTO dbo.DocExc (ColumnD) VALUES (49);  
    GO  
    -- Adding values that will fail the check constraint  
    INSERT INTO dbo.DocExc (ColumnD) VALUES (55);  
    GO  
  
    ```  
  
 자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)을 참조하세요.  
  
###  <a name="TsqlExample"></a>  
