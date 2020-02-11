---
title: 행 상태 배열 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- row status array [ODBC]
- cursors [ODBC], block
- result sets [ODBC], row status array
- block cursors [ODBC]
- result sets [ODBC], block cursors
- rowset status [ODBC]
ms.assetid: 4b69f189-2722-4314-8a02-f4ffecd6dabd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 57b187bf4f14bd5c05f91a433fa331e954fa0fb9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020373"
---
# <a name="row-status-array"></a>행 상태 배열
**Sqlfetch** 및 **sqlfetchscroll** 은 데이터 외에도 행 집합의 각 행에 대 한 상태를 제공 하는 배열을 반환할 수 있습니다. 이 배열은 SQL_ATTR_ROW_STATUS_PTR statement 특성을 통해 지정 됩니다. 이 배열은 응용 프로그램에 의해 할당 되며 SQL_ATTR_ROW_ARRAY_SIZE statement 특성에 지정 된 것과 같은 수의 요소를 포함 해야 합니다. 배열의 값은 **SQLBulkOperations**, **sqlfetch**, **sqlfetchscroll**및 SQLSetPos로 설정 됩니다 **.** 값은 행의 상태를 설명 하 고 마지막으로 인출 된 후 해당 상태가 변경 되었는지 여부를 설명 합니다.  
  
|행 상태 배열 값|Description|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|행이 인출 되었으며 마지막으로 인출 된 이후 변경 되지 않았습니다.|  
|SQL_ROW_SUCCESS_WITH_INFO|행이 인출 되었으며 마지막으로 인출 된 이후 변경 되지 않았습니다. 그러나 행에 대 한 경고가 반환 되었습니다.|  
|SQL_ROW_ERROR|행을 인출 하는 동안 오류가 발생 했습니다.|  
|SQL_ROW_UPDATED|행이 인출 되 고 마지막으로 인출 된 후 업데이트 되었습니다. 행을 다시 페치 하거나 **SQLSetPos**로 새로 고치면 상태가 새 상태로 변경 됩니다.<br /><br /> 일부 드라이버는 데이터에 대 한 변경 내용을 검색할 수 없으므로이 값을 반환할 수 없습니다. 드라이버가 refetched 형 행의 업데이트를 검색할 수 있는지 여부를 확인 하기 위해 응용 프로그램은 SQL_ROW_UPDATES 옵션으로 **SQLGetInfo** 를 호출 합니다.|  
|SQL_ROW_DELETED|행이 마지막으로 인출 된 후 삭제 되었습니다.|  
|SQL_ROW_ADDED|**SQLBulkOperations**에 의해 행이 삽입 되었습니다. 행을 다시 페치 하거나 **SQLSetPos**로 새로 고치면 상태가 SQL_ROW_SUCCESS 상태가 됩니다.<br /><br /> 이 값은 **Sqlfetch** 또는 **sqlfetchscroll**에 의해 설정 되지 않습니다.|  
|SQL_ROW_NOROW|행 집합은 결과 집합의 끝 부분을 속하는지를 행 상태 배열의이 요소에 해당 하는 행이 반환 되지 않았습니다.|
