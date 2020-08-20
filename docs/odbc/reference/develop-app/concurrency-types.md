---
description: 동시성 형식
title: 동시성 유형 | Microsoft Docs
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
ms.openlocfilehash: d55740b71d4e9a7d3b8d22400da0c5b3d94e73d3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461545"
---
# <a name="concurrency-types"></a>동시성 형식
커서에서 동시성 감소 문제를 해결 하기 위해 ODBC는 네 가지 유형의 커서 동시성을 노출 합니다.  
  
-   **읽기** 전용 커서는 데이터를 읽을 수 있지만 데이터를 업데이트 하거나 삭제할 수는 없습니다. 이는 기본 동시성 유형입니다. DBMS에서 반복 읽기 및 직렬화 가능 격리 수준을 적용 하기 위해 행을 잠글 수 있지만 쓰기 잠금 대신 읽기 잠금을 사용할 수 있습니다. 이로 인해 다른 트랜잭션이 데이터를 최소한으로 읽을 수 있으므로 동시성이 증가 합니다.  
  
-   **잠금** 커서는 결과 집합에서 행을 업데이트 하거나 삭제할 수 있는지 확인 하는 데 필요한 가장 낮은 수준의 잠금을 사용 합니다. 이는 일반적으로 반복 읽기 및 직렬화 가능 트랜잭션 격리 수준에서 매우 낮은 동시성 수준을 생성 합니다.  
  
-   **값을 사용 하 여 행 버전 및 낙관적 동시성을 사용 하는 낙관적 동시성** 커서는 낙관적 동시성을 사용 합니다. 마지막으로 읽은 이후 변경 되지 않은 경우에만 행을 업데이트 하거나 삭제 합니다. 변경 내용을 검색 하기 위해 행 버전이 나 값을 비교 합니다. 커서에서 행을 업데이트 하거나 삭제할 수는 없지만 잠금이 사용 되는 경우 보다 동시성은 훨씬 더 높습니다. 자세한 내용은 [낙관적 동시성](../../../odbc/reference/develop-app/optimistic-concurrency.md)섹션을 참조 하세요.  
  
 응용 프로그램은 커서가 SQL_ATTR_CONCURRENCY statement 특성과 함께 사용 하려는 동시성 유형을 지정 합니다. 지원 되는 형식을 확인 하기 위해 SQL_SCROLL_CONCURRENCY 옵션으로 **SQLGetInfo** 를 호출 합니다.
