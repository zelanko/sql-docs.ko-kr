---
title: 상호 운용성 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC]
- interoperability [ODBC], about interoperability
ms.assetid: 43b7c849-9d59-4002-9977-9e2c8730b859
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 486bfc2b144e8b228197b7b813af7aaebfe5b837
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913048"
---
# <a name="interoperability"></a>상호 운용성
*상호 운용성* 지원은 서로 다른 여러 Dbms와 함께 작동 하도록 단일 응용 프로그램의 기능입니다. 일반, 상호 운용 가능한 응용 프로그램을 작성할 필요가 ODBC의 개발에 중요 한 요인 중 하나 였습니다. 그러나 상호 운용성은 뒤에 "하지 상호 운용 가능"에서 간단한 경로가 아닙니다 "완전히 상호 운용 가능 합니다."를 경로 분기가 여러 개 및 각 균형을 맞추는 기능, 속도, 코드 복잡성 및 개발 시간이 필요 합니다.  
  
 상호 운용 가능한 응용 프로그램을 작성 하는 과정은 몇 가지 단계를 따릅니다.  
  
1.  응용 프로그램에서 ODBC를 사용할지 여부를 결정 해야 합니다.  
  
2.  상호 운용성 및 장단점은 해당 수준에 도달 하는 데 필요한 결정의 수준을 선택 합니다.  
  
3.  상호 운용 가능한 코드를 작성 하 고 가능한 한 완전 하 게 테스트 합니다.  
  
 상호 운용성은 응용 프로그램 기록기의 도메인 주로 하다는 점에 유의 해야 합니다. 드라이버는 단일 DBMS와 작동 하도록 설계 되었습니다 및 정의 따라 상호 운용 되지는 않습니다. 제대로 구현 하 고 단일 DBMS 통해 ODBC를 노출 하 여 상호 운용성에 영향을 줄 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ODBC가 응답입니까?](../../../odbc/reference/develop-app/is-odbc-the-answer.md)  
  
-   [상호 운용성 수준 선택](../../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)  
  
-   [대상 DBMS 및 드라이버 확인](../../../odbc/reference/develop-app/determining-the-target-dbmss-and-drivers.md)  
  
-   [사용할 데이터베이스 기능 고려](../../../odbc/reference/develop-app/considering-database-features-to-use.md)  
  
-   [제품 주기의 길이](../../../odbc/reference/develop-app/length-of-the-product-cycle.md)  
  
-   [상호 운용 가능한 응용 프로그램 작성](../../../odbc/reference/develop-app/writing-an-interoperable-application.md)  
  
-   [상호 운용 가능한 응용 프로그램 테스트](../../../odbc/reference/develop-app/testing-interoperable-applications.md)
