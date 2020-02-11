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
ms.openlocfilehash: 434b27bffe3b32aa9fa0c5c6fd3a7100e8c7ea8d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138860"
---
# <a name="interoperability"></a>상호 운용성
*상호 운용성* 은 여러 dbms로 작동 하는 단일 응용 프로그램의 기능입니다. 상호 운용 가능한 제네릭 응용 프로그램을 작성 해야 하는 것은 ODBC 개발에 가장 중요 한 요소 중 하나 였습니다. 그러나 상호 운용성은 단순한 경로와 "상호 운용할 수 없습니다"에서 "완전히 상호 운용 가능"으로 진행 되지 않습니다. 경로에는 여러 분기가 있으며 각 분기에는 기능, 속도, 코드 복잡성 및 개발 시간 간의 장단점이 필요 합니다.  
  
 상호 운용 가능한 응용 프로그램을 작성 하는 프로세스는 여러 단계를 따릅니다.  
  
1.  응용 프로그램에서 ODBC를 사용할지 여부를 결정 합니다.  
  
2.  상호 운용성 수준을 선택 하 고 해당 수준에 도달 하는 데 필요한 장단점을 결정 합니다.  
  
3.  상호 운용 가능한 코드를 작성 하 고 가능한 한 완전히 테스트 합니다.  
  
 상호 운용성이 주로 응용 프로그램 작성기의 도메인 임을 유의 해야 합니다. 드라이버는 단일 DBMS에서 사용할 수 있도록 설계 되었으며, 정의에 따라 상호 운용할 수 없습니다. 단일 DBMS에서 ODBC를 올바르게 구현 하 고 노출 하 여 상호 운용성의 역할을 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ODBC가 응답입니까?](../../../odbc/reference/develop-app/is-odbc-the-answer.md)  
  
-   [상호 운용성 수준 선택](../../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)  
  
-   [대상 DBMS 및 드라이버 확인](../../../odbc/reference/develop-app/determining-the-target-dbmss-and-drivers.md)  
  
-   [사용할 데이터베이스 기능 고려](../../../odbc/reference/develop-app/considering-database-features-to-use.md)  
  
-   [제품 주기의 길이](../../../odbc/reference/develop-app/length-of-the-product-cycle.md)  
  
-   [상호 운용 가능한 애플리케이션 작성](../../../odbc/reference/develop-app/writing-an-interoperable-application.md)  
  
-   [상호 운용 가능한 애플리케이션 테스트](../../../odbc/reference/develop-app/testing-interoperable-applications.md)
