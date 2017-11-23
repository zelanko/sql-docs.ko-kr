---
title: "행 상태 배열을 | Microsoft Docs"
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
- row status array [ODBC]
- cursors [ODBC], block
- result sets [ODBC], row status array
- block cursors [ODBC]
- result sets [ODBC], block cursors
- rowset status [ODBC]
ms.assetid: 4b69f189-2722-4314-8a02-f4ffecd6dabd
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f4451ccb74ca19a02c352c2e7361d0ec8e84c87d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="row-status-array"></a>행 상태 배열이
데이터 뿐만 아니라 **SQLFetch** 및 **SQLFetchScroll** 행 집합의 각 행의 상태를 제공 하는 배열을 반환할 수 있습니다. 이 배열은 SQL_ATTR_ROW_STATUS_PTR 문 특성을 통해 지정 됩니다. 이 배열은 응용 프로그램에 의해 할당 되 고 SQL_ATTR_ROW_ARRAY_SIZE 문 특성에 의해 지정 된 만큼의 요소에 있어야 합니다. 값 배열에 의해 설정 된 **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**, 및 **SQLSetPos 합니다.** 값의 상태는 행 및 해당 상태의 마지막으로 인출 된 후에 변경 되었는지 여부를 설명 합니다.  
  
|행 상태 배열 값입니다.|Description|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|행이 인출 된 성공적으로 및 마지막으로 인출 된 이후 변경 되지 않은 합니다.|  
|SQL_ROW_SUCCESS_WITH_INFO|행이 인출 된 성공적으로 및 마지막으로 인출 된 이후 변경 되지 않은 합니다. 그러나 행에 대 한 경고가 반환 되었습니다.|  
|SQL_ROW_ERROR|행을 인출 하는 동안 오류가 발생 했습니다.|  
|SQL_ROW_UPDATED|행이 인출 된 성공적으로 및 마지막으로 인출 된 이후에 업데이트 되었습니다. 행이 다시 인출 되거나을 새로 고칠 경우 **SQLSetPos**, 새 상태에 해당 상태가 변경 됩니다.<br /><br /> 일부 드라이버는 데이터의 변경 내용을 검색할 수 없습니다 및이 값을 반환할 수 없습니다. 드라이버에 따라 다시 인출 된 행에 업데이트를 검색할 수 있는지를 확인 하려면 응용 프로그램이 호출 **SQLGetInfo** SQL_ROW_UPDATES 옵션을 사용 합니다.|  
|SQL_ROW_DELETED|마지막으로 인출 된 이후 행 삭제 되었습니다.|  
|SQL_ROW_ADDED|의해 삽입 된 행 **SQLBulkOperations**합니다. 행이 다시 인출 됩니다 하거나 새로 고쳐질 **SQLSetPos**, 상태 SQL_ROW_SUCCESS입니다.<br /><br /> 이 값 설정 하지 않으면 **SQLFetch** 또는 **SQLFetchScroll**합니다.|  
|SQL_ROW_NOROW|행 집합 결과 집합의 끝 겹쳐진 및 행 상태 배열이의이 요소에 상응 하는 행이 반환 되었습니다.|
