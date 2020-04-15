---
title: 상호 운용 가능한 응용 프로그램 작성 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 553e718e0759e47701e7f8c04561693358d5dc52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81289085"
---
# <a name="writing-an-interoperable-application"></a>상호 운용 가능한 애플리케이션 작성
응용 프로그램이 두 개 이상의 드라이버에 대해 동일한 코드를 사용할 때마다 해당 코드는 해당 드라이버 간에 상호 운용가능해야 합니다. 대부분의 경우 이 작업은 쉬운 작업입니다. 예를 들어 정방향 전용 커서가 있는 행을 가져오는 코드는 모든 드라이버에 대해 동일합니다. 경우에 따라 이 작업을 더 어려울 수 있습니다. 예를 들어 SQL 문에서 사용할 식별자를 생성하는 코드는 식별자 대/소문자, 인용 및 한 부분, 두 부분 및 세 부분으로 구성된 명명 규칙을 고려해야 합니다.  
  
 일반적으로 상호 운용 가능한 코드는 기능 지원 및 기능 가변성 문제에 대처해야 합니다. *기능 지원은* 특정 기능이 지원되는지 여부를 나타냅니다. 예를 들어 모든 DBMS가 트랜잭션을 지원하는 것은 아니며 상호 운용 가능한 코드는 트랜잭션 지원에 관계없이 올바르게 작동해야 합니다. *기능 가변성은* 특정 피쳐가 지원되는 방식의 변화를 나타냅니다. 예를 들어 카탈로그 이름은 일부 DBMS의 식별자의 시작 부분과 다른 DBMS의 식별자의 끝에 배치됩니다.  
  
 응용 프로그램은 설계 시 또는 런타임에 기능 지원 및 기능 가변성을 처리할 수 있습니다. 디자인 타임에 기능 지원 및 가변성을 처리하기 위해 개발자는 대상 DBMS 및 드라이버를 살펴보고 동일한 코드가 상호 운용되도록 합니다. 일반적으로 상호 운용성이 낮거나 제한된 응용 프로그램이 이러한 문제를 처리하는 방식입니다.  
  
 예를 들어 개발자가 세로 응용 프로그램이 4개의 특정 DBMS에서만 작동하도록 보장하고 각 DBMS가 트랜잭션을 지원하는 경우 응용 프로그램은 런타임에 트랜잭션 지원을 확인하는 코드가 필요하지 않습니다. 트랜잭션을 지원하는 각각 4개의 DBMS만 사용하도록 디자인 타임 결정으로 인해 트랜잭션을 사용할 수 있다고 항상 가정할 수 있습니다.  
  
 런타임에 기능 지원 및 가변성을 처리하려면 응용 프로그램은 런타임에 서로 다른 기능을 테스트하고 그에 따라 조치를 취해야 합니다. 일반적으로 상호 운용성이 높은 응용 프로그램이 이러한 문제를 처리하는 방식입니다. 기능 지원 문제의 경우 기능을 선택사항으로 만드는 코드를 작성하거나 기능을 사용할 수 없을 때 에뮬레이트하는 코드를 작성해야 합니다. 기능 가변성 문제의 경우 가능한 모든 변형을 지원하는 코드를 작성하는 것을 의미합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [기능 지원 및 가변성 확인](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [주목할 기능](../../../odbc/reference/develop-app/features-to-watch-for.md)
