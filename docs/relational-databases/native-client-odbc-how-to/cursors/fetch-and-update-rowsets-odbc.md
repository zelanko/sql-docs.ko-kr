---
description: 행 집합 인출 및 업데이트(ODBC)
title: 행 집합 인출 및 업데이트 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowsets [ODBC]
ms.assetid: cf0eb3b4-8b72-49fc-a845-95edc360cf93
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b5eaa9a150589cbdf41a41d3528b2b49b00cd7c9
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467764"
---
# <a name="fetch-and-update-rowsets-odbc"></a>행 집합 인출 및 업데이트(ODBC)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

    
### <a name="to-fetch-and-update-rowsets"></a>행 집합을 인출하고 업데이트하려면  
  
1.  필요에 따라 SQL_ROW_ARRAY_SIZE를 사용 하 여 [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) 를 호출 하 여 행 집합의 행 수 (R)를 변경 합니다.  
  
2.  [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md) 또는 [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) 을 호출하여 행 집합을 가져옵니다.  
  
3.  바인딩된 열이 사용된 경우 행 집합의 바인딩된 열 버퍼에 있는 데이터 값과 데이터 길이를 사용합니다.  
  
     바인딩되지 않은 열이 사용된 경우 각 행에 대해 SQL_POSITION과 함께 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md) 를 호출하여 커서 위치를 설정한 다음 바인딩되지 않은 각 열에 대해 다음을 수행합니다.  
  
    -   [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) 를 한 번 이상 호출하여 행 집합의 바인딩된 마지막 열 이후의 바인딩되지 않은 열 데이터를 가져옵니다. [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) 는 번호가 가장 작은 열부터 차례로 호출해야 합니다.  
  
    -   [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) 를 여러 번 호출하여 텍스트나 이미지 열에서 데이터를 가져옵니다.  
  
4.  실행 시 데이터 텍스트 또는 이미지 열을 설정합니다.  
  
5.  [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md) 또는 [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md) 를 호출하여 행 집합 내에서 커서 위치를 설정하거나 행을 새로 고침, 업데이트, 삭제 또는 추가합니다.  
  
     업데이트 또는 추가 작업에 실행 시 데이터 텍스트 또는 이미지 열이 사용된 경우 해당 열을 처리합니다.  
  
6.  필요한 경우 커서 이름( [SQLGetCursorName](../../../relational-databases/native-client-odbc-api/sqlgetcursorname.md)에서 사용 가능)을 지정하고 같은 연결에서 다른 문 핸들을 사용하여 지정된 UPDATE 문이나 DELETE 문을 실행합니다.  
  
## <a name="see-also"></a>참고 항목  
 [커서 사용 방법 항목 ODBC&#41;&#40;](../../../relational-databases/native-client-odbc-how-to/cursors/using-cursors-how-to-topics-odbc.md)  
  
