---
title: 테이블 복제 | Microsoft 문서
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
- copying tables
- tables [SQL Server], duplicating
- duplicating tables
- table copying [SQL Server]
ms.assetid: c6b07423-d1e5-4e5e-8681-5088921f5df3
caps.latest.revision: 15
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 0f543c38a4fcc00e530aeac8c7e54014afe99429
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089910"
---
# <a name="duplicate-tables"></a>테이블 복제
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하거나 [!INCLUDE[tsql](../../includes/tsql-md.md)] 을 사용하여 새 테이블을 만들고, 기존 테이블에서 열 정보를 복사하여 기존 테이블을 복제할 수 있습니다.  
  
> [!IMPORTANT]  
>  이 작업은 테이블의 구조만 복제하며 테이블 행은 복제하지 않습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **테이블을 복제하려면**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 대상 데이터베이스에서 CREATE TABLE 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-duplicate-a-table"></a>테이블을 복제하려면  
  
1.  테이블을 만들려는 데이터베이스에 연결되어 있는지 확인한 다음 개체 탐색기에서 데이터베이스를 선택했는지 확인합니다.  
  
2.  개체 탐색기에서 **테이블** 을 마우스 오른쪽 단추로 클릭하고 **새 테이블**을 클릭합니다.  
  
3.  개체 탐색기에서 복사할 테이블을 마우스 오른쪽 단추로 클릭한 다음 **디자인**을 클릭합니다.  
  
4.  기존 테이블에서 열을 선택하고 **편집** 메뉴에서 **복사**를 클릭합니다.  
  
5.  새 테이블로 전환하고 첫 번째 행을 선택합니다.  
  
6.  **편집** 메뉴에서 **붙여넣기**를 클릭합니다.  
  
7.  **파일** 메뉴에서 **저장***테이블 이름*을 클릭합니다.  
  
8.  **이름 선택** 대화 상자에서 새 테이블의 이름을 입력하고 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-duplicate-a-table-in-query-editor"></a>쿼리 편집기에서 테이블을 복제하려면  
  
1.  테이블을 만들려는 데이터베이스에 연결되어 있는지 확인한 다음 개체 탐색기에서 데이터베이스를 선택했는지 확인합니다.  
  
2.  복제하려는 테이블을 마우스 오른쪽 단추로 클릭하고 **테이블 스크립팅**을 가리킨 후 **CREATE**를 가리키고 **새 쿼리 편집기 창**을 선택합니다.  
  
3.  테이블 이름을 변경합니다.  
  
4.  새 테이블에 필요하지 않은 모든 열을 제거합니다.  
  
5.  **실행**을 클릭합니다.  
  
  