---
description: 트랜잭션 ODBC
title: 트랜잭션 ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], about transactions
- transactions [ODBC]
ms.assetid: b4ca861a-c164-4e87-8672-d5de15e3823c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c40c51fa2b0154d90d5ea08952266997d175e3e3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456427"
---
# <a name="transactions-odbc"></a>트랜잭션 ODBC
*트랜잭션은* 단일 원자성 작업으로 수행 되는 작업 단위입니다. 즉, 작업이 성공 하거나 전체적으로 실패 합니다. 예를 들어 한 은행 계좌에서 다른 은행 계좌로 돈을 전송 하는 것이 좋습니다. 여기에는 첫 번째 계정에서 money를 입출금 계좌 두 번째 단계가 포함 됩니다. 두 단계가 모두 성공 해야 합니다. 한 단계가 성공 하거나 실패 하는 것은 허용 되지 않습니다. 트랜잭션을 지 원하는 데이터베이스는이를 보장할 수 있습니다.  
  
 트랜잭션을 *커밋하거나* 롤백하는 방법으로 완료할 수 *있습니다.* 트랜잭션이 커밋되면 해당 트랜잭션에서 변경한 내용이 영구적으로 적용 됩니다. 트랜잭션이 롤백될 때 영향을 받는 행은 트랜잭션이 시작 되기 전의 상태로 반환 됩니다. 계정 전송 예를 확장 하기 위해 응용 프로그램은 첫 번째 계정을 지불 하기 위해 하나의 SQL 문을 실행 하 고 두 번째 계정에 크레딧을 다른 SQL 문을 실행 합니다. 두 문이 모두 성공 하면 응용 프로그램은 트랜잭션을 커밋합니다. 그러나 어떤 이유로 든 두 문이 모두 실패 하면 응용 프로그램은 트랜잭션을 롤백합니다. 두 경우 모두 응용 프로그램은 트랜잭션이 끝날 때 일관 된 상태를 보장 합니다.  
  
 단일 트랜잭션은 서로 다른 시간에 발생 하는 여러 데이터베이스 작업을 포함할 수 있습니다. 다른 트랜잭션에 중간 결과에 대 한 완전 한 액세스 권한이 있는 경우 트랜잭션이 서로 방해할 수 있습니다. 예를 들어 한 트랜잭션이 행을 삽입 하 고, 두 번째 트랜잭션이 해당 행을 읽고, 첫 번째 트랜잭션이 롤백됩니다. 이제 두 번째 트랜잭션에는 존재 하지 않는 행의 데이터가 있습니다.  
  
 이 문제를 해결 하기 위해 여러 가지 방법으로 트랜잭션을 격리할 수 있습니다. *트랜잭션 격리* 는 일반적으로 두 개 이상의 트랜잭션이 동시에 동일한 행을 사용 하지 못하도록 하 여 행을 잠그기 때문에 구현 됩니다. 일부 데이터베이스에서는 행을 잠그면 다른 행도 잠길 수 있습니다.  
  
 트랜잭션 격리를 늘리면 *동시성이* 감소 하거나 두 트랜잭션에서 동일한 데이터를 동시에 사용할 수 있습니다. 자세한 내용은 [트랜잭션 격리 수준 설정](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md)을 참조 하세요.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ODBC의 트랜잭션](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [트랜잭션 격리](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [동시성 제어](../../../odbc/reference/develop-app/concurrency-control.md)
