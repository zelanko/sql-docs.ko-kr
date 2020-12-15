---
description: 행 집합 바인딩 사용(ODBC)
title: 행 집합 바인딩 사용 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowset binding [ODBC]
ms.assetid: a7be05f0-6b11-4b53-9fbc-501e591eef09
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 794ec9c416a6004674c965354f7c98316ef4c32b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467754"
---
# <a name="use-rowset-binding-odbc"></a>행 집합 바인딩 사용(ODBC)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

    
### <a name="to-use-column-wise-binding"></a>열 단위 바인딩을 사용하려면  
  
1.  바인딩된 각 열에 대해 다음을 수행합니다.  
  
    -   데이터 값을 저장할 R개 이상의 열 버퍼 배열을 할당합니다. 여기서 R은 행 집합의 행 수입니다.  
  
    -   필요에 따라 데이터 길이를 저장할 R개 이상의 열 버퍼 배열을 할당합니다.  
  
    -   [SQLBindCol](../../../relational-databases/native-client-odbc-api/sqlbindcol.md) 을 호출하여 열의 데이터 값 및 데이터 길이 배열을 행 집합의 열에 바인딩합니다.  
  
2.  [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) 을 호출하여 다음 특성을 설정합니다.  
  
    -   SQL_ATTR_ROW_ARRAY_SIZE를 행 집합의 행 수(R)로 설정합니다.  
  
    -   SQL_ATTR_ROW_BIND_TYPE을 SQL_BIND_BY_COLUMN으로 설정합니다.  
  
    -   SQL_ATTR_ROWS FETCHED_PTR 특성을 인출된 행 수를 보유하는 SQLUINTEGER 변수를 가리키도록 설정합니다.  
  
    -   SQL_ATTR_ROW_STATUS_PTR을 행 상태 표시를 보유하는 SQLUSSMALLINT 변수의 배열[R]을 가리키도록 설정합니다.  
  
3.  해당 문을 실행합니다.  
  
4.  [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md) 또는 [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) 에 대한 각 호출에서 R개의 행을 검색하여 데이터를 바인딩된 열로 전송합니다.  

### <a name="to-use-row-wise-binding"></a>행 단위 바인딩을 사용하려면  
  
1.  구조의 배열[R]을 할당합니다. 여기서 R은 행 집합의 행 수입니다. 구조에는 각 열에 대해 요소가 하나씩 포함되고 각 요소에는 두 부분이 포함됩니다.  
  
    -   첫 번째 부분은 열 데이터를 보유하는 적절한 데이터 형식의 변수입니다.  
  
    -   두 번째 부분은 열 상태 표시를 보유하는 SQLINTEGER 변수입니다.  
  
2.  [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) 을 호출하여 다음 특성을 설정합니다.  
  
    -   SQL_ATTR_ROW_ARRAY_SIZE를 행 집합의 행 수(R)로 설정합니다.  
  
    -   SQL_ATTR_ROW_BIND_TYPE을 1단계에서 할당한 구조의 크기로 설정합니다.  
  
    -   SQL_ATTR_ROWS_FETCHED_PTR 특성을 인출된 행 수를 보유하는 SQLUINTEGER 변수를 가리키도록 설정합니다.  
  
    -   SQL_ATTR_PARAMS_STATUS_PTR을 행 상태 표시를 보유하는 SQLUSSMALLINT 변수의 배열[R]을 가리키도록 설정합니다.  
  
3.  결과 집합의 각 열에 대해 [SQLBindCol](../../../relational-databases/native-client-odbc-api/sqlbindcol.md) 을 호출하여 열의 데이터 값 및 데이터 길이 포인터가 1단계에서 할당한 구조 배열의 첫 번째 요소에 있는 해당 변수를 가리키도록 합니다.  
  
4.  해당 문을 실행합니다.  
  
5.  [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md) 또는 [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) 에 대한 각 호출에서 R개의 행을 검색하여 데이터를 바인딩된 열로 전송합니다.  
  
## <a name="see-also"></a>참고 항목  
 [커서 사용 방법 항목 ODBC&#41;&#40;](../../../relational-databases/native-client-odbc-how-to/cursors/using-cursors-how-to-topics-odbc.md)   
 [커서 구현 방법](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)   
 [ODBC&#41;&#40;커서 사용 ](../../../relational-databases/native-client-odbc-how-to/cursors/use-cursors-odbc.md)  
  
