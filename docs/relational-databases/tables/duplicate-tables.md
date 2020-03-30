---
title: 테이블 복제 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- copying tables
- tables [SQL Server], duplicating
- duplicating tables
- table copying [SQL Server]
ms.assetid: c6b07423-d1e5-4e5e-8681-5088921f5df3
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 45fabf20b18fb0f3227f99ab2a6b5270e245562a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "72907307"
---
# <a name="duplicate-tables"></a>테이블 복제
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하거나 [!INCLUDE[tsql](../../includes/tsql-md.md)] 을 사용하여 새 테이블을 만들고, 기존 테이블에서 열 정보를 복사하여 기존 테이블을 복제할 수 있습니다.  
  
> [!IMPORTANT]  
>  이 작업은 테이블의 구조만 복제하며 테이블 행은 복제하지 않습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **테이블을 복제하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 대상 데이터베이스에서 CREATE TABLE 권한이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-duplicate-a-table"></a>테이블을 복제하려면  
  
1.  테이블을 만들려는 데이터베이스에 연결되어 있는지 확인한 다음 개체 탐색기에서 데이터베이스를 선택했는지 확인합니다.  
  
2.  개체 탐색기에서 **테이블** 을 마우스 오른쪽 단추로 클릭하고 **새 테이블**을 클릭합니다.  
  
3.  개체 탐색기에서 복사할 테이블을 마우스 오른쪽 단추로 클릭한 다음 **디자인**을 클릭합니다.  
  
4.  기존 테이블에서 열을 선택하고 **편집** 메뉴에서 **복사**를 클릭합니다.  
  
5.  새 테이블로 전환하고 첫 번째 행을 선택합니다.  
  
6.  **편집** 메뉴에서 **붙여넣기**를 클릭합니다.  
  
7.  **파일** 메뉴에서 **저장**_table name_을 클릭합니다.  
  
8.  **이름 선택** 대화 상자에서 새 테이블의 이름을 입력하고 **확인**을 클릭합니다.  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-duplicate-a-table-in-query-editor"></a>쿼리 편집기에서 테이블을 복제하려면  
  
1.  테이블을 만들려는 데이터베이스에 연결되어 있는지 확인한 다음 개체 탐색기에서 데이터베이스를 선택했는지 확인합니다.  
  
2.  복제하려는 테이블을 마우스 오른쪽 단추로 클릭하고 **테이블 스크립팅**을 가리킨 후 **CREATE**를 가리키고 **새 쿼리 편집기 창**을 선택합니다.  
  
3.  테이블 이름을 변경합니다.  
  
4.  새 테이블에 필요하지 않은 모든 열을 제거합니다.  
  
5.  **실행**을 클릭합니다.  
  
  
