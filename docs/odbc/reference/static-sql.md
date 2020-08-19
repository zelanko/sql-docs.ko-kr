---
description: 정적 SQL
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19c4ec3454a5d5891a87203fe8c7aeaff21b239b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428985"
---
# <a name="static-sql"></a>정적 SQL
[EMBEDDED Sql 예제](../../odbc/reference/embedded-sql-example.md) 에 표시 된 포함 된 sql을 정적 sql 이라고 합니다. 이는 프로그램의 SQL 문이 정적 이므로 정적 SQL 이라고 합니다. 즉, 프로그램이 실행 될 때마다 변경 되지 않습니다. 이전 섹션에서 설명한 대로 이러한 문은 프로그램의 나머지 부분이 컴파일될 때 컴파일됩니다.  
  
 정적 SQL은 다양 한 상황에서 효과적으로 작동 하며, 프로그램 디자인 타임에 데이터 액세스를 확인할 수 있는 모든 응용 프로그램에서 사용할 수 있습니다. 예를 들어 주문 입력 프로그램은 항상 같은 문을 사용 하 여 새 주문을 삽입 하 고 항공 예약 시스템은 항상 동일한 문을 사용 하 여 사용자의 상태를 사용 가능에서 예약 됨으로 변경 합니다. 이러한 각 문은 호스트 변수를 사용 하 여 일반화 됩니다. 판매 주문에는 다른 값을 삽입할 수 있으며 다른 사용자는 예약할 수 있습니다. 이러한 문은 프로그램에서 하드 코드 될 수 있으므로 이러한 프로그램은 컴파일 시간에 문을 구문 분석 하 고, 유효성을 검사 하 고 한 번만 최적화 해야 한다는 장점이 있습니다. 이로 인해 비교적 빠른 코드가 생성 됩니다.
