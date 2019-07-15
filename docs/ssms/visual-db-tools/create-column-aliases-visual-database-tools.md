---
title: 열 별칭 만들기(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], aliases
- aliases [SQL Server], columns
ms.assetid: e2e1c166-8ea7-47a2-b6a7-e419bf0fa3bb
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: db485284b23c56a13f55d94f609a6c482669b61c
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67686074"
---
# <a name="create-column-aliases-visual-database-tools"></a>열 별칭 만들기(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
열 이름에 대한 별칭을 만들면 열 이름, 계산 및 요약 값에 대한 작업을 좀 더 쉽게 수행할 수 있습니다. 예를 들어, 열 별칭을 만들어 다음 작업을 수행할 수 있습니다.  
  
-   `(quantity * unit_price)` 같은 식이나 집계 함수에 대해 "Total Amount" 같은 열 이름을 만들 수 있습니다.  
  
-   대신 `"d_id"` 같이 축약된 형식의 열 이름을 만들 수 있습니다. `"discounts.stor_id."`  
  
열 별칭을 정의한 후에 선택 쿼리에 이 별칭을 사용하여 쿼리 결과를 지정할 수 있습니다.  
  
### <a name="to-create-a-column-alias"></a>열 별칭을 만들려면  
  
1.  **조건 창**에서 별칭을 만들려는 데이터 열이 포함된 행을 찾은 다음 필요한 경우 이 행을 출력하도록 표시합니다. 데이터 열이 아직 표에 없으면 이를 추가합니다.  
  
2.  선택한 행의 **별칭** 열에 별칭을 입력합니다. 별칭은 SQL의 모든 명명 규칙을 준수해야 합니다. 입력한 별칭 이름에 공백이 포함되어 있으면 쿼리 및 뷰 디자이너에서 공백 주위에 자동으로 구분 기호가 추가됩니다.  
  
## <a name="see-also"></a>참고 항목  
[쿼리에 열 추가&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-columns-to-queries-visual-database-tools.md)  
[쿼리 결과 정렬 및 그룹화&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[쿼리 결과 요약&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[쿼리 관련 기본 작업 수행&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
