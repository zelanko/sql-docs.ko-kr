---
title: 사용자 지정 식을 사용하여 값 요약 또는 집계 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- summarizing query results
- custom expressions to aggregate values [SQL Server]
ms.assetid: 34130ac1-0106-4766-b324-acb0b7bb6f6e
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 07d5e322c715f5aaec7a4fc713d87fac171c2a8c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="summarize-or-aggregate-values-using-custom-expressions-visual-database-tools"></a>사용자 지정 식을 사용하여 값 요약 또는 집계(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
집계 함수를 사용하여 데이터를 집계할 수 있을 뿐만 아니라 사용자 지정 식을 만들어 집계 값을 산출할 수도 있습니다. 집계 쿼리에서 집계 함수를 사용할 위치에 어디든지 사용자 지정 식을 사용할 수 있습니다.  
  
예를 들어, `titles` 테이블에서 일반적인 평균 가격뿐만 아니라 가격이 할인된 경우의 평균 가격까지 표시하는 쿼리를 만들 수 있습니다.  
  
테이블의 개별 행만 사용되는 계산에 기반한 식은 포함할 수 없습니다. 식을 계산할 때는 집계 값만 사용할 수 있으므로 이 식은 집계 값을 기반으로 해야 합니다.  
  
### <a name="to-specify-a-custom-expression-for-a-summary-value"></a>요약 값을 위한 사용자 지정 식을 지정하려면  
  
1.  쿼리의 그룹을 지정합니다. 자세한 내용은 [쿼리 결과 행 그룹화&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/group-rows-in-query-results-visual-database-tools.md)를 참조하세요.  
  
2.  조건 창의 빈 행으로 이동한 다음 **열** 열에 식을 입력합니다.  
  
    [쿼리 및 뷰 디자이너](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)는 열 별칭을 식에 자동으로 할당하여 쿼리 출력에서 유용한 열 머리글을 만듭니다. 자세한 내용은 [열 별칭 만들기&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-column-aliases-visual-database-tools.md)를 참조하세요.  
  
3.  식의 **그룹화 방법** 열에서 **식**을 선택합니다.  
  
4.  쿼리를 실행합니다.  
  
## <a name="see-also"></a>참고 항목  
[쿼리 결과 정렬 및 그룹화&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[쿼리 결과 요약&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
  
