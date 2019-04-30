---
title: 영향을 받는 행 수를 결정 합니다. | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 99e3676c3b73b177f5e6fc3acef0d93d55cce898
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63262098"
---
# <a name="determining-the-number-of-affected-rows"></a>영향을 받는 행 수 확인
응용 프로그램 업데이트, 삭제 또는 행을 삽입, 후 호출할 수 있습니다 **SQLRowCount** 영향을 받은 행 수를 확인 하려면. **SQLRowCount** 표시할지, 아니면 행 업데이트, 삭제 되거나, 실행 하 여 삽입 된이 값을 반환 합니다.는 **업데이트**를 **삭제**, 또는 **삽입** 문 배치를 실행 하 여 업데이트 또는 delete 문의 하거나 호출 하 여 **SQLSetPos**합니다.  
  
 SQL 문의 일괄 처리를 실행 하는 경우 영향을 받는 행 수가 일괄 처리의 모든 문에 대 한 총 또는 일괄 처리의 각 문에 대해 개별 수 수 있습니다. 자세한 내용은 [SQL 문 일괄 처리](../../../odbc/reference/develop-app/batches-of-sql-statements.md) 하 고 [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)합니다.  
  
 문 핸들을 사용 하 여 연결 된 진단 영역의 SQL_DIAG_ROW_COUNT 진단 헤더 필드에 영향을 받는 행 수가 반환 됩니다. 그러나이 필드의에서 데이터를 다시 설정 됩니다 후 동일한 문 핸들에 대해 모든 함수 호출에서 반환 하는 반면 **SQLRowCount** 호출 될 때까지 동일 하 게 유지 **SQLBulkOperations**합니다 **SQLExecute**, **SQLExecDirect**하십시오 **SQLPrepare**, 또는 **SQLSetPos**합니다.
