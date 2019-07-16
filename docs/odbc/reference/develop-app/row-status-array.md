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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020373"
---
# <a name="row-status-array"></a>행 상태 배열
데이터 뿐만 아니라 **SQLFetch** 하 고 **SQLFetchScroll** 행 집합의 각 행의 상태를 제공 하는 배열을 반환할 수 있습니다. 이 배열은 SQL_ATTR_ROW_STATUS_PTR 문 특성을 통해 지정 됩니다. 이 배열 응용 프로그램에 의해 할당 되 고 SQL_ATTR_ROW_ARRAY_SIZE 문 특성에 의해 지정 된 만큼의 요소가 있어야 합니다. 배열의 값 설정 됩니다 **SQLBulkOperations**를 **SQLFetch**합니다 **SQLFetchScroll**, 및 **SQLSetPos 합니다.** 값의 행과 마지막 페치된 이후로 해당 상태가 변경 되었는지 여부 상태를 설명 합니다.  
  
|행 상태 배열 값입니다.|설명|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|행을 성공적으로 가져온 및 마지막 페치된 후 변경 되지 않은 합니다.|  
|SQL_ROW_SUCCESS_WITH_INFO|행을 성공적으로 가져온 및 마지막 페치된 후 변경 되지 않은 합니다. 그러나 행에 대 한 경고가 반환 되었습니다.|  
|SQL_ROW_ERROR|행을 인출 하는 동안 오류가 발생 했습니다.|  
|SQL_ROW_UPDATED|행을 성공적으로 가져온 및 마지막으로 가져온 후에 업데이트 되었습니다. 행이 다시 인출 되거나으로 새로 고침 하는 경우 **SQLSetPos**, 새로운 상태에 해당 상태가 변경 됩니다.<br /><br /> 일부 드라이버는 데이터의 변경 내용을 검색할 수 없습니다 및이 값을 반환할 수 없습니다. 응용 프로그램이 호출 드라이버에 따라 다시 인출 된 행에 업데이트를 검색할 수 있는지 여부를 결정할 **SQLGetInfo** SQL_ROW_UPDATES 옵션을 사용 합니다.|  
|SQL_ROW_DELETED|마지막으로 페치된 이후로 행 삭제 되었습니다.|  
|SQL_ROW_ADDED|행으로 삽입 된 **SQLBulkOperations**합니다. 행이 다시 인출 됩니다 아니면으로 새로 고쳐집니다 **SQLSetPos**, 상태가 SQL_ROW_SUCCESS입니다.<br /><br /> 이 값이 설정 되지 않습니다 **SQLFetch** 하거나 **SQLFetchScroll**합니다.|  
|SQL_ROW_NOROW|행 집합 결과 집합의 끝을 중첩 하 고 행이 행 상태 배열이 요소에 해당 하는 반환 된 키를 누릅니다.|
