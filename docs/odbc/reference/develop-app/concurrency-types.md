---
title: 동시성 유형 | 마이크로 소프트 문서
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
- locking concurrency control [ODBC]
- optimistic concurrency [ODBC]
- read-only concurrency control [ODBC]
ms.assetid: 46762ae5-17dd-4777-968e-58156f470fe1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 642301d09c5aa189276db534e58aca0c5e00e3ce
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299103"
---
# <a name="concurrency-types"></a>동시성 형식
ODBC는 커서에서 동시성이 감소하는 문제를 해결하기 위해 다음 네 가지 유형의 커서 동시성을 노출합니다.  
  
-   **읽기 전용** 커서는 데이터를 읽을 수 있지만 데이터를 업데이트하거나 삭제할 수는 없습니다. 기본 동시성 유형입니다. DBMS는 반복 읽기 및 Serializable 격리 수준을 적용하기 위해 행을 잠글 수 있지만 쓰기 잠금 대신 읽기 잠금을 사용할 수 있습니다. 따라서 다른 트랜잭션은 적어도 데이터를 읽을 수 있기 때문에 동시성도 높아지게 됩니다.  
  
-   **잠금 장치** 커서는 결과 집합에서 행을 업데이트하거나 삭제할 수 있는지 확인하는 데 필요한 최하위 잠금 수준을 사용합니다. 이렇게 하면 일반적으로 반복 가능한 읽기 및 Serializable 트랜잭션 격리 수준에서 매우 낮은 동시성 수준이 발생합니다.  
  
-   **행 버전을 사용하는 낙관적 동시성 및 값을 사용하는 낙관적 동시성** 커서는 낙관적 동시성을 사용합니다: 마지막으로 읽은 이후 변경되지 않은 경우에만 행을 업데이트하거나 삭제합니다. 변경 내용을 검색하기 위해 행 버전 또는 값을 비교합니다. 커서가 행을 업데이트하거나 삭제할 수 있다는 보장은 없지만 잠금을 사용할 때보다 동시성이 훨씬 높습니다. 자세한 내용은 다음 섹션, [낙관적 동시성을](../../../odbc/reference/develop-app/optimistic-concurrency.md)참조하십시오.  
  
 응용 프로그램은 커서가 SQL_ATTR_CONCURRENCY 문 특성과 함께 사용할 동시성 유형을 지정합니다. 지원되는 형식을 확인하려면 SQL_SCROLL_CONCURRENCY 옵션을 사용하여 **SQLGetInfo를** 호출합니다.
