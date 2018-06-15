---
title: 인출 된 행 수 및 상태 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- row status array [ODBC]
- number of rows fetched [ODBC]
- result sets [ODBC], row status array
ms.assetid: a069b979-5108-4905-932f-8ae8e7905ff2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 16bc3a279e2d4565529dd175c16bce01f9431403
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32914008"
---
# <a name="number-of-rows-fetched-and-status"></a>인출 된 행 수 및 상태
에 대 한 호출에 의해 인출 된 행 수를 반환 하는 버퍼를 지정 SQL_ATTR_ROWS_FETCHED_PTR 문 특성 설정 된 경우 **SQLFetch** 또는 **SQLFetchScroll**, 및 오류 행. (이 숫자는 SQL_ROW_NO_ROWS 상태를 갖지 않는 모든 행의 수입니다.) 호출한 후 **SQLBulkOperations** 또는 **SQLSetPos**, 버퍼는 함수에 의해 수행 대량 작업에 의해 영향을 받는 행 수를 포함 합니다. SQL_ATTR_ROW_STATUS_PTR을 문 특성 설정 된 경우 **SQLFetch** 또는 **SQLFetchScroll** 반환 된 *행 상태 배열이* 각 상태를 제공 하는 반환 된 행입니다. 이러한 필드가 가리키는 버퍼의 둘 다 응용 프로그램에 의해 할당 되 고 드라이버에 의해 채워집니다. 응용 프로그램은 이러한 포인터는 커서를 닫을 때까지 유효한 상태로 있는지 확인 해야 합니다.  
  
 행 상태 배열이 상태에서 항목 추가 각 행이 인출 된 성공적으로 업데이트 된 있는지 여부 또는 마지막 인출할 이후 및 행을 인출 하는 동안 오류가 발생 했는지 여부를 삭제 합니다. 경우 **SQLFetch** 또는 **SQLFetchScroll** 다중 행을 행 집합의 한 행을 검색 하는 동안 오류가 발생 하거나 **SQLBulkOperations** 와 *작업*  SQL_FETCH_BY_BOOKMARK의 인수에서 대량 가져오기 수행 하는 동안 오류가 발생, SQL_ROW_ERROR 행 상태 배열이의 해당 값을 설정, 행을 인출 합니다. 계속 하 고 SQL_SUCCESS_WITH_INFO를 반환 합니다. 오류 처리 및 행 상태 배열이 하는 방법에 대 한 자세한 내용은 참조는 [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md) 및 [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) 설명 작동 합니다.
