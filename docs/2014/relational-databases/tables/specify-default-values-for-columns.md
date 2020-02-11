---
title: 열의 기본값 지정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], defaults
- default values
ms.assetid: 64514aed-b846-407b-992e-cf813f9a1a91
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8a02385a6cd12b85be1661c738488c000f810510
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68196721"
---
# <a name="specify-default-values-for-columns"></a>열의 기본값 지정
  
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 열에 입력되는 기본값을 지정할 수 있습니다. 기본값이 지정되지 않은 상태에서 사용자가 열을 빈 채로 두면 다음과 같은 결과가 발생합니다.  
  
-   Null 값이 허용되도록 옵션을 설정한 경우 NULL이 열에 삽입됩니다.  
  
-   Null 값을 허용하는 옵션을 설정하지 않은 경우 열이 빈 채로 남겨지지만 사용자가 열의 값을 입력하지 않으면 행을 저장할 수 없습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **기본값을 지정 하려면 다음을 사용 합니다.**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   
  **기본값** 필드에 값을 입력하여 괄호 없이 표시되는 바인딩된 기본값을 바꾸려는 경우 기본값을 바인딩 해제하고 새 기본값으로 대체하라는 메시지가 나타납니다.  
  
-   텍스트 문자열을 입력하려면 값을 작은따옴표(')로 묶어야 합니다. 큰따옴표(")는 따옴표 붙은 식별자용으로 예약되어 있으므로 사용하지 않아야 합니다.  
  
-   숫자 기본값을 입력하려면 따옴표를 사용하지 않고 숫자를 입력합니다.  
  
-   개체/함수를 입력하려면 따옴표 없이 개체/함수의 이름을 입력합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 권한  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-specify-a-default-value-for-a-column"></a>열의 기본값을 지정하려면  
  
1.  **개체 탐색기**에서 소수 자릿수를 변경할 열이 포함된 테이블을 마우스 오른쪽 단추로 클릭하고 **디자인**을 클릭합니다.  
  
2.  기본값을 지정하려는 열을 선택합니다.  
  
3.  
  **열 속성** 탭에서 **기본값 또는 바인딩** 속성에 새 기본값을 입력합니다.  
  
    > [!NOTE]  
    >  숫자 기본값을 입력하려면 숫자를 입력합니다. 개체나 함수의 경우 해당 이름을 입력합니다. 영숫자 기본값의 경우 원하는 값을 작은따옴표로 묶어 입력합니다.  
  
4.  **파일** 메뉴에서 **테이블 이름**_저장_을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-specify-a-default-value-for-a-column"></a>열의 기본값을 지정하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    CREATE TABLE dbo.doc_exz ( column_a INT, column_b INT) ;  
    GO  
    INSERT INTO dbo.doc_exz (column_a)VALUES ( 7 ) ;  
    GO  
    ALTER TABLE dbo.doc_exz  
    ADD CONSTRAINT col_b_def  
    DEFAULT 50 FOR column_b ;  
    GO  
  
    ```  
  
 자세한 내용은 [ALTER TABLE &#40;transact-sql&#41;](/sql/t-sql/statements/alter-table-transact-sql)을 참조 하세요.  
  
###  <a name="TsqlExample"></a>  
