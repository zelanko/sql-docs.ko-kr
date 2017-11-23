---
title: "인출 및 업데이트 행 집합 (ODBC) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-how-to
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: rowsets [ODBC]
ms.assetid: cf0eb3b4-8b72-49fc-a845-95edc360cf93
caps.latest.revision: "12"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 86e7aa7654e6350582ef8b2975492ed223f218ee
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="fetch-and-update-rowsets-odbc"></a>행 집합 인출 및 업데이트(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

    
### <a name="to-fetch-and-update-rowsets"></a>행 집합을 인출하고 업데이트하려면  
  
1.  필요에 따라 호출 [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) 와 필요한 경우 sql_row_array_size와 행 집합의 행 (R) 수를 변경 합니다.  
  
2.  호출 [SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401) 또는 [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) 행 집합을 얻으려고 합니다.  
  
3.  바인딩된 열이 사용된 경우 행 집합의 바인딩된 열 버퍼에 있는 데이터 값과 데이터 길이를 사용합니다.  
  
     바인딩되지 않은 열이 사용된 경우 각 행에 대해 SQL_POSITION과 함께 [SQLSetPos](http://go.microsoft.com/fwlink/?LinkId=58407) 를 호출하여 커서 위치를 설정한 다음 바인딩되지 않은 각 열에 대해 다음을 수행합니다.  
  
    -   호출 [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) 바인딩된 마지막 열 행 집합의 한 후 한 번 이상에 대 한 데이터를 가져오는 바인딩되지 않은 열입니다. 에 대 한 호출이 [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) 의 열 번호를 오름차순 이어야 합니다.  
  
    -   [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md)를 여러 번 호출하여 텍스트나 이미지 열에서 데이터를 가져옵니다.  
  
4.  실행 시 데이터 텍스트 또는 이미지 열을 설정합니다.  
  
5.  [SQLSetPos](http://go.microsoft.com/fwlink/?LinkId=58407) 또는 [SQLBulkOperations](http://go.microsoft.com/fwlink/?LinkId=58398) 를 호출하여 행 집합 내에서 커서 위치를 설정하거나 행을 새로 고침, 업데이트, 삭제 또는 추가합니다.  
  
     업데이트 또는 추가 작업에 실행 시 데이터 텍스트 또는 이미지 열이 사용된 경우 해당 열을 처리합니다.  
  
6.  필요에 따라 커서 이름을 지정 하는 위치 지정된 UPDATE 또는 DELETE 문의 실행 (에서 사용할 수 있는 [SQLGetCursorName](../../../relational-databases/native-client-odbc-api/sqlgetcursorname.md)) 동일한 연결에서 다른 문 핸들을 사용 하 고 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [커서 방법 도움말 항목 &#40; ODBC &#41;를 사용 하 여](../../../relational-databases/native-client-odbc-how-to/cursors/using-cursors-how-to-topics-odbc.md)  
  
  
