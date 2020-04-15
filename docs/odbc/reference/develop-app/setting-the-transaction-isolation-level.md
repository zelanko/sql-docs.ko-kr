---
title: 트랜잭션 격리 수준 설정 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: 64a037f0-5065-4f45-9669-6710404a540c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 80401b276355a47469355cb6921d768d168398ae
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299813"
---
# <a name="setting-the-transaction-isolation-level"></a>트랜잭션 격리 수준 설정
트랜잭션 격리 수준을 설정하기 위해 응용 프로그램은 SQL_ATTR_TXN_ISOLATION 연결 특성을 사용합니다. 데이터 원본이 요청된 격리 수준을 지원하지 않는 경우 드라이버 또는 데이터 원본은 더 높은 수준을 설정할 수 있습니다. 데이터 원본이 지원하는 트랜잭션 격리 수준과 기본 격리 수준이 무엇인지 확인하기 위해 응용 프로그램은 각각 SQL_TXN_ISOLATION_OPTION 및 SQL_DEFAULT_TXN_ISOLATION 옵션을 사용하여 **SQLGetInfo를** 호출합니다.  
  
 트랜잭션 격리 수준이 높을수록 데이터베이스 데이터의 무결성을 가장 많이 보호할 수 있습니다. Serializable 트랜잭션은 다른 트랜잭션의 영향을 받지 않으므로 데이터베이스 무결성을 유지하도록 보장됩니다.  
  
 그러나 트랜잭션 격리 수준이 높을수록 응용 프로그램이 데이터에 대한 잠금이 해제될 때까지 기다려야 할 가능성이 높아지므로 성능이 저하될 수 있습니다. 응용 프로그램은 다음과 같은 경우 성능을 높이기 위해 낮은 수준의 격리를 지정할 수 있습니다.  
  
-   응용 프로그램의 트랜잭션을 방해할 수 있는 다른 트랜잭션이 없음을 보장할 수 있는 경우 이러한 상황은 한 회사의 한 사람이 한 컴퓨터에 직원 데이터를 포함하고 이러한 파일을 공유하지 않는 dBASE 파일을 유지 관리하는 경우와 같이 제한된 상황에서만 발생합니다.  
  
-   속도가 정확도보다 더 중요하고 오류가 작을 가능성이 있는 경우. 예를 들어 회사에서 소규모 판매를 많이 하고 큰 판매량이 드물다는 가정이 있습니다. 열려 있는 모든 판매의 총 가치를 추정하는 트랜잭션은 커밋되지 않은 격리 읽기 수준을 안전하게 사용할 수 있습니다. 트랜잭션에는 열리거나 닫혀 있고 이후에 롤백되는 주문이 포함되지만 일반적으로 서로 를 취소하고 이러한 주문이 발생할 때마다 차단되지 않으므로 트랜잭션이 훨씬 빠릅니다.  
  
 자세한 내용은 [낙관적 동시성](../../../odbc/reference/develop-app/optimistic-concurrency.md)을 참조하십시오.
