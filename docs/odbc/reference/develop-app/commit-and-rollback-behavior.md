---
title: 커밋 및 롤백 동작 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c67c29b295160a2908152b22c7a349ce4c0f9f50
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299133"
---
# <a name="commit-and-rollback-behavior"></a>커밋 및 롤백 동작
서버 DBMS 간의 일반적인 동작은 명령문이 커밋되거나 롤백될 때 커서를 닫고 준비된 문을 삭제하는 것입니다. 데스크톱 데이터베이스는 커서를 열어 두고 준비된 문을 유지할 가능성이 높습니다. 자세한 내용은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명 및 [커서 및 준비된 명령문에 대한 트랜잭션의 효과에서](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)SQL_CURSOR_COMMIT_BEHAVIOR 및 SQL_CURSOR_ROLLBACK_BEHAVIOR 옵션을 참조하십시오.
