---
title: "커밋 및 롤백 동작 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 2ac8f012-e46d-41ca-81bb-e4a3246e3241
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8e2bf47aa43ad68871a1c69a7f8b97ca608f8175
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="commit-and-rollback-behavior"></a>커밋 및 롤백 동작
커서를 닫고 문이 커밋되거나 롤백될 때 준비 된 문을 취소 하 서버 Dbms 간에 일반적인 동작이입니다. 데스크톱 데이터베이스는 준비 된 문을 커서를 열어 두고 가능성이 높습니다. 자세한 내용은의 SQL_CURSOR_COMMIT_BEHAVIOR 및 SQL_CURSOR_ROLLBACK_BEHAVIOR 옵션을 참조 하십시오.는 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명 및 [커서 및 준비 된 문에서효과의트랜잭션](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).
