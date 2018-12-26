---
title: 상호 운용 가능한 응용 프로그램 작성 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: 8b42b8ae-7862-4b63-a0b3-2a204e0c43a5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8e559eab5787a64b6bdf0850147d7d9128fc435c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47757261"
---
# <a name="writing-an-interoperable-application"></a>상호 운용 가능한 애플리케이션 작성
응용 프로그램에 둘 이상의 드라이버에 대해 동일한 코드를 사용 하는 때마다 코드 드라이버만 간에 상호 운용 가능한 이어야 합니다. 대부분의 경우에는 쉽게 작업입니다. 예를 들어, 정방향 전용 커서를 사용 하 여 행을 인출 하는 코드는 모든 드라이버에 대 한 동일 합니다. 경우에 따라이 더 어려울 수 있습니다. 예를 들어 SQL 문에서 사용에 대 한 식별자를 생성 하는 코드 식별자 대/소문자, 인용 부호를 및 한 부분, 두 부분, 및 세 부분으로 이루어진 명명 규칙을 고려해 야 합니다.  
  
 일반적으로 상호 운용 가능한 코드 기능 지원 및 기능 가변성 문제에 대처 해야 합니다. *기능 지원을* 특정 기능이 지원 되는지 여부를 나타냅니다. 예를 들어, 일부 Dbms 트랜잭션 지원 및 상호 운용 가능한 코드 트랜잭션 지원에 관계 없이 올바르게 작동 해야 합니다. *가변성 기능* 는 특정 기능을 지원 되는 방식으로 편차를 나타냅니다. 예를 들어, 카탈로그 이름은 일부 Dbms에 있는 식별자의 시작 및 끝 다른 식별자에 배치 됩니다.  
  
 응용 프로그램을 디자인 타임 또는 런타임에 기능 지원 및 가변성 기능을 사용 하 여 처리할 수 있습니다. 디자인 타임 기능 지원 및 가변성을 사용 하 여 처리, 개발자 대상 Dbms 및 드라이버를 확인 하 고 동일한 코드 간의 상호 운용 되도록 확인 합니다. 이 방법이 일반적으로는 낮은 또는 제한 된 상호 운용성을 사용 하 여 응용 프로그램 이러한 문제를 처리 합니다.  
  
 예를 들어 개발자는 수직적 응용 프로그램 에서만 작동 4 특정 Dbms 보장 및 각 해당 Dbms에서 트랜잭션을 지원 하면 응용 프로그램 필요는 없습니다 런타임에 트랜잭션 지원을 확인 하는 코드. 항상 트랜잭션을 지 원하는 각 네 개의 Dbms를 사용 하도록 디자인 타임 결정으로 인해 트랜잭션을 사용할 수 있는 가정할 수 있습니다.  
  
 런타임에 기능 지원 및 가변성을 사용 하 여 처리를 응용 프로그램 실행 시 다양 한 기능에 대 한 테스트 하 고 적절 하 게 작동 해야 합니다. 이 방법이 일반적으로는 응용 프로그램 상호 운용성이 매우 이러한 문제를 처리 합니다. 기능 지원 문제에 대 한 기능 선택적 또는 작성 코드를 사용할 수 없을 때 기능을 에뮬레이트하는 코드를 작성을 의미 합니다. 기능 가변성 문제에 대 한 모든 가능한 변형을 지 원하는 코드를 작성을 의미 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [기능 지원 및 가변성 확인](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [주목할 기능](../../../odbc/reference/develop-app/features-to-watch-for.md)
