---
title: 스크롤 가능 커서 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 70d02b933104a3106d95f6760cbdcf0abb347716
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47791560"
---
# <a name="scrollable-cursors"></a>스크롤 가능 커서
최신 화면 기반 응용 프로그램에서 사용자 데이터를 뒤로 및 앞으로 스크롤합니다. 이러한 응용 프로그램에 대 한 이전에 인출된 된 행을 반환 합니다. 문제가 있는 경우 한 가지 방법은 닫습니다 하 고 커서를 닫은 후 커서 필요한 행에 도달할 때까지 행을 인출 하는 것입니다. 다른 방법은 결과 집합을 읽고, 로컬로 캐시 하 고, 응용 프로그램에서 스크롤을 구현 하는 것입니다. 모두 가능성 결과 집합이 작은 경우 에서만 잘 작동 하 고 두 번째 가능성은 구현 하기가 어렵습니다. 더 나은 방법은 사용 하는 *스크롤 가능 커서* 뒤로 이동할 수 있으며 결과 집합에 전달 합니다.  
  
 A *스크롤 가능 커서* 최신 화면 기반 응용 프로그램에는 사용자가 스크롤할 앞뒤로 데이터에서 일반적으로 사용 됩니다. 그러나 응용 프로그램 사용 해야 스크롤 가능 커서 정방향 전용 커서 작업을 수행 하지 것입니다 하는 경우에 스크롤 가능 커서는 정방향 전용 커서 보다 일반적으로 더 비쌉니다.  
  
 뒤로 이동 기능을 정방향 전용 커서에 적용할 수 없는 질문을 발생 시킵니다: 스크롤 가능 커서를 감지 해야 이전에 가져온 행 변경 내용을? 업데이트, 삭제 및 새로 삽입 된 행을 검색 해야, 해야 하지?  
  
 결과의 정의 설정 하기 때문에이 질문 발생-특정 기준과 일치 하는 행 집합-때 행을 확인 하는 조건과 일치 하는 나이 상태는 여부를 나타내지는지 않습니다 여부 행 데이터를 포함 해야 동일한 인출 될 때마다 합니다. 이전 생략은 스크롤 가능 커서 행 삽입 되거나 후자 수 있도록 하 여 업데이트 된 데이터를 검색 하는 동안 삭제 되었는지 여부를 검색할 수 있도록 만듭니다.  
  
 변경 내용을 검색 하는 기능 경우가 있습니다 경우에 따라 유용 하지 않습니다. 예를 들어, 회계 응용 프로그램에 필요한 모든 변경 사항을; 무시 하는 커서 온라인 설명서를 균형 조정 커서 최신 변경 내용을 표시 되 면 수는 없습니다. 다른 한편으로 항공편 예약 시스템 필요한 데이터를 최신 변경 내용을 보여 주는 커서 이러한 커서 없이 최신 비행 가용성을 표시 하려면 데이터베이스를 지속적으로 다시 해야 것입니다.  
  
 다른 응용 프로그램의 요구를 해결 하기 위해 ODBC 네 가지 유형의 스크롤 가능 커서를 정의 합니다. 이러한 커서 모두 비용 다르며 결과에 변경 내용을 검색 하는 기능에서을 설정 합니다. 참고는 스크롤 가능 커서를 행에 변경 내용을 검색 하 고, 경우만 감지할 수에 해당 행을 다시 페치 하려고 할 때 데이터 원본으로 현재 인출된 된 행의 변경 내용 커서에 알릴 방법이 없습니다. 변경 내용 표시를 트랜잭션 격리 수준을; 제어는 물론을 참고 자세한 내용은 [트랜잭션 격리](../../../odbc/reference/develop-app/transaction-isolation.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [스크롤 가능 커서 유형](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [스크롤 가능 커서 사용](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [상대 및 절대 스크롤](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [책갈피](../../../odbc/reference/develop-app/bookmarks-odbc.md)
