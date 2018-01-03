---
title: "SQL 창(Visual Database Tools) | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Query Designer [SQL Server], SQL pane
- View Designer, SQL pane
- SQL pane [Visual Database Tools]
ms.assetid: dbabab18-0614-415b-a2ef-9bcd0d320d5c
caps.latest.revision: "3"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a44627a7853237edd1bfebb3cb576f495535c6d7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sql-pane-visual-database-tools"></a>SQL Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] SQL 창을 사용하여 고유한 SQL 문을 만들거나 조건 창 및 다이어그램 창을 사용하여 문을 만들 수 있습니다. 조건 창이나 다이어그램 창을 사용해도 SQL 문은 SQL 창에 작성됩니다. 쿼리를 작성할 때 SQL 창은 자동으로 업데이트되고 읽기 쉽도록 서식이 다시 지정됩니다.  
  
SQL 창을 열려면 먼저 **데이터베이스** 메뉴에서 **새 쿼리**를 클릭하여 서버 탐색기에서 데이터베이스 개체를 선택한 상태로 쿼리 및 뷰 디자이너를 엽니다. 그런 다음 **쿼리 디자이너** 메뉴에서 **창** 을 가리키고 **SQL**을 클릭합니다.  
  
SQL 창에서 다음 작업을 수행할 수 있습니다.  
  
-   SQL 문을 입력하여 새 쿼리를 만듭니다.  
  
-   다이어그램 창과 조건 창의 설정에 기반하여 쿼리 및 뷰 디자이너에서 만든 SQL 문을 수정합니다.  
  
-   사용 중인 데이터베이스의 특정 기능을 활용할 수 있는 문을 입력합니다.  
  
> [!NOTE]  
> 사용 중인 데이터베이스의 데이터베이스 개체 식별 규칙을 잘 알고 있어야 합니다. 자세한 내용은 데이터베이스 관리 시스템의 설명서를 참조하십시오.  
  
## <a name="statements-in-the-sql-pane"></a>SQL 창의 문  
SQL 창에서 현재 쿼리를 직접 편집할 수 있습니다. 다른 창으로 이동할 때 쿼리 및 뷰 디자이너는 문 서식을 자동으로 지정한 다음 다이어그램 창과 조건 창을 문과 일치하도록 변경합니다.  
  
다이어그램 창과 조건 창에 문을 나타낼 수 없고 해당 창들이 표시되는 경우 쿼리 및 뷰 디자이너는 오류를 표시한 후 다음과 같은 두 가지 선택을 제공합니다.  
  
-   다이어그램 창과 조건 창에 문을 나타낼 수 없다는 사실을 무시합니다.  
  
-   나타낼 수 없는 변경 내용을 취소하고 가장 최근 버전의 SQL 문으로 되돌립니다.  
  
다이어그램 창과 조건 창에 문을 나타낼 수 없다는 사실을 무시하도록 선택하면 쿼리 및 뷰 디자이너에서 다른 창이 흐리게 표시됩니다. 이는 해당 창에 SQL 창의 내용이 더 이상 반영되지 않음을 의미합니다.  
  
다른 SQL 문을 사용할 때와 같이 문을 계속 편집하고 실행할 수 있습니다.  
  
> [!NOTE]  
> SQL 문을 입력한 다음 다이어그램 창과 조건 창을 변경하여 쿼리를 추가로 변경하면 쿼리 및 뷰 디자이너는 SQL 문을 다시 작성하여 표시합니다. 일부 경우 이 동작으로 인해 결과는 같지만 원래 입력한 내용과 다른 SQL 문이 만들어지기도 합니다. 이러한 차이는 AND와 OR로 연결된 여러 절을 포함하는 검색 조건을 사용하여 작업할 때 특히 자주 나타납니다.  
  
## <a name="see-also"></a>참고 항목  
[쿼리 만들기&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-queries-visual-database-tools.md)  
[쿼리 실행&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/run-queries-visual-database-tools.md)  
[쿼리 및 뷰 디자인 방법 도움말 항목&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[다이어그램 창&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)  
[조건 창&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)  
[결과 창&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)  
  
