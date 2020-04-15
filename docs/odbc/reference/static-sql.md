---
title: 정적 SQL | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- static SQL [ODBC]
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- SQL statements [ODBC], static SQL
- embedded SQL [ODBC]
- SQL [ODBC], static SQL
ms.assetid: 667d92ec-fed9-4028-81d4-bb9ba867356a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55710d8ea734cba86ae5e4daa725f75e94e65a64
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81279905"
---
# <a name="static-sql"></a>정적 SQL
[임베디드 SQL 예제에](../../odbc/reference/embedded-sql-example.md) 표시된 임베디드 SQL을 정적 SQL이라고 합니다. 프로그램의 SQL 문이 정적이기 때문에 정적 SQL이라고 합니다. 즉, 프로그램이 실행될 때마다 변경되지 않습니다. 이전 섹션에서 설명한 대로 이러한 문은 프로그램의 나머지 부분을 컴파일할 때 컴파일됩니다.  
  
 정적 SQL은 많은 상황에서 잘 작동하며 프로그램 디자인 시간에 데이터 액세스를 결정할 수 있는 모든 응용 프로그램에서 사용할 수 있습니다. 예를 들어, 주문 입력 프로그램은 항상 동일한 명세서를 사용하여 새 주문을 삽입하고, 항공사 예약 시스템은 항상 동일한 명세서를 사용하여 좌석 상태를 사용 가능한 좌석에서 예약으로 변경합니다. 이러한 각 문은 호스트 변수를 사용하여 일반화됩니다. 다른 값을 판매 주문에 삽입할 수 있으며 다른 좌석을 예약할 수 있습니다. 이러한 문은 프로그램에서 하드 코딩할 수 있으므로 이러한 프로그램은 컴파일 타임에 한 번만 구문 분석, 유효성 검사 및 최적화해야 한다는 장점이 있습니다. 이로 인해 비교적 빠른 코드가 생성됩니다.
