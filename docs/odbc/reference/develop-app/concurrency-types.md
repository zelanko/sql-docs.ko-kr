---
title: "동시성 유형은 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
- locking concurrency control [ODBC]
- optimistic concurrency [ODBC]
- read-only concurrency control [ODBC]
ms.assetid: 46762ae5-17dd-4777-968e-58156f470fe1
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 737fadc881109457051cf30bfce9b493bd164f1c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="concurrency-types"></a>동시성 유형
ODBC는 커서의 감소 동시성 문제를 해결 하려면 네 가지 유형의 커서 동시성을 제공 합니다.  
  
-   **읽기 전용** 커서 데이터를 읽을 수 있지만 업데이트 수 없습니다 또는 데이터를 삭제 합니다. 기본 동시성 형식입니다. DBMS Repeatable Read 및 Serializable 격리 수준을 적용 하는 행을 잠그는 수 있지만 읽기 잠금을 쓰기 잠금 대신 사용할 수 있습니다. 그러면 더 높은 동시성 하므로 다른 트랜잭션이 데이터를 읽을 수 이상입니다.  
  
-   **잠금** 커서 가장 낮은 수준의 업데이트나 결과 집합의 행을 삭제할 수 있는지 확인 하는 데 필요한 잠금을 사용 합니다. 일반적으로 매우 낮은 동시성 수준이 Repeatable Read 및 Serializable 트랜잭션 격리 수준에서 특히 발생 합니다.  
  
-   **행 버전을 사용 하 여 낙관적 동시성 및 값을 사용 하는 낙관적 동시성** 낙관적 동시성을 사용 하는 커서: 업데이트 또는 마지막으로 읽은 후 변경 되지 않은 경우에 행을 삭제 합니다. 변경 내용을 감지에 행 버전 또는 값을 비교 합니다. 보장이 없습니다 커서를 업데이트 하거나 행을 삭제할 수 있지만 동시성 잠금을 사용할 때 보다 훨씬 높습니다. 자세한 내용은 다음 섹션을 참조 하십시오. [낙관적 동시성](../../../odbc/reference/develop-app/optimistic-concurrency.md)합니다.  
  
 응용 프로그램을 문 특성 SQL_ATTR_CONCURRENCY 사용 하면 커서 브로드캐스트하며 동시성 유형을 지정 합니다. 지원 되는 형식을 확인 하려면 호출 **SQLGetInfo** SQL_SCROLL_CONCURRENCY 옵션을 사용 합니다.
