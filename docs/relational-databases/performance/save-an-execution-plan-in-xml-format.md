---
title: XML 형식으로 실행 계획 저장 | Microsoft 문서
description: SQL Server Management Studio를 사용하여 실행 계획을 XML 형식으로 저장하고 열어서 보는 방법을 알아봅니다. 이 작업에는 적절한 권한이 필요합니다.
ms.custom: ''
ms.date: 08/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- XML query plans [SQL Server]
- opening execution plans
- XML Showplans [SQL Server]
- execution plans [SQL Server], saving
- saving execution plans
ms.assetid: c439e53b-56f3-4442-97c6-dabd48a203d8
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3c9c95103e574f51ef530f17432125fe99a591e6
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97469174"
---
# <a name="save-an-execution-plan-in-xml-format"></a>XML 형식으로 실행 계획 저장
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 실행 계획을 XML 파일로 저장하고 열어서 볼 수 있습니다.  
  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 실행 계획 기능을 사용하거나 XML 실행 계획 SET 옵션을 사용하려면 사용자에게 실행 계획을 생성할 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 실행하는 데 적합한 권한이 있어야 하며 쿼리에서 참조하는 모든 데이터베이스에 대한 SHOWPLAN 권한을 부여해야 합니다.  
  
### <a name="to-save-a-query-plan-by-using-the-xml-showplan-set-options"></a>XML 실행 계획 SET 옵션을 사용하여 쿼리 계획을 저장하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 쿼리 편집기를 열고 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  다음 문으로 [SHOWPLAN_XML](../../t-sql/statements/set-showplan-xml-transact-sql.md)을 설정합니다.  
  
    ```sql  
    SET SHOWPLAN_XML ON;  
    GO  
    ```  
  
    [STATISTICS XML](../../t-sql/statements/set-statistics-xml-transact-sql.md)을 설정하려면 다음 문을 사용합니다.  
  
    ```sql  
    SET STATISTICS XML ON;  
    GO  
    ```  
  
     > [!NOTE] 
     > SHOWPLAN_XML은 쿼리에 대한 컴파일 시간 쿼리 실행 계획 정보를 생성하지만 쿼리를 실행하지는 않습니다. **예상** 실행 계획이라고도 합니다. STATISTICS XML은 쿼리에 대한 런타임 쿼리 실행 계획 정보를 생성하고 쿼리를 실행합니다. **실제** 실행 계획이라고도 합니다.  
  
3.  쿼리를 실행합니다. 예제:  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    SET SHOWPLAN_XML ON;  
    GO  
    -- Execute a query.  
    SELECT BusinessEntityID   
    FROM HumanResources.Employee  
    WHERE NationalIDNumber = '509647174';  
    GO  
    SET SHOWPLAN_XML OFF;  
    ```  
  
4.  **결과** 창에서 쿼리 계획을 포함하는 **Microsoft SQL Server XML Showplan** 을 마우스 오른쪽 단추로 클릭한 다음 **다른 이름으로 결과 저장** 을 클릭합니다.  
  
5.  \<Grid or Text> **결과** **저장** 대화 상자의 **다른 이름으로 저장** 상자에서 **모든 파일(\*.\*)** 을 선택합니다.  
  
6.  **파일 이름** 상자에 이름을 \<name> **.sqlplan** 형식으로 입력하고 **저장** 을 클릭합니다.  

### <a name="to-save-an-execution-plan-by-using-sql-server-management-studio-options"></a>SQL Server Management Studio 옵션을 사용하여 실행 계획을 저장하려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 사용하여 예상 실행 계획이나 실제 실행 계획을 생성합니다. 자세한 내용은 [예상 실행 계획 표시](../../relational-databases/performance/display-the-estimated-execution-plan.md) 및 [실제 실행 계획 표시](../../relational-databases/performance/display-an-actual-execution-plan.md)를 참조하세요.  
  
2.  결과 창의 **실행 계획** 탭에서 그래픽 실행 계획을 마우스 오른쪽 단추로 클릭하고 **실행 계획을 다른 이름으로 저장** 을 선택합니다.  
  
     또는 **파일** 메뉴에서 **실행 계획을 다른 이름으로 저장** 을 선택할 수도 있습니다.  
  
3.  **다른 이름으로 저장** 대화 상자에서 **파일 형식** 이 **실행 계획 파일(\*.sqlplan)** 로 설정되어 있는지 확인합니다.  
  
4.  **파일 이름** 상자에 이름을 \<name> **.sqlplan** 형식으로 입력하고 **저장** 을 클릭합니다.  
  
### <a name="to-open-a-saved-xml-query-plan-in-sql-server-management-studio"></a>SQL Server Management Studio에서 저장된 XML 쿼리 계획을 열려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 **파일** 메뉴에서 **열기** 를 선택한 다음 **파일** 을 클릭합니다.  
  
2.  **파일 열기** 대화 상자에서 **파일 형식** 을 **실행 계획 파일(\*.sqlplan)** 로 설정하여 저장된 XML 쿼리 계획 파일의 필터링된 목록을 생성합니다.  
  
3.  보려는 XML 쿼리 계획 파일을 선택하고 **열기** 를 클릭합니다.  
  
     또는 Windows 탐색기에서 확장명이 **.sqlplan** 인 파일을 두 번 클릭합니다. 계획이 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 열립니다.  
  
## <a name="see-also"></a>참고 항목  
 [SET SHOWPLAN_XML&#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-xml-transact-sql.md)   
 [SET STATISTICS XML&#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-xml-transact-sql.md)  
  
  
