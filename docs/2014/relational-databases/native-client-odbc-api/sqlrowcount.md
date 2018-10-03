---
title: SQLRowCount | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLRowCount function
ms.assetid: 967ed3d4-3d31-4485-ac92-027076ebc829
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9858619250b5f71e973e4af8eb92868f094e2193
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48165033"
---
# <a name="sqlrowcount"></a>SQLRowCount
  문 실행에 대 한 매개 변수 값의 배열을 바인딩한 경우 때 `SQLRowCount` 매개 변수 값의 모든 행 문 실행에서 오류 조건을 생성 하는 경우 SQL_ERROR를 반환 합니다. 이 함수의 *RowCountPtr* 인수를 통해서는 값이 반환되지 않습니다.  
  
 응용 프로그램에서는 SQL_ATTR_PARAMS_PROCESSED_PTR 매개 변수 특성을 사용하여 오류가 발생하기 전에 처리된 매개 변수 수를 캡처할 수 있습니다.  
  
 또한 응용 프로그램에서는 SQL_ATTR_PARAM_STATUS_PTR 문 특성을 사용하여 바인딩된 상태 값의 배열을 사용하여 문제를 일으키는 매개 변수 행의 배열 오프셋을 캡처할 수도 있습니다. 응용 프로그램에서는 상태 배열을 트래버스하여 처리된 실제 행 수를 확인할 수 있습니다.  
  
 경우는 [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT, UPDATE, DELETE 또는 MERGE 문의 OUTPUT 절을 사용 하 여 실행 되 고, SQLRowCount OUTPUT 절에서 생성 한 결과 집합의 모든 행이 소비 될 때까지 영향을 받는 행의 수를 반환 하지 것입니다. 소비이 행 호출 SQLFetch 또는 SQLFetchScroll입니다. 모든 결과 행이 소비 될 때까지 SQLResultCols는-1을 반환 합니다. SQLFetch 또는 SQLFetchScroll sql_no_data가 반환 된 후 응용 프로그램을 다음 결과로 이동할 SQLMoreResults를 호출 하기 전에 영향을 받는 행 수를 확인 하려면 SQLRowCount 호출 해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQLRowCount 함수](http://go.microsoft.com/fwlink/?LinkId=59367)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
