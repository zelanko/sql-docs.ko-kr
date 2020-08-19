---
description: 페치된 행 수 및 상태
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc328aab77d6e59db258c463a7dae1554f7d4c11
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429215"
---
# <a name="number-of-rows-fetched-and-status"></a>페치된 행 수 및 상태
SQL_ATTR_ROWS_FETCHED_PTR statement 특성이 설정 된 경우 **Sqlfetch** 또는 **sqlfetchscroll**에 대 한 호출에서 인출 된 행 수를 반환 하는 버퍼와 오류 행을 지정 합니다. 이 수는 SQL_ROW_NO_ROWS 상태가 없는 모든 행의 수입니다. **SQLBulkOperations** 또는 **SQLSetPos**를 호출한 후에는 함수에 의해 수행 된 대량 작업의 영향을 받은 행 수가 버퍼에 포함 됩니다. SQL_ATTR_ROW_STATUS_PTR statement 특성이 설정 된 경우 **Sqlfetch** 또는 **sqlfetchscroll** 은 반환 된 각 행의 상태를 제공 하는 *행 상태 배열을* 반환 합니다. 이러한 필드가 가리키는 버퍼는 모두 응용 프로그램에 의해 할당 되 고 드라이버에 의해 채워집니다. 응용 프로그램은 커서가 닫힐 때까지 이러한 포인터가 유효한 상태로 남아 있는지 확인 해야 합니다.  
  
 행 상태 배열 상태에서 항목은 각 행이 성공적으로 인출 되었는지, 업데이트, 추가 또는 삭제 되었는지, 마지막으로 인출 된 이후 삭제 되었는지 여부 및 행을 페치하는 동안 오류가 발생 했는지 여부를 나타냅니다. 다중 행 집합의 한 행을 검색 하는 동안 **Sqlfetch** 또는 **sqlfetchscroll** 에서 오류가 발생 하거나 대량 페치를 수행 하는 동안 SQL_FETCH_BY_BOOKMARK의 *작업* 인수를 사용 하는 **SQLBulkOperations** 에 오류가 발생 하는 경우 행 상태 배열의 해당 값을 SQL_ROW_ERROR로 설정 하 고, 행을 계속 가져오고 SQL_SUCCESS_WITH_INFO을 반환 합니다. 오류 처리 및 행 상태 배열에 대 한 자세한 내용은 [Sqlfetch](../../../odbc/reference/syntax/sqlfetch-function.md) 및 [sqlfetchscroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) 함수 설명을 참조 하세요.
