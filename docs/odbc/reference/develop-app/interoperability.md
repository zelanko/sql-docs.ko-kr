---
title: 상호 운용성 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8d5e4fbee458bec88461d3e2945a466c848d3345
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62446490"
---
# <a name="interoperability"></a>상호 운용성
*상호 운용성* 은 여러 다른 Dbms를 사용 하 여 작동 하는 단일 응용 프로그램의 기능입니다. 제네릭, 상호 운용 가능한 응용 프로그램을 작성할 필요가 앞에 ODBC의 개발에 중요 한 요인 중 하나 였습니다. 그러나 상호 운용성이 뒤에 "하지 상호 운용 가능한"에서 간단한 경로에 "완전히 상호 운용 가능 합니다." 경로 많은 분기가 있고 각 기능, 속도, 코드 복잡성 및 개발 시간 간의 절충이 필요 합니다.  
  
 상호 운용 가능한 응용 프로그램을 작성 하는 프로세스는 몇 가지 단계를 따릅니다.  
  
1.  응용 프로그램에서 ODBC를 사용할지 여부를 결정 합니다.  
  
2.  수준의 상호 운용성 및 장단점은 해당 수준에 도달 하는 데 필요한 결정을 선택 합니다.  
  
3.  상호 운용 가능한 코드를 작성 하 고 가능한 완벽 하 게 테스트 합니다.  
  
 상호 운용성 주로 응용 프로그램 작성자의 도메인 인지 확인 해야 합니다. 드라이버는 단일 DBMS를 사용 하 여 작동 하도록 설계 되었습니다 및 정의 따라 상호 운용 되지는 않습니다. 이러한 역할을 상호 운용성에 올바르게 구현 하 고 단일 DBMS를 통해 ODBC를 노출 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ODBC가 응답입니까?](../../../odbc/reference/develop-app/is-odbc-the-answer.md)  
  
-   [상호 운용성 수준 선택](../../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)  
  
-   [대상 DBMS 및 드라이버 확인](../../../odbc/reference/develop-app/determining-the-target-dbmss-and-drivers.md)  
  
-   [사용할 데이터베이스 기능 고려](../../../odbc/reference/develop-app/considering-database-features-to-use.md)  
  
-   [제품 주기의 길이](../../../odbc/reference/develop-app/length-of-the-product-cycle.md)  
  
-   [상호 운용 가능한 애플리케이션 작성](../../../odbc/reference/develop-app/writing-an-interoperable-application.md)  
  
-   [상호 운용 가능한 애플리케이션 테스트](../../../odbc/reference/develop-app/testing-interoperable-applications.md)
