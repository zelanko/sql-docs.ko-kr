---
title: 인출 된 행 수 및 상태 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab4830ddd56335959dd7049a1dabdcc3a0354213
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47808771"
---
# <a name="number-of-rows-fetched-and-status"></a>페치된 행 수 및 상태
호출에 의해 인출 된 행 수를 반환 하는 버퍼 지정 SQL_ATTR_ROWS_FETCHED_PTR 문 특성에 설정한 경우 **SQLFetch** 하거나 **SQLFetchScroll**, 및 오류 행. (이 숫자는 SQL_ROW_NO_ROWS 상태에 있지 않은 모든 행의 수입니다.) 호출한 후 **SQLBulkOperations** 또는 **SQLSetPos**, 버퍼 함수에서 수행 하는 대량 작업에 의해 영향을 받는 행 수를 포함 합니다. SQL_ATTR_ROW_STATUS_PTR 문 특성에 설정한 경우 **SQLFetch** 또는 **SQLFetchScroll** 반환 된 *행 상태 배열* 각 상태를 제공 하는 반환 된 행입니다. 이러한 필드에서 가리키는 버퍼의 두 응용 프로그램에 의해 할당 되 고 드라이버에서 채워집니다. 응용 프로그램은 커서를 닫을 때까지 이러한 포인터 유효 하 고 있는지 확인 해야 합니다.  
  
 행 상태 배열 상태의 항목 업데이트 된 여부를 각 행 성공적으로 가져온 지 여부를 추가 또는 마지막 페치된 이후로 및 행을 인출 하는 동안 오류가 발생 했는지 여부를 삭제 합니다. 하는 경우 **SQLFetch** 하거나 **SQLFetchScroll** 다중 행 집합의 한 행을 검색 하는 동안 오류가 발생 이거나 **SQLBulkOperations** 사용 하 여는 *작업*  대량 페치를 수행 하는 동안 오류가 발생 하는 인수의 SQL_FETCH_BY_BOOKMARK SQL_ROW_ERROR 행 상태 배열에서 해당 값을 설정, 행을 인출 합니다. 계속 하 고 SQL_SUCCESS_WITH_INFO를 반환 합니다. 오류 처리 및 행 상태 배열에 대 한 자세한 내용은 참조 하세요. 합니다 [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md) 하 고 [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) 함수 설명 합니다.
