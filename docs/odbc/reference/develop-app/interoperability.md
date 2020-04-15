---
title: 상호 운용성 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC]
- interoperability [ODBC], about interoperability
ms.assetid: 43b7c849-9d59-4002-9977-9e2c8730b859
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31b20a696c601ff91c591e4c717f468beca34e36
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306224"
---
# <a name="interoperability"></a>상호 운용성
*상호 운용성은* 단일 응용 프로그램이 다양한 DBMS로 작동할 수 있는 기능입니다. 상호 운용 가능한 일반 응용 프로그램을 작성해야 하는 필요성은 ODBC 개발로 이어지는 주요 요인 중 하나였습니다. 그러나 상호 운용성은 "상호 운용 가능하지 않음"에서 "완전히 상호 운용 가능"으로 이어지는 간단한 경로가 아닙니다. 경로에는 여러 분기가 있으며 각 분기에는 기능, 속도, 코드 복잡성 및 개발 시간 간의 절충이 필요합니다.  
  
 상호 운용 가능한 응용 프로그램을 작성하는 프로세스는 다음과 같은 몇 가지 단계를 따릅니다.  
  
1.  응용 프로그램이 ODBC를 사용할지 여부를 결정합니다.  
  
2.  상호 운용성 수준을 선택하고 해당 수준에 도달하는 데 필요한 절충점을 결정합니다.  
  
3.  상호 운용 가능한 코드를 작성하고 가능한 한 완벽하게 테스트합니다.  
  
 상호 운용성은 주로 응용 프로그램 작성기의 도메인이라는 점에 유의해야 합니다. 드라이버는 단일 DBMS로 작동하도록 설계되었으며 정의에 따라 상호 운용할 수 없습니다. 단일 DBMS를 통해 ODBC를 올바르게 구현하고 노출하여 상호 운용성에서 역할을 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ODBC가 응답입니까?](../../../odbc/reference/develop-app/is-odbc-the-answer.md)  
  
-   [상호 운용성 수준 선택](../../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)  
  
-   [대상 DBMS 및 드라이버 확인](../../../odbc/reference/develop-app/determining-the-target-dbmss-and-drivers.md)  
  
-   [사용할 데이터베이스 기능 고려](../../../odbc/reference/develop-app/considering-database-features-to-use.md)  
  
-   [제품 주기의 길이](../../../odbc/reference/develop-app/length-of-the-product-cycle.md)  
  
-   [상호 운용 가능한 애플리케이션 작성](../../../odbc/reference/develop-app/writing-an-interoperable-application.md)  
  
-   [상호 운용 가능한 애플리케이션 테스트](../../../odbc/reference/develop-app/testing-interoperable-applications.md)
