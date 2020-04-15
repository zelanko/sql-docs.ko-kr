---
title: 상태 레코드 시퀀스 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 0e0436cc-230f-44b0-b373-04a57e83ee76
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bb26731a85d1d6313658fe9c24a32167b351d2d9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304174"
---
# <a name="sequence-of-status-records"></a>상태 레코드의 시퀀스
둘 이상의 상태 레코드가 반환되면 드라이버 관리자와 드라이버가 다음 규칙에 따라 순위를 지정합니다. 순위가 가장 높은 레코드는 첫 번째 레코드입니다. 레코드의 소스(드라이버 관리자, 드라이버, 게이트웨이 등)는 레코드의 순위를 매를 정할 때 고려되지 않습니다.  
  
-   **오류** 오류를 설명하는 상태 레코드의 순위가 가장 높습니다. 오류 레코드 중 트랜잭션 오류 또는 트랜잭션 오류 가능성을 나타내는 레코드가 다른 모든 레코드보다 우선합니다. 둘 이상의 레코드가 동일한 오류 조건을 설명하는 경우 Open 그룹 CLI 사양(클래스 03 ~ HZ)에 의해 정의된 SQLSTAT는 ODBC 정의 및 드라이버 정의 SQLSTATEs보다 앞선다.  
  
-   **구현 정의 데이터 값 없음** 드라이버 정의 데이터 없음 값(클래스 02)을 설명하는 상태 레코드의 순위가 두 번째로 높습니다.  
  
-   **경고 메시지** 경고(클래스 01)를 설명하는 상태 레코드의 순위가 가장 낮습니다. 둘 이상의 레코드가 동일한 경고 조건을 설명하는 경우 Open 그룹 CLI 사양에 정의된 경고 SQLSTATEs가 ODBC 정의 및 드라이버 정의 SQLSTATEs보다 앞선다.  
  
 순위가 가장 높은 레코드가 두 개 이상 있는 경우 첫 번째 레코드인 레코드가 정의되지 않습니다. 다른 모든 레코드의 순서는 정의되지 않습니다. 특히 오류가 발생하기 전에 경고가 나타날 수 있으므로 함수가 SQL_SUCCESS 이외의 값을 반환할 때 응용 프로그램은 모든 상태 레코드를 확인해야 합니다.
