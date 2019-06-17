---
title: 데이터를 삽입 하는 SQLSetPos 호출 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], inserting data
- backward compatibility [ODBC], SqlSetPos
ms.assetid: 03e5c4d0-2bb3-4649-9781-89cab73f78eb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c7424206318436532cad62690b01427f079a589
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63159270"
---
# <a name="calling-sqlsetpos-to-insert-data"></a>SQLSetPos를 호출하여 데이터 삽입
경우는 ODBC 2. *x* 는 ODBC 3을 사용 하는 응용 프로그램 *.x* 드라이버 호출 **SQLSetPos** 사용 하 여는 *작업* SQL_ADD, 드라이버 관리자의 인수 이 호출으로 매핑되지 **SQLBulkOperations**합니다. 경우는 ODBC 3 *.x* 드라이버를 호출 하는 응용 프로그램과 함께 작동 해야 **SQLSetPos** 드라이버 SQL_ADD를 사용 하 여 해당 작업을 지원 해야 합니다.  
  
 동작에서 한 가지 주요 차이점 때 **SQLSetPos** 와 라고 SQL_ADD S6 상태에서 호출 될 때 발생 합니다. Odbc 2. *x*, S1010를 반환 하면 **SQLSetPos** S6 상태의 SQL_ADD로 호출 되었습니다 (커서를 사용 하 여 배치 된 후 **SQLFetch**). ODBC 3에서 *.x*하십시오 **SQLBulkOperations** 사용 하 여는 *작업* SQL_ADD의 S6 상태의 호출할 수 있습니다. 동작의 두 번째 주요 차이점 **SQLBulkOperations** 사용 하 여는 *작업* SQL_ADD의 S5 상태의 호출 하는 동안 **SQLSetPos** 사용 하 여는  **작업** SQL_ADD의 수 없습니다. ODBC 3에서 동일한 호출에 대 한 발생할 수 있는 문 전환 *.x*를 참조 하세요 [부록 b: ODBC 상태 전환 테이블](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)합니다.
