---
description: 커서 행 집합 크기
title: 커서 행 집합 크기 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], rowset size
- ODBC cursors, rowset size
- rowsets [ODBC]
ms.assetid: 2febe2ae-fdc1-490e-a79f-c516bc8e7c3f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 66d8314123ffd37bb8163dc18900e62b252a6ce0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473754"
---
# <a name="cursor-rowset-size"></a>커서 행 집합 크기
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  ODBC 커서는 한 번에 한 행씩만 인출하도록 제한되지 않습니다. **Sqlfetch** 또는 [sqlfetchscroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)에 대 한 각 호출에서 여러 행을 검색할 수 있습니다. Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 같은 클라이언트/서버 데이터베이스 작업을 할 때는 한 번에 여러 행을 인출하는 것이 효율적입니다. 인출 시 반환 되는 행 수는 행 집합 크기 라고 하며 [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)의 SQL_ATTR_ROW_ARRAY_SIZE을 사용 하 여 지정 됩니다.  
  
```  
SQLUINTEGER uwRowsize;  
SQLSetStmtAttr(m_hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)uwRowsetSize, SQL_IS_UINTEGER);  
```  
  
 행 집합 크기가 1보다 큰 커서를 블록 커서라고 합니다.  
  
 블록 커서를 위해 결과 집합 열을 바인딩하는 다음 두 가지 옵션이 있습니다.  
  
-   열 단위 바인딩  
  
     각 열이 변수 배열에 바인딩됩니다. 각 배열의 요소 수는 행 집합 크기와 같습니다.  
  
-   행 단위 바인딩  
  
     행의 모든 열에 대한 데이터와 표시기가 포함된 구조를 사용하여 배열이 작성됩니다. 배열의 구조 수는 행 집합 크기와 같습니다.  
  
 열 단위 또는 행 단위 바인딩을 사용할 경우 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출할 때마다 바인딩된 배열이 검색 된 행 집합의 데이터로 채워집니다.  
  
 [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) 는 블록 커서에서 열 데이터를 검색 하는 데도 사용할 수 있습니다. **Sqlgetdata** 는 한 번에 한 행씩 작동 하므로 **sqlgetdata** 를 호출 하기 전에 **SQLSetPos** 를 호출 하 여 행 집합의 특정 행을 현재 행으로 설정 해야 합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native CLIENT ODBC 드라이버는 행 집합을 사용 하 여 전체 결과 집합을 신속 하 게 검색 하는 최적화를 제공 합니다. 이 최적화를 사용 하려면 **Sqlexecdirect** 또는 **sqlexecute** 를 호출할 때 커서 특성을 기본값 (앞 으로만 이동, 읽기 전용, 행 집합 크기 = 1)으로 설정 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native CLIENT ODBC 드라이버는 기본 결과 집합을 설정 합니다. 스크롤 없이 결과를 클라이언트로 전송하는 경우 이 방법이 서버 커서보다 더 효율적입니다. 문이 실행된 후 행 집합 크기를 늘리고 열 단위 또는 행 단위 바인딩을 사용합니다. 이렇게 하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기본 결과 집합을 사용 하 여 클라이언트에 결과 행을 효율적으로 보낼 수 있으며, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] NATIVE client ODBC 드라이버는 계속 해 서 클라이언트의 네트워크 버퍼에서 행을 가져옵니다.  
  
## <a name="see-also"></a>참고 항목  
 [커서 속성](../../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
  
