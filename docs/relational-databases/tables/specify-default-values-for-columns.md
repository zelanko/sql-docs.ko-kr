---
title: 열의 기본값 지정 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], defaults
- default values
ms.assetid: 64514aed-b846-407b-992e-cf813f9a1a91
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 171f7806dacb158bb1ad596f300787f5b6c8ada9
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38044341"
---
# <a name="specify-default-values-for-columns"></a>열의 기본값 지정
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 열에 입력되는 기본값을 지정할 수 있습니다. 기본값이 지정되지 않은 상태에서 사용자가 열을 빈 채로 두면 다음과 같은 결과가 발생합니다.  
  
-   Null 값이 허용되도록 옵션을 설정한 경우 NULL이 열에 삽입됩니다.  
  
-   Null 값을 허용하는 옵션을 설정하지 않은 경우 열이 빈 채로 남겨지지만 사용자가 열의 값을 입력하지 않으면 행을 저장할 수 없습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **기본값을 지정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   **기본값** 필드에 값을 입력하여 괄호 없이 표시되는 바인딩된 기본값을 바꾸려는 경우 기본값을 바인딩 해제하고 새 기본값으로 대체하라는 메시지가 나타납니다.  
  
-   텍스트 문자열을 입력하려면 값을 작은따옴표(')로 묶어야 합니다. 큰따옴표(")는 따옴표 붙은 식별자용으로 예약되어 있으므로 사용하지 않아야 합니다.  
  
-   숫자 기본값을 입력하려면 따옴표를 사용하지 않고 숫자를 입력합니다.  
  
-   개체/함수를 입력하려면 따옴표 없이 개체/함수의 이름을 입력합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-specify-a-default-value-for-a-column"></a>열의 기본값을 지정하려면  
  
1.  **개체 탐색기**에서 소수 자릿수를 변경할 열이 포함된 테이블을 마우스 오른쪽 단추로 클릭하고 **디자인**을 클릭합니다.  
  
2.  기본값을 지정하려는 열을 선택합니다.  
  
3.  **열 속성** 탭에서 **기본값 또는 바인딩** 속성에 새 기본값을 입력합니다.  
  
    > [!NOTE]  
    >  숫자 기본값을 입력하려면 숫자를 입력합니다. 개체나 함수의 경우 해당 이름을 입력합니다. 영숫자 기본값의 경우 원하는 값을 작은따옴표로 묶어 입력합니다.  
  
4.  **파일** 메뉴에서 *****테이블 이름 저장*을 클릭합니다.  
  
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
  
 자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)을 참조하세요.  
  
###  <a name="TsqlExample"></a>  
