---
title: "데이터를 삽입 하는 SQLSetPos 호출 | Microsoft Docs"
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
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], inserting data
- backward compatibility [ODBC], SqlSetPos
ms.assetid: 03e5c4d0-2bb3-4649-9781-89cab73f78eb
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4d7693d4072ec27264112b6cca0d79f413aa3b21
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="calling-sqlsetpos-to-insert-data"></a>데이터를 삽입 하는 SQLSetPos 호출
경우는 ODBC 2. *x* ODBC 3을 사용 하는 응용 프로그램*.x* 드라이버 호출 **SQLSetPos** 와 *작업* SQL_ADD, 드라이버 관리자의 인수 이 호출으로 매핑되지 않는 **SQLBulkOperations**합니다. ODBC 3 경우*.x* 드라이버를 호출 하는 응용 프로그램 작업 해야 **SQLSetPos** 드라이버와 SQL_ADD, 해당 작업을 지원 해야 합니다.  
  
 동작에서 한 가지 주요 차이점 때 **SQLSetPos** 사용 하 여 호출 SQL_ADD S6 상태에서 호출 될 때 발생 합니다. Odbc 2. *x*, 드라이버 반환 S1010 때 **SQLSetPos** S6 상태의 SQL_ADD로 호출 했습니다 (커서를 배치 된 후 **SQLFetch**). ODBC 3에서*.x*, **SQLBulkOperations** 와 *작업* SQL_ADD의 S6 상태에서 호출할 수 있습니다. 동작에 두 번째 주요 차이점은 **SQLBulkOperations** 와 *작업* SQL_ADD의 될 수 있습니다 상태 S5 호출 하는 동안 **SQLSetPos** 와  **작업** SQL_ADD의 수 없습니다. ODBC 3에서 동일한 호출에 대해 발생할 수 있는 문 전환에 대 한*.x*, 참조 [부록 b: ODBC 상태 전환 테이블](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)합니다.
