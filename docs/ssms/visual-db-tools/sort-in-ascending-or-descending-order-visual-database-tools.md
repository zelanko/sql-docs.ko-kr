---
title: 오름차순 또는 내림차순으로 정렬(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- descending sorts
- ascending sorts
ms.assetid: d61cc55b-9ee8-4ecf-a32f-6459ae43910b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 37e81aef5c27f6302bfec677fdeff44ad2d59acb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47612967"
---
# <a name="sort-in-ascending-or-descending-order-visual-database-tools"></a>오름차순 또는 내림차순으로 정렬(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
**ASC** 또는 **DESC** 키워드를 **ORDER BY** 절과 함께 사용하면 결과 집합에 있는 하나 이상의 열에 대해 쿼리 결과를 오름차순이나 내림차순으로 정렬할 수 있습니다.  
  
> [!NOTE]  
> 정렬 순서는 부분적으로 열의 배치 순서에 따라 결정됩니다. [데이터 정렬 대화 상자](../../ssms/visual-db-tools/collation-dialog-box-visual-database-tools.md)에서 데이터 정렬 순서를 변경할 수 있습니다.  
  
다음 절차에서는 ORDER BY 절을 사용하여 하나 이상의 열을 정렬하는 쿼리를 뷰 디자이너에서 열고 있다고 가정합니다.  
  
### <a name="to-specify-or-change-the-order-in-which-results-are-sorted"></a>결과 정렬 순서를 지정하거나 변경하려면  
  
1.  [조건 창](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)에서 순서를 변경하려는 열의 **정렬 형식** 필드를 클릭합니다.  
  
2.  **오름차순** 이나 **내림차순** 을 선택하여 열의 정렬 순서를 지정합니다.  
  
조건 창에서 작업하는 경우 가장 최근의 동작에 일치하도록 쿼리의 UNION 절이 변경됩니다.  
  
> [!NOTE]  
> 여러 열을 기준으로 결과를 정렬하는 경우 정렬 순서 열을 사용하여 각 열에 대해 서로를 기준으로 열이 검색되는 순서를 지정합니다. 자세한 내용은 [쿼리에서 여러 열 정렬&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-multiple-columns-in-queries-visual-database-tools.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[쿼리 결과 정렬 및 그룹화&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[쿼리 결과 요약&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[쿼리 및 뷰 디자인 방법 도움말 항목&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
