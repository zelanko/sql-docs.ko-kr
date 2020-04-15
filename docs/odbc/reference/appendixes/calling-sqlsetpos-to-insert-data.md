---
title: 데이터를 삽입하기 위해 SQLSetPos 호출 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cb374b2506d55b400207c8f60bdf42bb6bb4065e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306604"
---
# <a name="calling-sqlsetpos-to-insert-data"></a>SQLSetPos를 호출하여 데이터 삽입
ODBC *3.x* 드라이버로 작업하는 ODBC *2.x* 응용 프로그램이 SQL_ADD *작업* 인수로 **SQLSetPos를** 호출하는 경우 드라이버 관리자는 이 호출을 **SQLBulkOperations**에 매핑하지 않습니다. ODBC *3.x* 드라이버가 **SQLSetPos를** SQL_ADD 호출하는 응용 프로그램과 함께 작동해야 하는 경우 드라이버는 해당 작업을 지원해야 합니다.  
  
 **SQLSetPos가** 상태 S6에서 호출 될 때 발생 SQL_ADD 호출 할 때 동작의 한 가지 주요 차이점은 발생합니다. ODBC *2.x에서*드라이버는 **SQLSetPos가** 상태 S6에서 SQL_ADD 호출되었을 때 S1010을 반환했습니다 (커서가 **SQLFetch로**배치 된 후). ODBC *3.x에서*SQL_ADD *작업이* 있는 **SQLBulkOperations는** 상태 S6에서 호출할 수 있습니다. 동작의 두 번째 주요 차이점은 SQL_ADD *작업이* 있는 **SQLBulkOperations를** 상태 S5에서 호출할 수 있지만 SQL_ADD **작업이** 있는 **SQLSetPos는** 수행할 수 없다는 것입니다. ODBC *3.x에서*동일한 호출에 대해 발생할 수 있는 명령문 전환의 경우 [부록 B: ODBC 상태 전환 테이블을](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)참조하십시오.
