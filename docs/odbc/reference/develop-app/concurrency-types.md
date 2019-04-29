---
title: 동시성 유형은 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 12891d7ee674167157bcb02300d2e4181ef51734
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63012110"
---
# <a name="concurrency-types"></a>동시성 형식
ODBC는 커서의 축소 된 동시성 문제를 해결 하려면 네 가지 유형의 커서 동시성을 노출 합니다.  
  
-   **읽기 전용** 커서 수 데이터를 읽을 하지만 업데이트 하거나 삭제할 수 없습니다 데이터입니다. 기본 동시성 형식입니다. DBMS는 Repeatable Read 및 Serializable 격리 수준을 적용 하는 행 잠금을 수 있지만 쓰기 잠금 대신 읽기 잠금을 사용할 수 있습니다. 다른 트랜잭션을 하나 이상 데이터를 읽을 수 없으므로 더 높은 동시성 깔 합니다.  
  
-   **잠금** 커서 결과 집합의 행을 삭제 또는 업데이트할 수 있는지 확인 하는 데 필요한 잠금에 대 한 가장 낮은 수준의 사용 합니다. 이 일반적으로 Repeatable Read 및 Serializable 트랜잭션 격리 수준에서 특히 매우 낮은 동시성 수준에서 발생 합니다.  
  
-   **행 버전을 사용 하 여 낙관적 동시성 및 값을 사용 하 여 낙관적 동시성** 커서가 낙관적 동시성을 사용 합니다. 업데이트 또는 마지막으로 읽은 이후에 변경 되지 않은 경우에 행을 삭제 합니다. 변경 내용을 감지 하는 행 버전이 나 값 비교 합니다. 보장은 없습니다는 커서를 업데이트 하거나 행을 삭제할 수 있지만 동시성 잠금을 사용할 때 보다 훨씬 높습니다. 자세한 내용은 다음 섹션을 참조 하세요 [낙관적 동시성](../../../odbc/reference/develop-app/optimistic-concurrency.md)합니다.  
  
 응용 프로그램 커서 문 특성 SQL_ATTR_CONCURRENCY 사용 하려고 동시성 유형을 지정 합니다. 호출한 지 원하는 형식을 결정할 **SQLGetInfo** SQL_SCROLL_CONCURRENCY 옵션을 사용 합니다.
