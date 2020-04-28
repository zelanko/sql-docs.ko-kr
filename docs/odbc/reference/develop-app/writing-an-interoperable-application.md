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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 553e718e0759e47701e7f8c04561693358d5dc52
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81289085"
---
# <a name="writing-an-interoperable-application"></a>상호 운용 가능한 애플리케이션 작성
응용 프로그램에서 둘 이상의 드라이버에 대해 동일한 코드를 사용할 때마다 해당 코드는 해당 드라이버 간에 상호 운용이 가능 해야 합니다. 대부분의 경우에는이 작업을 쉽게 수행할 수 있습니다. 예를 들어 앞 으로만 이동 가능한 커서를 사용 하 여 행을 인출 하는 코드는 모든 드라이버에 대해 동일 합니다. 일부 경우에는이 방법이 더 어려울 수 있습니다. 예를 들어 SQL 문에 사용할 식별자를 생성 하는 코드는 식별자의 대/소문자, 따옴표, 한 부분, 두 부분, 세 부분으로 구성 된 명명 규칙을 고려해 야 합니다.  
  
 일반적으로 상호 운용 가능한 코드는 기능 지원 및 기능 산포도의 문제를 해결 해야 합니다. *기능 지원은* 특정 기능이 지원 되는지 여부를 나타냅니다. 예를 들어 일부 Dbms는 트랜잭션을 지원 하지 않으며, 상호 운용 가능한 코드는 트랜잭션 지원에 관계 없이 제대로 작동 해야 합니다. *기능의 가변성* 은 특정 기능이 지원 되는 방식으로 변형 된 것을 의미 합니다. 예를 들어 카탈로그 이름은 일부 Dbms에서 식별자의 시작 부분에 배치 되 고 다른 Dbms에서는 식별자의 끝에 배치 됩니다.  
  
 응용 프로그램은 디자인 타임 또는 런타임에 기능 지원 및 기능 산포도를 처리할 수 있습니다. 디자인 타임에 기능 지원 및 가변성을 처리 하기 위해 개발자는 대상 Dbms 및 드라이버를 확인 하 고 같은 코드를 상호 운용할 수 있습니다. 이는 일반적으로 상호 운용성이 낮거나 제한 된 응용 프로그램이 이러한 문제를 해결 하는 방법입니다.  
  
 예를 들어 개발자가 세로 응용 프로그램이 4 개의 특정 Dbms 에서만 작동 하도록 보장 하 고 각 Dbms에서 트랜잭션을 지 원하는 경우 응용 프로그램은 런타임에 트랜잭션 지원을 확인 하는 코드가 필요 하지 않습니다. 항상 트랜잭션을 지 원하는 4 개의 Dbms만 사용 하도록 디자인 타임 결정으로 인해 트랜잭션을 사용할 수 있다고 가정할 수 있습니다.  
  
 런타임에 기능 지원과 가변성을 처리 하려면 응용 프로그램에서 런타임에 다른 기능을 테스트 하 고 적절 하 게 작동 해야 합니다. 이는 일반적으로 상호 운용 가능성이 매우 큰 응용 프로그램이 이러한 문제를 처리 하는 방법입니다. 기능 지원 문제에 대해 기능을 사용할 수 없는 경우 기능을 에뮬레이트하는 코드를 작성 하는 코드를 작성 하는 것이 좋습니다. 기능 변동 문제의 경우 가능한 모든 변형을 지 원하는 코드를 작성 해야 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [기능 지원 및 가변성 확인](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [주목할 기능](../../../odbc/reference/develop-app/features-to-watch-for.md)
