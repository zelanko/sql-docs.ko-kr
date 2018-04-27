---
title: 테이블 별칭 만들기(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- table aliases [SQL Server]
- aliases [SQL Server], tables
ms.assetid: 49e61e85-8abf-4ca7-8c70-7e9f8f1078bd
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 403ec79488077b308b94be0c02f6bd9870592272
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="create-table-aliases-visual-database-tools"></a>테이블 별칭 만들기(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
별칭을 사용하면 테이블 이름이 필요한 작업을 더 쉽게 수행할 수 있습니다. 별칭은 다음과 같은 경우에 유용하게 사용할 수 있습니다.  
  
-   [SQL 창](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md) 에서 문을 더 간결하고 읽기 쉽게 만들려는 경우  
  
-   열 이름을 한정하는 경우 등과 같이 쿼리에 테이블 이름을 자주 사용할 때 쿼리에 대해 지정된 특정 문자 길이 제한을 준수하려는 경우. 일부 데이터베이스에서는 쿼리의 최대 길이가 제한됩니다.  
  
-   자체 조인 등과 같이 동일한 테이블의 여러 인스턴스를 사용하여 작업할 때 특정 인스턴스를 지정해야 하는 경우  
  
예를 들어, 테이블 이름 `employee_information`에 대한 별칭 `"e"`를 만든 다음 쿼리의 나머지 부분 전반에 걸쳐 테이블을 `"e"`로 지칭할 수 있습니다.  
  
### <a name="to-create-an-alias-for-a-table-or-table-valued-object"></a>테이블이나 테이블 반환 개체에 대한 별칭을 만들려면  
  
1.  테이블이나 테이블 반환 개체를 쿼리에 추가합니다.  
  
2.  **다이어그램 창**에서 별칭을 만들려는 개체를 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **속성** 을 선택합니다.  
  
3.  **속성** 창의 **별칭** 필드에 별칭을 입력합니다.  
  
## <a name="see-also"></a>참고 항목  
[쿼리에 테이블 추가&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-tables-to-queries-visual-database-tools.md)  
[쿼리 결과 정렬 및 그룹화&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[쿼리 결과 요약&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[쿼리 관련 기본 작업 수행&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
