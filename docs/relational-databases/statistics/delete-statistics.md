---
title: "통계 삭제 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: statistics
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-statistics
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- statistics [SQL Server], deleting
- deleting statistics
ms.assetid: eccce0aa-591e-4a1d-bd10-373b022f8749
caps.latest.revision: "8"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3adb0891686a6742378debe105b447eba039020f
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="delete-statistics"></a>통계 삭제
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 테이블 및 뷰에서 통계를 삭제할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 테이블 또는 뷰에서 통계를 삭제하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   통계를 삭제할 때는 주의하세요. 통계를 삭제하면 쿼리 최적화 프로그램이 선택한 실행 계획에 영향을 줄 수 있습니다.  
  
-   인덱스에 대한 통계는 DROP STATISTICS를 사용하여 삭제할 수 없으며 인덱스가 존재하는 한 통계도 유지됩니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 테이블이나 뷰에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-drop-statistics-from-a-table-or-view"></a>테이블 또는 뷰에서 통계를 삭제하려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 통계를 삭제할 데이터베이스를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **테이블** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 통계를 삭제할 테이블을 확장합니다.  
  
4.  더하기 기호를 클릭하여 **통계** 폴더를 확장합니다.  
  
5.  삭제할 통계 개체를 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택합니다.  
  
6.  **개체 삭제** 대화 상자에서 올바른 통계를 선택했는지 확인하고 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-drop-statistics-from-a-table-or-view"></a>테이블 또는 뷰에서 통계를 삭제하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- First, create two statistics named VendorCredit and CustomerTotal  
    -- The first statistic uses a random 50% sample of information provided from the Name and CreditRating columns in the Purchasing.Vendor table.  
    CREATE STATISTICS VendorCredit  
        ON Purchasing.Vendor (Name, CreditRating)  
        WITH SAMPLE 50 PERCENT  
    -- The second statistic uses all of the information from the CustomerID and TotalDue columns in the Sales.SalesOrderHeader table  
    CREATE STATISTICS CustomerTotal  
        ON Sales.SalesOrderHeader (CustomerID, TotalDue)  
        WITH FULLSCAN;  
    GO  
    -- This next statement drops both of the statistics created above. Note that the naming convention is [table_name].[statistics_name].  
    DROP STATISTICS Purchasing.Vendor.VendorCredit, Sales.SalesOrderHeader.CustomerTotal;  
    GO  
    ```  
  
 자세한 내용은 [DROP STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)를 참조하세요.  
  
  
