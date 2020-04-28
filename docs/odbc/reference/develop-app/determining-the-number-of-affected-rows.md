---
title: 영향을 받는 행 수 결정 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305894"
---
# <a name="determining-the-number-of-affected-rows"></a>영향을 받는 행 수 확인
응용 프로그램에서 행을 업데이트, 삭제 또는 삽입 한 후 **Sqlrowcount** 를 호출 하 여 영향을 받는 행 수를 확인할 수 있습니다. **Sqlrowcount** 는 **update**, **delete**또는 **INSERT** 문을 실행 하 고, 위치 지정 UPDATE 또는 delete 문을 실행 하거나, **SQLSetPos**를 호출 하 여 행을 업데이트, 삭제 또는 삽입 하는 방법으로이 값을 반환 합니다.  
  
 SQL 문 일괄 처리를 실행 하는 경우 영향을 받는 행 수가 일괄 처리의 모든 문에 대 한 총 개수 이거나 일괄 처리의 각 문에 대 한 개별 개수가 될 수 있습니다. 자세한 내용은 [SQL 문 일괄 처리](../../../odbc/reference/develop-app/batches-of-sql-statements.md) 및 [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)를 참조 하세요.  
  
 영향을 받는 행의 수는 문 핸들과 연결 된 진단 영역의 SQL_DIAG_ROW_COUNT 진단 헤더 필드에도 반환 됩니다. 그러나이 필드의 데이터는 동일한 문 핸들의 모든 함수 호출 후 다시 설정 되지만 **Sqlrowcount** 에서 반환 되는 값은 **SQLBulkOperations**, **sqlrowcount**, **Sqlexecdirect**, **sqlrowcount**또는 **SQLSetPos**를 호출할 때까지 동일 하 게 유지 됩니다.
