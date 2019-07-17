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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083342"
---
# <a name="commit-and-rollback-behavior"></a>커밋 및 롤백 동작
Server Dbms 간에 커서를 닫고 문을 커밋하거나 롤백할 때 준비 된 문은 삭제 하는 일반적인 동작은 합니다. 데스크톱 데이터베이스를 준비 된 문은 커서를 열어 두고 가능성이 높아집니다. 자세한 내용은 SQL_CURSOR_COMMIT_BEHAVIOR 및 SQL_CURSOR_ROLLBACK_BEHAVIOR 옵션을 보려면 합니다 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명 및 [커서 및 준비 된 문에서효과의트랜잭션](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).
