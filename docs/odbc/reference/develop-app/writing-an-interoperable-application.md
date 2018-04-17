---
title: 상호 운용 가능한 응용 프로그램 작성 | Microsoft Docs
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
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: 8b42b8ae-7862-4b63-a0b3-2a204e0c43a5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8a0b70251acdfebbe05bb0900af8be7ea25b6fa6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="writing-an-interoperable-application"></a>상호 운용 가능한 응용 프로그램 작성
응용 프로그램 둘 이상의 드라이버에 대해 동일한 코드를 사용할 때마다 해당 코드 드라이버만 간에 상호 운용 가능 해야 합니다. 대부분의 경우 쉬운 일입니다. 예를 들어, 정방향 전용 커서와 함께 행을 인출 하는 코드에 대 한 모든 드라이버 같습니다. 경우에 따라이 어려울 수 있습니다. 예를 들어 SQL 문에서 사용에 대 한 식별자를 생성 하는 코드는 식별자의 대/소문자, 인용 부호를 및 한 부분, 두 부분 및 세 부분으로 이루어진 명명 규칙을 고려해 야 합니다.  
  
 일반적으로 상호 운용 가능한 코드의 기능 지원 및 기능은 변경 사항 문제 처리 해야 합니다. *기능 지원을* 특정 기능이 지원 되는지 여부를 나타냅니다. 예를 들어 일부 Dbms 트랜잭션을 지원 하 고 상호 운용 가능한 코드 트랜잭션 지원에 관계 없이 제대로 작동 해야 합니다. *가변성 기능* 은 특정 기능이 지원 되는지 방식에서 편차를 나타냅니다. 예를 들어 카탈로그 이름 끝에 있고 다른 식별자 및 일부 Dbms에 있는 식별자의 시작 부분에 배치 됩니다.  
  
 디자인 타임 또는 런타임에 응용 프로그램의 기능 지원 및 기능은 변경 사항 처리할 수 있습니다. 디자인 타임에 기능 지원 및 가변성 다루기가, 개발자 대상 Dbms 및 드라이버를 살펴보고 하 고 동일한 코드 간에 상호 운용 가능한 되도록 확인 합니다. 이것이 일반적으로 응용 프로그램 낮은 또는 제한 된 상호 운용성을 이러한 문제를 처리 하는 방법입니다.  
  
 예를 들어 개발자는 세로 응용 프로그램이 작동 하는지만 4 개의 특정 Dbms 보장 및 각 해당 Dbms에서 트랜잭션을 지원 하면 응용 프로그램이 필요는 없습니다 실행 시 트랜잭션 지원을 확인 하는 코드. 디자인 타임을 했으므로 4 Dbms를 사용 하 여 트랜잭션을 지원 하며 각 트랜잭션을 사용할 수 있는 항상 가정할 수 있습니다.  
  
 런타임 시 기능 지원 및 가변성 다루기가, 응용 프로그램 실행 시 다양 한 기능에 대 한 테스트 하 고 적절 하 게 작동 해야 합니다. 이 일반적으로는 높은 상호 운용 가능한 응용 프로그램이 이러한 문제를 처리 하는 방법입니다. 기능 지원 문제에 대 한 코드를 사용할 수 없는 경우 기능을 에뮬레이션 하는 기능 옵션 또는 작성 코드 작성을 의미 합니다. 기능 변경 사항 문제에 대 한 코드를 지 원하는 모든 가능한 변형을 작성을 의미 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [기능 지원 및 가변성 확인](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [주목할 기능](../../../odbc/reference/develop-app/features-to-watch-for.md)
