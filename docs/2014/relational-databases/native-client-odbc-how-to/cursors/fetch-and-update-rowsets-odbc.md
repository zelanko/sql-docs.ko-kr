---
title: 인출할 행 집합 및 업데이트 (ODBC) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowsets [ODBC]
ms.assetid: cf0eb3b4-8b72-49fc-a845-95edc360cf93
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fc6a5254afc715a950f2d3c63d02bfca7a1890ea
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48076583"
---
# <a name="fetch-and-update-rowsets-odbc"></a>행 집합 인출 및 업데이트(ODBC)
    
### <a name="to-fetch-and-update-rowsets"></a>행 집합을 인출하고 업데이트하려면  
  
1.  필요에 따라 호출할 [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) (R) 행 집합의 행 수를 변경 하려면 필요한 경우 SQL_ROW_ARRAY_SIZE와 합니다.  
  
2.  호출 [SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401) 하거나 [SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md) 행 집합을 가져오려고 합니다.  
  
3.  바인딩된 열이 사용된 경우 행 집합의 바인딩된 열 버퍼에 있는 데이터 값과 데이터 길이를 사용합니다.  
  
     바인딩되지 않은 열이 사용된 경우 각 행에 대해 SQL_POSITION과 함께 [SQLSetPos](http://go.microsoft.com/fwlink/?LinkId=58407) 를 호출하여 커서 위치를 설정한 다음 바인딩되지 않은 각 열에 대해 다음을 수행합니다.  
  
    -   호출 [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) 마지막 행 집합의 열을 바인딩한 후 한 번 이상에 대 한 데이터를 가져올 바인딩되지 않은 열입니다. 에 대 한 호출 [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) 열 번호를 증가 하는 순서에 있어야 합니다.  
  
    -   [SQLGetData](../../native-client-odbc-api/sqlgetdata.md)를 여러 번 호출하여 텍스트나 이미지 열에서 데이터를 가져옵니다.  
  
4.  실행 시 데이터 텍스트 또는 이미지 열을 설정합니다.  
  
5.  [SQLSetPos](http://go.microsoft.com/fwlink/?LinkId=58407) 또는 [SQLBulkOperations](http://go.microsoft.com/fwlink/?LinkId=58398) 를 호출하여 행 집합 내에서 커서 위치를 설정하거나 행을 새로 고침, 업데이트, 삭제 또는 추가합니다.  
  
     업데이트 또는 추가 작업에 실행 시 데이터 텍스트 또는 이미지 열이 사용된 경우 해당 열을 처리합니다.  
  
6.  커서 이름을 지정 하는 위치 지정된 UPDATE 또는 DELETE 문의 필요에 따라 실행 (에서 사용할 수 있습니다 [SQLGetCursorName](../../native-client-odbc-api/sqlgetcursorname.md)) 및 동일한 연결에서 다른 문 핸들을 사용 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [커서 방법 도움말 항목을 사용 하 여 &#40;ODBC&#41;](using-cursors-how-to-topics-odbc.md)  
  
  
