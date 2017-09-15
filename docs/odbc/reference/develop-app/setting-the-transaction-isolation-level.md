---
title: "트랜잭션 격리 수준 설정 | Microsoft Docs"
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
- isolation levels [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: 64a037f0-5065-4f45-9669-6710404a540c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d91c7789fbcd0c4dc197f2da13b23c1da34666bb
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setting-the-transaction-isolation-level"></a>트랜잭션 격리 수준 설정
트랜잭션 격리 수준의 설정 하려면 응용 프로그램에서 SQL_ATTR_TXN_ISOLATION 연결 특성을 사용 합니다. 데이터 원본에 요청 된 격리 수준 지원 하지 않으면, 드라이버 또는 데이터 원본을 더 높은 수준을 설정할 수 있습니다. 어떤 트랜잭션 격리 수준으로 데이터 소스를 확인 하려면 지원 하 고 응용 프로그램이 호출 기본 격리 수준이 이면 **SQLGetInfo** SQL_TXN_ISOLATION_OPTION 및 SQL_DEFAULT_TXN_ISOLATION 옵션 각각.  
  
 더 높은 수준의 트랜잭션 격리는 데이터베이스 데이터의 무결성에 가장 강력한 보호를 제공합니다. 직렬화 가능 트랜잭션은 다른 트랜잭션에 의해 영향을 받지 않을 이며 데이터베이스 무결성을 유지 관리를 보장 합니다.  
  
 그러나 더 높은 수준의 트랜잭션 격리는 응용 프로그램 출시 될 데이터에 대해 잠금을 대기 해야 할 가능성을 증가 하기 때문에 성능이 저하를 발생할 수 있습니다. 응용 프로그램에 다음과 같은 경우에는 성능을 향상 시키기 위해 격리의 더 낮은 수준의 지정할 수 있습니다.:  
  
-   때 그 보장할 수 있는 다른 트랜잭션이 존재 하는지는 응용 프로그램의 트랜잭션을과 충돌할 수 있습니다. 이 경우 비어 있는 명 유지 한 컴퓨터에서 개인 데이터를 포함 하는 dBASE 파일을 관리 하는 경우 등의 제한 된 경우에만 발생 하 고 이러한 파일을 공유 하지 않습니다.  
  
-   속도가 정확도 및 오류 보다 작은 일 수 있습니다. 예를 들어 회사는 많은 소규모 영업 및 큰 sales 드문 경우를 가정 합니다. 열려 있는 모든 판매액의 합계 값을 예측 하는 트랜잭션이 Read Uncommitted 격리 수준 안전 하 게 사용 될 수 있습니다. 트랜잭션이 열리거나 닫힐 있으며 이후에 주문을 포함 하지만,이 일반적으로 서로 위배 롤백되고 한다는 이러한 주문 발견 될 때마다 차단 되지 않은 트랜잭션이 훨씬 속도가 더 빠를 수는.  
  
 자세한 내용은 참조 [낙관적 동시성](../../../odbc/reference/develop-app/optimistic-concurrency.md)합니다.
