---
description: 통합 쿼리 만들기(Visual Database Tools)
title: UNION 쿼리 만들기
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], types
- UNION queries
- Select query
- combining query results
- merged SELECT query [SQL Server]
ms.assetid: b5aafb1d-e4ed-4922-b790-56abc5ec551a
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: b6d4d7618b3130e2b06d3efb8e9e2a35bc7ca0ee
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038376"
---
# <a name="create-union-queries-visual-database-tools"></a>통합 쿼리 만들기(Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
UNION 키워드를 사용하면 두 SELECT 문의 결과를 하나의 결과 테이블에 포함할 수 있습니다. 각 SELECT 문에서 반환된 모든 행이 UNION 식의 결과로 결합됩니다. 예를 보려면 [SELECT 예(Transact-SQL)](../../t-sql/queries/select-examples-transact-sql.md)를 참조하세요.  
  
> [!NOTE]  
> 다이어그램 창에는 SELECT 절을 하나만 표시할 수 있습니다. 따라서 통합 쿼리 작업을 진행할 때는 쿼리 디자이너에서 테이블 작업 창이 숨겨집니다.  
  
### <a name="to-create-a-merged-select-query"></a>병합된 선택 쿼리를 만들려면  
  
1.  쿼리를 열거나 새 쿼리를 만듭니다.  
  
2.  SQL 창에서 유효한 UNION 식을 입력합니다.  
  
    다음 예에서는 UNION 식이 유효합니다.  
  
    ```  
    SELECT ProductModelID, Name  
    FROM Production.ProductModel  
    UNION  
    SELECT ProductModelID, Name   
    FROM dbo.Gloves;  
    ```  
  
3.  **쿼리 디자이너** 메뉴에서 **SQL 실행** 을 클릭하여 쿼리를 실행합니다.  
  
    쿼리 디자이너에서 통합 쿼리의 서식이 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
[지원되는 쿼리 형식](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[쿼리 및 뷰 디자인 방법 도움말 항목](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[쿼리 관련 기본 작업 수행](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
[UNION(Transact-SQL)](../../t-sql/language-elements/set-operators-union-transact-sql.md)