---
title: 스크롤 가능한 커서 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 2c8a5f50-9b37-452f-8160-05f42bc4d97e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2762ffc7fa179fc6a68f92c23f92ca12803f5ab7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304214"
---
# <a name="scrollable-cursors"></a>스크롤 가능 커서
최신 화면 기반 응용 프로그램에서 사용자는 데이터를 앞뒤로 스크롤합니다. 이러한 응용 프로그램의 경우 이전에 가져온 행으로 돌아가는 것이 문제입니다. 한 가지 가능성은 커서를 닫고 다시 연 다음 커서가 필요한 행에 도달할 때까지 행을 가져오는 것입니다. 또 다른 가능성은 결과 집합을 읽고, 로컬로 캐시하고, 응용 프로그램에서 스크롤을 구현하는 것입니다. 두 가지 가능성은 작은 결과 집합에서만 잘 작동하며 후자의 가능성은 구현하기가 어렵습니다. 더 나은 해결책은 결과 집합에서 앞뒤로 이동할 수 있는 *스크롤 가능한 커서를* 사용하는 것입니다.  
  
 *스크롤 가능한 커서는* 사용자가 데이터를 앞뒤로 스크롤하는 최신 화면 기반 응용 프로그램에서 일반적으로 사용됩니다. 그러나 스크롤 가능한 커서가 일반적으로 정방향 전용 커서보다 비용이 많이 들기 때문에 응용 프로그램은 정방향 전용 커서가 작업을 수행하지 않는 경우에만 스크롤 가능한 커서를 사용해야 합니다.  
  
 뒤로 이동하는 기능은 앞으로 전용 커서에 적용되지 않는 질문을 제기합니다: 스크롤 가능한 커서가 이전에 가져온 행에 대한 변경 내용을 검색해야 합니까? 즉, 업데이트, 삭제 및 새로 삽입된 행을 검색해야 합니까?  
  
 이 질문은 특정 조건과 일치하는 행 집합인 결과 집합의 정의가 행이 해당 기준과 일치하는지 여부를 확인하기 위해 검사할 때 명시되지 않으며, 행이 가져올 때마다 동일한 데이터를 포함해야 하는지 여부를 명시하지 않기 때문에 발생합니다. 전자 누락을 사용하면 스크롤 가능한 커서가 행이 삽입 또는 삭제되었는지 여부를 감지할 수 있으며, 후자는 업데이트된 데이터를 검색할 수 있습니다.  
  
 변경 내용을 검색하는 기능은 유용할 때도 있으며 그렇지 않은 경우도 있습니다. 예를 들어 회계 응용 프로그램에는 모든 변경 내용을 무시하는 커서가 필요합니다. 커서가 최신 변경 사항을 표시하는 경우 책의 균형을 맞추는 것은 불가능합니다. 반면에 항공사 예약 시스템에는 데이터의 최신 변경 내용을 표시하는 커서가 필요합니다. 이러한 커서가 없으면 데이터베이스를 지속적으로 다시 쿼리하여 최신 항공편 가용성을 보여야 합니다.  
  
 ODBC는 다양한 응용 프로그램의 요구 사항을 충족하기 위해 네 가지 유형의 스크롤 가능한 커서를 정의합니다. 이러한 커서는 비용과 결과 집합의 변경 내용을 검색하는 능력이 모두 다릅니다. 스크롤 가능한 커서가 행의 변경 내용을 검색할 수 있는 경우 해당 행을 다시 가져오려고 할 때만 해당 커서를 검색할 수 있습니다. 데이터 원본이 현재 가져온 행에 대한 변경 내용을 커서에 알릴 수 있는 방법은 없습니다. 또한 변경 에 대한 가시성은 트랜잭션 격리 수준에 의해 제어됩니다. 자세한 내용은 [트랜잭션 격리](../../../odbc/reference/develop-app/transaction-isolation.md)를 참조하십시오.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [스크롤 가능 커서 형식](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [스크롤 가능 커서 사용](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [상대 및 절대 스크롤](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [책갈피](../../../odbc/reference/develop-app/bookmarks-odbc.md)
