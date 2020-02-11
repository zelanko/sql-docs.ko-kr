---
title: 행 집합 인출 및 업데이트 (ODBC) | Microsoft Docs
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
ms.openlocfilehash: f04184e968b60a58c4adfa067d516b58b0a43292
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63200447"
---
# <a name="fetch-and-update-rowsets-odbc"></a>행 집합 인출 및 업데이트(ODBC)
    
### <a name="to-fetch-and-update-rowsets"></a>행 집합을 인출하고 업데이트하려면  
  
1.  필요에 따라 SQL_ROW_ARRAY_SIZE를 사용 하 여 [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) 를 호출 하 여 행 집합의 행 수 (R)를 변경 합니다.  
  
2.  
  [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) 또는 [SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md) 을 호출하여 행 집합을 가져옵니다.  
  
3.  바인딩된 열이 사용된 경우 행 집합의 바인딩된 열 버퍼에 있는 데이터 값과 데이터 길이를 사용합니다.  
  
     바인딩되지 않은 열이 사용된 경우 각 행에 대해 SQL_POSITION과 함께 [SQLSetPos](https://go.microsoft.com/fwlink/?LinkId=58407) 를 호출하여 커서 위치를 설정한 다음 바인딩되지 않은 각 열에 대해 다음을 수행합니다.  
  
    -   
  [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) 를 한 번 이상 호출하여 행 집합의 바인딩된 마지막 열 이후의 바인딩되지 않은 열 데이터를 가져옵니다. 
  [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) 는 번호가 가장 작은 열부터 차례로 호출해야 합니다.  
  
    -   
  [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) 를 여러 번 호출하여 텍스트나 이미지 열에서 데이터를 가져옵니다.  
  
4.  실행 시 데이터 텍스트 또는 이미지 열을 설정합니다.  
  
5.  
  [SQLSetPos](https://go.microsoft.com/fwlink/?LinkId=58407) 또는 [SQLBulkOperations](https://go.microsoft.com/fwlink/?LinkId=58398) 를 호출하여 행 집합 내에서 커서 위치를 설정하거나 행을 새로 고침, 업데이트, 삭제 또는 추가합니다.  
  
     업데이트 또는 추가 작업에 실행 시 데이터 텍스트 또는 이미지 열이 사용된 경우 해당 열을 처리합니다.  
  
6.  필요한 경우 커서 이름( [SQLGetCursorName](../../native-client-odbc-api/sqlgetcursorname.md)에서 사용 가능)을 지정하고 같은 연결에서 다른 문 핸들을 사용하여 지정된 UPDATE 문이나 DELETE 문을 실행합니다.  
  
## <a name="see-also"></a>참고 항목  
 [커서 사용 방법 항목 ODBC&#41;&#40;](using-cursors-how-to-topics-odbc.md)  
  
  
