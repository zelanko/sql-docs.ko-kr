---
title: 테이블에 열 추가(데이터베이스 엔진) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- inserting columns
- columns [SQL Server], adding
- adding columns
ms.assetid: abeb8d52-d562-4e29-9e1e-2923ae874859
caps.latest.revision: 17
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 08e262af1a2e424f497aa39e7b136c62cb5ac09c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080836"
---
# <a name="add-columns-to-a-table-database-engine"></a>테이블에 열 추가(데이터베이스 엔진)
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 테이블에 새 열을 추가하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **사용 하 여 열을 삽입 합니다.**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
 ALTER TABLE 문을 사용하여 테이블에 열을 추가하면 해당 열이 자동으로 테이블 끝에 추가됩니다. 테이블에서 특정 순서로 열을 지정하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용합니다. 하지만 이러한 방식은 데이터베이스 설계상 최선의 방법이 아닙니다. 가장 좋은 방법은 응용 프로그램 및 쿼리 수준에서 반환된 열에서 순서를 지정하는 것입니다. SELECT *를 사용해도 테이블에 정의된 순서에 따라 모든 열이 순서대로 반환된다고 가정해서는 안됩니다. 항상 열을 표시하려는 순서에 따라 쿼리 및 응용 프로그램에서 이름으로 열을 지정하세요.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-insert-columns-into-a-table-with-table-designer"></a>테이블 디자이너에서 테이블에 열을 삽입하려면  
  
1.  **개체 탐색기**에서 열을 추가할 테이블을 마우스 오른쪽 단추로 클릭하고 **디자인**을 선택합니다.  
  
2.  **열 이름** 열에서 첫 번째 빈 셀을 클릭합니다.  
  
3.  셀에 열 이름을 입력합니다. 열 이름은 반드시 입력해야 합니다.  
  
4.  Tab 키를 눌러 **데이터 형식** 셀로 이동한 다음 드롭다운에서 데이터 형식을 선택합니다. 데이터 형식도 반드시 지정해야 하며, 사용자가 이 값을 선택하지 않으면 기본값이 할당됩니다.  
  
    > [!NOTE]  
    >  **데이터베이스 도구** 아래의 **옵션**대화 상자에서 기본값을 변경할 수 있습니다.  
  
5.  **열 속성** 탭에서 다른 열 속성을 계속 정의합니다.  
  
    > [!NOTE]  
    >  새 열을 만들면 열 속성에 기본값이 자동으로 추가됩니다. 이러한 값은 **열 속성** 탭에서 변경할 수 있습니다.  
  
6.  열을 모두 추가 했으면는 **파일** 메뉴 선택 **저장 * * * 테이블 이름*합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-insert-columns-into-a-table"></a>테이블에 열을 삽입하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예에서는 `dbo.doc_exa`테이블에 두 개의 열을 추가합니다. 다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
```  
ALTER TABLE dbo.doc_exa ADD column_b VARCHAR(20) NULL, column_c INT NULL ;  
```  
  
##  <a name="FollowUp"></a> 자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)을 참조하세요.  
  
  
