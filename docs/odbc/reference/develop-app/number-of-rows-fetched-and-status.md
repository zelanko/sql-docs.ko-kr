---
title: 가져온 행 수 및 상태 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- row status array [ODBC]
- number of rows fetched [ODBC]
- result sets [ODBC], row status array
ms.assetid: a069b979-5108-4905-932f-8ae8e7905ff2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 20e1632e8da765b0da2785bd846b67d13ebe01ed
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302364"
---
# <a name="number-of-rows-fetched-and-status"></a>페치된 행 수 및 상태
SQL_ATTR_ROWS_FETCHED_PTR 문 특성이 설정된 경우 **SQLFetch** 또는 **SQLFetchScroll**및 오류 행에 대한 호출에서 가져온 행 수를 반환하는 버퍼를 지정합니다. 이 숫자는 상태 SQL_ROW_NO_ROWS 없는 모든 행의 개수입니다. **SQLBulkOperations** 또는 **SQLSetPos를**호출한 후 버퍼에는 함수에서 수행하는 대량 작업의 영향을 받은 행 수가 포함됩니다. SQL_ATTR_ROW_STATUS_PTR 문 특성이 설정된 경우 **SQLFetch** 또는 **SQLFetchScroll는** 반환된 각 행의 상태를 제공하는 *행 상태 배열을* 반환합니다. 이 필드가 가리키는 두 버퍼는 응용 프로그램에서 할당되고 드라이버에 의해 채워집니다. 응용 프로그램은 커서가 닫혀야 이러한 포인터가 유효한지 확인해야 합니다.  
  
 행 상태 배열의 항목은 각 행을 성공적으로 가져왔는지 여부, 마지막으로 가져온 이후 업데이트, 추가 또는 삭제되었는지 여부, 행을 가져오는 동안 오류가 발생했는지 여부를 지정합니다. **SQLFetch** 또는 **SQLFetchScroll** 다중 행 행 집합의 한 행을 검색 하는 동안 오류가 발생 하는 경우 또는 SQL_FETCH_BY_BOOKMARK *작업* **인수와 SQLBulkOperations** 대량 가져오기를 수행 하는 동안 오류가 발생 하는 경우 SQL_ROW_ERROR 행 상태 배열에 해당 값을 설정 하 고 행을 계속 하 고 SQL_SUCCESS_WITH_INFO 반환 합니다. 오류 처리 및 행 상태 배열에 대한 자세한 내용은 [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md) 및 [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) 함수 설명을 참조하십시오.
