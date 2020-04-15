---
title: 행 상태 배열 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 60dead23fe0051c05698e094f37ddad96b2b337d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304294"
---
# <a name="row-status-array"></a>행 상태 배열
데이터 외에도 **SQLFetch** 및 **SQLFetchScroll는** 행 집합의 각 행 의 상태를 제공하는 배열을 반환할 수 있습니다. 이 배열은 SQL_ATTR_ROW_STATUS_PTR 문 특성을 통해 지정됩니다. 이 배열은 응용 프로그램에서 할당되며 SQL_ATTR_ROW_ARRAY_SIZE 문 특성에 의해 지정된 만큼의 요소가 있어야 합니다. 배열의 값은 **SQLBulkOperations,** **SQLFetch,** **SQLFetchScroll**및 **SQLSetPos에** 의해 설정됩니다. 이 값은 행의 상태와 해당 상태가 마지막으로 가져온 이후 변경되었는지 여부를 설명합니다.  
  
|행 상태 배열 값|설명|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|행이 성공적으로 인출되었으며 마지막으로 가져온 이후 변경되지 않았습니다.|  
|SQL_ROW_SUCCESS_WITH_INFO|행이 성공적으로 인출되었으며 마지막으로 가져온 이후 변경되지 않았습니다. 그러나 행에 대한 경고가 반환되었습니다.|  
|SQL_ROW_ERROR|행을 가져오는 동안 오류가 발생했습니다.|  
|SQL_ROW_UPDATED|행이 성공적으로 인출되었으며 마지막으로 가져온 이후 업데이트되었습니다. 행을 다시 가져오거나 **SQLSetPos에서**새로 고치는 경우 해당 상태가 새 상태로 변경됩니다.<br /><br /> 일부 드라이버는 데이터 변경 내용을 검색할 수 없으므로 이 값을 반환할 수 없습니다. 드라이버가 다시 가져온 행에 대한 업데이트를 검색할 수 있는지 여부를 확인하기 위해 응용 프로그램은 SQL_ROW_UPDATES 옵션을 사용하여 **SQLGetInfo를** 호출합니다.|  
|SQL_ROW_DELETED|행이 마지막으로 가져온 이후 삭제되었습니다.|  
|SQL_ROW_ADDED|행은 **SQLBulkOperations**. 행을 다시 가져오거나 **SQLSetPos에**의해 새로 고치는 경우 해당 상태가 SQL_ROW_SUCCESS.<br /><br /> 이 값은 **SQLFetch** 또는 **SQLFetchScroll**에 의해 설정되지 않습니다.|  
|SQL_ROW_NOROW|행 집합은 결과 집합의 끝을 겹치고 행 상태 배열의 이 요소에 해당하는 행이 반환되지 않았습니다.|
