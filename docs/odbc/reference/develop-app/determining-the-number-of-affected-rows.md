---
title: "영향을 받는 행 수를 결정할 | Microsoft Docs"
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
- updating data [ODBC], number of rows affected
- number of rows affected by update [ODBC]
- data updates [ODBC], number of rows affected
ms.assetid: 1e56297d-a786-415e-b66d-b42d1b2a8d45
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 003268d449fd21ba23bbe8a905fafc972ee13914
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="determining-the-number-of-affected-rows"></a>영향을 받는 행 수를 결정합니다.
응용 프로그램 업데이트, 삭제 또는 행을 삽입, 후 호출할 수 **SQLRowCount** 행의 수가 영향을 받았는지 확인 합니다. **SQLRowCount** 여부 행 된 업데이트, 삭제 또는 삽입을 실행 하 여이 값을 반환 합니다.는 **업데이트**, **삭제**, 또는 **삽입** 위치 지정된 update 또는 delete 문을 실행 하 여 또는 호출 하 여 문에서 **SQLSetPos**합니다.  
  
 SQL 문의 일괄 처리를 실행 하는 경우 일괄 처리의 모든 문에 대 한 총 개수 또는 일괄 처리의 각 문에 대 한 개별 개수 영향을 받는 행의 수 수 있습니다. 자세한 내용은 참조 [SQL 문 일괄 처리](../../../odbc/reference/develop-app/batches-of-sql-statements.md) 및 [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)합니다.  
  
 문 핸들에 연결 된 진단 영역의 SQL_DIAG_ROW_COUNT 진단 헤더 필드에 영향을 받는 행 수가 반환도 됩니다. 그러나,이 필드의 데이터는 다시 설정 후 동일한 문 핸들에서 모든 함수 호출에서 반환 하는 반면 **SQLRowCount** 에 대 한 호출 될 때까지 동일 하 게 유지 **SQLBulkOperations**, **SQLExecute**, **SQLExecDirect**, **SQLPrepare**, 또는 **SQLSetPos**합니다.
