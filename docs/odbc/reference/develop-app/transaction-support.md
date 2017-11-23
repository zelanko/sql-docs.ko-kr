---
title: "트랜잭션 지원 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: transactions [ODBC], degree of support
ms.assetid: d56e1458-8da2-4d73-a777-09e045c30a33
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ac759747a088f98f1426afedf8623169d91b113f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="transaction-support"></a>트랜잭션 지원
트랜잭션에 대 한 지원 수준을 드라이버 정의입니다. ODBC가 해당 데이터에 대 한 여러 업데이트를 관리할 필요가 없는 단일 사용자 또는 데스크톱 데이터베이스에서 구현 하도록 설계 되었습니다. 트랜잭션을 지 원하는 일부 데이터베이스의 경우에 SQL;의 데이터 조작 언어 (DML) 문을 수행 하는 또한 제한이 나 특별 한 트랜잭션 의미 체계 데이터 정의 언어 (DDL)를 사용 하면 됩니다 트랜잭션이 활성 상태입니다. 즉, 수 및 트랜잭션 중 테이블의 정의 변경 하지 않습니다 테이블에 여러 동시 업데이트에 대 한 트랜잭션 지원이 있을 수 있습니다.  
  
 응용 프로그램 트랜잭션이 지원 되는지 여부를 DDL 트랜잭션과 DDL 호출 하 여 거래에 포함 하는 모든 특수 효과에 포함 될 수 있는지 여부를 확인 **SQLGetInfo** SQL_TXN_CAPABLE 옵션을 사용 합니다. 자세한 내용은 참조는 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명 합니다.  
  
 드라이버는 트랜잭션을 지원 하지 않습니다. 응용 프로그램 데이터의 잠금을 해제 (ODBC 이외의 API 사용) 하는 기능에 되지만 응용 프로그램 잠금 및 잠금 해제 레코드 및 필요에 따라 테이블에서 트랜잭션 지원을 얻을 수 있지만 계정 전송 예제를 구현 하려면 응용 프로그램은 두 계정 모두에 대 한 레코드를 잠글, 현재 값을 복사, 첫 번째 계좌에서 금액, 두 번째 계정을 신용 및 레코드의 잠금을 해제 합니다. 모든 단계에 실패 한 경우 응용 프로그램 복사본을 사용 하 여 계정을 약 수 있습니다.  
  
 데이터 원본 트랜잭션을 지 원하는 특정 환경 내에서 한 번에 둘 이상의 트랜잭션을 지원할 수 수 있습니다. 응용 프로그램 호출 **SQLGetInfo** SQL_MULTIPLE_ACTIVE_TXN 것인지 데이터 소스를 동일한 환경에서 둘 이상의 연결에서 동시 활성 트랜잭션을 지원 하는지 확인 합니다. 연결당 하나의 트랜잭션만 이기 때문에이 동일한 데이터 원본에 대 한 여러 연결이 있는 응용 프로그램에 관심 있는.
