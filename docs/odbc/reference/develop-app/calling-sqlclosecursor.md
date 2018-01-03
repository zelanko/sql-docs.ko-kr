---
title: "SQLCloseCursor 호출 | Microsoft Docs"
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
- application upgrades [ODBC], SQLCloseCursor
- backward compatibility [ODBC], SqlCloseCursor
- SQLCloseCursor function [ODBC], calling
- upgrading applications [ODBC], SQLCloseCursor
- compatibility [ODBC], SQLCloseCursor
ms.assetid: ef448c39-a9ad-4f07-8ef3-65bd4cef672a
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3c3870a36138fd55a2e404d38e28db327990ba1b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="calling-sqlclosecursor"></a>SQLCloseCursor 호출
때문에 **SQLCloseCursor** 거의 동일 **SQLFreeStmt** SQL_CLOSE와 드라이버 관리자는이 함수 매핑되지 않습니다. 대체 함수는 기존 있도록 매핑됩니다 ODBC 2*.x* 응용 프로그램을 ODBC 3 쉽게 이동할 수 있습니다. *x* 새로운 함수를 사용 하 여 합니다. 이러한 이동 쉽게 새 ODBC 3을 사용 하려면 이러한 응용 프로그램에 대 한 있습니다. *x* 모듈식에서 조건부 코드 내부 기능입니다. **SQLCloseCursor** 는 새로운 기능을 나타내지 않습니다. 응용 프로그램으로 이동 하 여 이점이 얻지 않습니다 **SQLCloseCursor** 에서 **SQLFreeStmt** SQL_CLOSE 사용 합니다.
