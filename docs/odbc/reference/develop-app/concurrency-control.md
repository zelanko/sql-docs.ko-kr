---
title: 동시성 제어 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
ms.assetid: 75e4adb3-3d43-49c5-8c5e-8df96310d912
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8afba3b3b8c8fee1307473c790186d509b37d982
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294853"
---
# <a name="concurrency-control"></a>동시성 제어
*동시성은* 두 트랜잭션이 동시에 동일한 데이터를 사용할 수 있는 기능이며 트랜잭션 격리가 증가하면 일반적으로 동시성이 줄어듭니다. 이는 일반적으로 행을 잠그면 트랜잭션 격리가 구현되고 더 많은 행이 잠기면 잠긴 행에 의해 일시적으로 차단되지 않고 더 적은 트랜잭션을 완료할 수 있기 때문입니다. 감소된 동시성은 일반적으로 데이터베이스 무결성을 유지하는 데 필요한 높은 트랜잭션 격리 수준에 대한 절충으로 허용되지만 커서를 사용하는 읽기/쓰기 활동이 많은 대화형 응용 프로그램에서문제가 될 수 있습니다.  
  
 예를 들어 응용 프로그램이 **주문에서 선택SQL \* **문을 실행한다고 가정합니다. 결과 집합 주위를 스크롤하기 위해 **SQLFetchScroll을** 호출하고 사용자가 주문을 업데이트, 삭제 또는 삽입할 수 있도록 합니다. 사용자가 주문을 업데이트, 삭제 또는 삽입하면 응용 프로그램이 트랜잭션을 커밋합니다.  
  
 격리 수준이 반복 읽기인 경우 트랜잭션이 구현되는 방식에 따라 **SQLFetchScroll**에서 반환되는 각 행을 잠글 수 있습니다. 격리 수준이 Serializable인 경우 트랜잭션이 전체 Orders 테이블을 잠글 수 있습니다. 두 경우 모두 트랜잭션이 커밋되거나 롤백될 때만 잠금을 해제합니다. 따라서 사용자가 주문을 읽는 데 많은 시간을 소비하고 업데이트, 삭제 또는 삽입하는 데 거의 시간을 소비하는 경우 트랜잭션은 많은 수의 행을 쉽게 잠그어 다른 사용자가 사용할 수 없게 만들 수 있습니다.  
  
 이 문제는 커서가 읽기 전용이고 응용 프로그램에서 사용자가 기존 주문만 읽을 수 있도록 허용하는 경우에도 문제가 됩니다. 이 경우 응용 프로그램은 트랜잭션을 커밋하고 **SQLCloseCursor(자동** 커밋 모드에서) 또는 **SQLEndTran(수동** 커밋 모드에서)을 호출할 때 잠금을 해제합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [동시성 형식](../../../odbc/reference/develop-app/concurrency-types.md)  
  
-   [낙관적 동시성](../../../odbc/reference/develop-app/optimistic-concurrency.md)
