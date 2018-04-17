---
title: 정적 SQL | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- static SQL [ODBC]
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- SQL statements [ODBC], static SQL
- embedded SQL [ODBC]
- SQL [ODBC], static SQL
ms.assetid: 667d92ec-fed9-4028-81d4-bb9ba867356a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 392cf843734bcc668c88f6408227b20df97d43ae
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="static-sql"></a>정적 SQL
에 표시 된 포함 된 SQL [포함 된 SQL 예제](../../odbc/reference/embedded-sql-example.md) 정적 SQL 라고 합니다. 프로그램의 SQL 문에 정적; 정적 SQL 라고 즉, 프로그램 실행 될 때마다를 변경 하지 마십시오. 이전 섹션에서 설명한 대로 이러한 문은 프로그램의 나머지를 컴파일할 때 컴파일됩니다.  
  
 정적 SQL 다양 한 상황에서 잘 작동 하 고 프로그램 디자인 타임에 확인할 수는 데이터 액세스를 모든 응용 프로그램에서 사용할 수 있습니다. 예를 들어 주문 입력 프로그램 항상는 동일한 문을 사용 하 여 새 주문을 삽입 하 고 항공권 예약 시스템에서 예약을 사용할 수 있는 한 라이선스 상태를 변경 하려면 항상 동일한 문에서 사용 합니다. 호스트 변수를 사용 하 여 일반화는 이러한 각 문은 판매 주문에 다른 값을 삽입할 수 및 다른 사용자를 예약할 수 있습니다. 이러한 문의 프로그램에 하드 코드 될 수 있습니다, 때문에 이러한 프로그램은 문을 구문 분석, 유효성을 검사 하 고 컴파일 시간에 한 번만 최적화 하는 장점이 많습니다. 이 인해 상대적으로 속도가 빠른 코드입니다.
