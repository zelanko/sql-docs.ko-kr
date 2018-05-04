---
title: 스크롤 가능 커서 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 2c8a5f50-9b37-452f-8160-05f42bc4d97e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6e779d551385c62ae8cddc5a2e7612b88095497
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="scrollable-cursors"></a>스크롤 가능 커서
최신 스크린 기반 응용 프로그램에서 사용자 데이터를 뒤로 및 앞으로 스크롤합니다. 이러한 응용 프로그램에 대 한 문제는 이전에 인출 된 행을 반환 합니다. 한 가지 예로 닫기 및 커서를 다시 열고 다음 커서 필요한 행에 도달할 때까지 행을 인출 합니다. 다른 가능한 결과 집합을 읽고 로컬에 캐시, 스크롤 응용 프로그램에서 구현 하는 것입니다. 두 가능성 작은 결과 집합에만 제대로 작동 하 고 후자의 가능성은 구현 하기가 어렵습니다. 더 나은 방법은 사용 하는 *스크롤 가능 커서* 결과 집합 마다 앞으로 또는 뒤로 이동 수입니다.  
  
 A *스크롤 가능 커서* 최신 스크린 기반 응용 프로그램에는 사용자에 의해 스크롤될 간에 데이터에서 일반적으로 사용 됩니다. 그러나 응용 프로그램을 사용 해야 스크롤 가능 커서 정방향 전용 커서는 작업을 수행 하지 것입니다 하는 경우에 스크롤 가능 커서는 정방향 전용 커서 보다 일반적으로 더 비쌉니다.  
  
 뒤로 이동 하는 기능 발생 질문 정방향 전용 커서에 적용할 수 없음: 스크롤 가능 커서를 검색 해야 이전에 가져온 행 변경 내용을? 즉, 업데이트, 삭제 및 새로 삽입 된 행을 검색할 해야 것 있나요?  
  
 이 질문 정의의 결과 설정 하기 때문에 발생-특정 조건에 일치 하는 행 집합-행 모두 검사 하 해당 조건에 일치 하거나 상태지 않습니다 것 있는지 여부를 확인 하는 경우에 나와 있지 않은 여부 행 데이터를 포함 해야 동일한은 인출 될 때마다 합니다. 이전 생략을 사용 하면 행 삽입 되거나 후자 것을 가능 하 게 하 여 업데이트 된 데이터를 검색 하는 동안 삭제 되었는지 여부를 검색 하는 스크롤 가능 커서에 대 한 수 있습니다.  
  
 변경 내용을 검색 하는 기능 경우에 따라 유용 하 게 경우가 아닌 경우 예를 들어 회계 프로그램 필요한 모든 변경 사항을; 무시 하는 커서 설명서 균형 조정 커서 최신 변경 내용을 표시 하는 경우에 수는 없습니다. 항공권 예약 시스템은 데이터에 대 한 최신 변경 내용을 보여 주는 커서를 요구 하는 반면에 이러한 커서 없이 가장 최신 비행 사용 가능한을 나타냅니다 데이터베이스를 계속 해 서 다시 해야 것입니다.  
  
 ODBC는 서로 다른 응용 프로그램의 요구를 처리 하려면 네 가지 종류의 스크롤 가능 커서를 정의 합니다. 이러한 커서는 비용에 둘 다를 변경 하 고 결과에 변경 내용을 검색 하는 기능에 설정 합니다. 참고는 스크롤 가능 커서 행의 변경 내용을 검색할 수 있는 경우만 감지할 수에 해당 행을 다시 인출 하려고 할 때 현재 인출 된 행의 변경 내용 커서에 알리기 위해 데이터 원본에 대 한 방법이 없습니다. 변경 내용 표시 된 트랜잭션 격리 수준을;에 의해 제어도 됩니다도 참고 자세한 내용은 참조 [트랜잭션 격리](../../../odbc/reference/develop-app/transaction-isolation.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [스크롤 가능 커서 유형](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [스크롤 가능 커서 사용](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [상대 및 절대 스크롤](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [책갈피](../../../odbc/reference/develop-app/bookmarks-odbc.md)
