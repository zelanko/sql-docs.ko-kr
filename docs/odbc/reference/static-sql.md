---
title: 정적 SQL | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e6d053e4d2a5520432c4c1debbafb35fdb17bc4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016744"
---
# <a name="static-sql"></a>정적 SQL
Embedded SQL 에서처럼 [Embedded SQL 예제](../../odbc/reference/embedded-sql-example.md) 정적 SQL 이라고 합니다. 프로그램에서 SQL 문은 정적; 때문에 정적 SQL 라고 즉, 프로그램이 실행 될 때마다를 변경 하지 마십시오. 이전 섹션에서 설명한 대로, 프로그램의 나머지 부분을 컴파일하면 이러한 문이 컴파일됩니다.  
  
 정적 SQL 다양 한 상황에서 잘 작동 하 고는 데이터 액세스를 확인할 수 있습니다 프로그램 디자인 타임에 응용 프로그램에서 사용할 수 있습니다. 예를 들어, 주문 입력 프로그램 항상를 동일한 문을 사용 하 여 새 주문을 삽입 하 고는 항공편 예약 시스템에서 예약을 사용할 수는 사용자의 상태를 변경 하려면 동일한 문에서 항상 사용 합니다. 호스트 변수를 사용 하 여 일반화는 이러한 각 문은 판매 주문에 다른 값을 삽입할 수 있습니다 하 고 다른 사용자를 예약할 수 있습니다. 이러한 문의 일 수 있으므로 프로그램에 하드 코드 된 이러한 프로그램 문을 구문 분석, 유효성을 검사 하 고 컴파일 시간에 한 번만 최적화 해야 하는 장점이 있습니다. 이 인해 비교적 빠른 코드입니다.
