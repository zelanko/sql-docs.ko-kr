---
title: 커밋 및 롤백 동작 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 2ac8f012-e46d-41ca-81bb-e4a3246e3241
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 643d7d4174df66abfcee274c1f987e8f405d19b9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083342"
---
# <a name="commit-and-rollback-behavior"></a>커밋 및 롤백 동작
서버 Dbms 간의 일반적인 동작은 문이 커밋되거나 롤백될 때 커서를 닫고 준비 된 문을 삭제 하는 것입니다. 데스크톱 데이터베이스는 커서를 열린 상태로 유지 하 고 준비 된 문을 유지할 가능성이 높습니다. 자세한 내용은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명의 SQL_CURSOR_COMMIT_BEHAVIOR 및 SQL_CURSOR_ROLLBACK_BEHAVIOR 옵션 및 [커서와 준비 된 문의 트랜잭션 효과](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)를 참조 하세요.
