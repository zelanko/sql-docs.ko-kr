---
title: 영향을 받는 행 수 결정 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], number of rows affected
- number of rows affected by update [ODBC]
- data updates [ODBC], number of rows affected
ms.assetid: 1e56297d-a786-415e-b66d-b42d1b2a8d45
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 156a5fe41d2c9b57a33bbc2bdb4540d1f5b00340
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305894"
---
# <a name="determining-the-number-of-affected-rows"></a>영향을 받는 행 수 확인
응용 프로그램이 행을 업데이트, 삭제 또는 삽입한 후 **SQLRowCount를** 호출하여 영향을 받은 행 수를 확인할 수 있습니다. **SQLRowCount** 는 **업데이트,** **DELETE**또는 **INSERT** 문을 실행하거나 위치 가있는 업데이트 또는 삭제 문을 실행하거나 **SQLSetPos**를 호출하여 행이 업데이트, 삭제 또는 삽입되었는지 여부에 관계없이 이 값을 반환합니다.  
  
 SQL 문 일괄 처리가 실행되는 경우 영향을 받는 행의 수는 일괄 처리의 모든 문에 대한 총 개수이거나 일괄 처리의 각 문에 대한 개별 개수일 수 있습니다. 자세한 내용은 SQL 문 및 [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)의 [일괄 처리를](../../../odbc/reference/develop-app/batches-of-sql-statements.md) 참조하십시오.  
  
 영향을 받는 행의 수는 문 핸들과 연결된 진단 영역에서 SQL_DIAG_ROW_COUNT 진단 헤더 필드에도 반환됩니다. 그러나 이 필드의 데이터는 동일한 문 핸들에서 모든 함수가 호출된 후 재설정되지만 **SQLRowCount에서** 반환되는 값은 **SQLBulkOperations**, **SQLExecDirect**, **SQLSetDirect**, **SQLSetPos 또는 SQLSetPos**에 대한 호출까지 동일하게 유지됩니다. **SQLExecute**
