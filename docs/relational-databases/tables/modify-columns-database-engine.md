---
title: "열 수정(데이터베이스 엔진) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying data types
- column data types [SQL Server]
- data types [SQL Server], columns
ms.assetid: b67b95c5-61ef-4bd8-9a3e-1640eb7583ac
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: d4c39a2a76c33fdb52d55aa73970db271b1c23bd
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="modify-columns-database-engine"></a>열 수정(데이터베이스 엔진)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 열의 데이터 형식을 수정할 수 있습니다.  
  
> [!WARNING]  
>  이미 데이터가 포함되어 있는 열의 데이터 형식을 수정하면 기존 데이터를 새 형식으로 변환하는 과정에서 데이터를 완전히 잃을 수도 있습니다. 또한 수정된 열에 의존하고 있는 코드나 응용 프로그램에 문제가 발생할 수 있습니다. 여기에는 쿼리, 뷰, 저장 프로시저, 사용자 정의 함수, 클라이언트 응용 프로그램 등이 포함됩니다. 이러한 문제는 연쇄적인 파급 효과를 가져올 수 있습니다. 예를 들어 수정된 열에 의존하는 사용자 정의 함수를 호출하는 저장 프로시저가 실패할 수도 있습니다. 따라서 열을 변경할 때는 이러한 결과를 미리 신중하게 고려해야 합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [보안](#Security)  
  
-   **열의 데이터 형식을 수정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-modify-the-data-type-of-a-column"></a>열의 데이터 형식을 수정하려면  
  
1.  **개체 탐색기**에서 소수 자릿수를 변경할 열이 포함된 테이블을 마우스 오른쪽 단추로 클릭하고 **디자인**을 클릭합니다.  
  
2.  데이터 형식을 수정하려는 열을 선택합니다.  
  
3.  **열 속성** 탭에서 **데이터 형식** 속성의 표 형태 셀을 클릭하고 드롭다운 목록에서 새 데이터 형식을 선택합니다.  
  
4.  **파일** 메뉴에서 **저장***table name*을 클릭합니다.  
  
> [!NOTE]  
>  열의 데이터 형식을 수정하면 선택한 데이터 형식에 대해 이미 다른 길이를 지정했더라도 테이블 디자이너에서 해당 형식의 기본 길이가 적용됩니다. 데이터 형식을 지정한 후에 항상 데이터 형식 길이를 원하는 값으로 설정해야 합니다.  
  
> [!WARNING]  
>  다른 테이블과 연관된 열의 데이터 형식을 수정하려고 시도하면 해당 변경 내용을 다른 테이블에도 적용할지 묻는 확인 메시지가 테이블 디자이너에 표시됩니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-modify-the-data-type-of-a-column"></a>열의 데이터 형식을 수정하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    CREATE TABLE dbo.doc_exy (column_a INT ) ;  
    GO  
    INSERT INTO dbo.doc_exy (column_a) VALUES (10) ;  
    GO  
    ALTER TABLE dbo.doc_exy ALTER COLUMN column_a DECIMAL (5, 2) ;  
    GO  
  
    ```  
  
 자세한 내용은 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)을 참조하세요.  
  
  
